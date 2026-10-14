#!/usr/bin/env python3
"""Count lines of code per language across a GitHub user's repositories (via cloc)
and rewrite the section between <!--LOC:START--> and <!--LOC:END--> in README.md.

Environment variables
  GH_USER           GitHub username (required unless --local is used)
  GH_TOKEN          token used to list/clone repos (required unless --local is used)
  INCLUDE_PRIVATE   "true" to include private repos (needs a PAT with repo read access). Default: false
  EXCLUDE_REPOS     comma-separated repo names to skip (e.g. "dotfiles,scratch")
  EXCLUDE_LANGS     comma-separated cloc language names to ignore
  TOP_N             languages shown before grouping the rest as "Other". Default: 8

Usage
  python scripts/update_loc.py                 # GitHub mode (used by the workflow)
  python scripts/update_loc.py --local DIR...  # count local folders (for testing)
"""
import argparse
import base64
import json
import os
import shutil
import subprocess
import sys
import tempfile
import urllib.request
from collections import defaultdict
from datetime import datetime, timezone

START, END = "<!--LOC:START-->", "<!--LOC:END-->"
DEFAULT_EXCLUDE_LANGS = "JSON,YAML,XML,CSV,SVG,Markdown,Text,Jupyter Notebook,SUM,header"
EXCLUDE_DIRS = (
    ".git,node_modules,dist,build,out,target,vendor,venv,.venv,env,__pycache__,"
    ".next,.nuxt,coverage,staticfiles,migrations,site-packages,.idea,.vscode"
)
EXCLUDE_FILES = r"(package-lock\.json|pnpm-lock\.yaml|yarn\.lock|poetry\.lock|Cargo\.lock|.*\.min\.(js|css))"


def api(url, token):
    req = urllib.request.Request(url, headers={
        "Authorization": f"Bearer {token}",
        "Accept": "application/vnd.github+json",
        "X-GitHub-Api-Version": "2022-11-28",
    })
    with urllib.request.urlopen(req) as r:
        return json.load(r)


def list_repos(user, token, include_private, exclude):
    repos, page = [], 1
    while True:
        if include_private:
            url = f"https://api.github.com/user/repos?affiliation=owner&per_page=100&page={page}"
        else:
            url = f"https://api.github.com/users/{user}/repos?type=owner&per_page=100&page={page}"
        batch = api(url, token)
        if not batch:
            break
        repos.extend(batch)
        page += 1
    out = []
    for r in repos:
        if r["owner"]["login"].lower() != user.lower():
            continue
        if r["fork"] or r["name"] in exclude:
            continue
        if r["private"] and not include_private:
            continue
        out.append(r)
    return out


def clone(repo, token, dest):
    basic = base64.b64encode(f"x-access-token:{token}".encode()).decode()
    subprocess.run(
        ["git", "-c", f"http.extraheader=AUTHORIZATION: basic {basic}",
         "clone", "--depth", "1", "--quiet", repo["clone_url"], dest],
        check=True, stdout=subprocess.DEVNULL,
    )


def run_cloc(path, skip_langs):
    cmd = ["cloc", "--json", "--quiet", f"--exclude-dir={EXCLUDE_DIRS}",
           f"--not-match-f={EXCLUDE_FILES}", path]
    res = subprocess.run(cmd, capture_output=True, text=True)
    if res.returncode != 0 or not res.stdout.strip():
        return {}
    data = json.loads(res.stdout)
    return {lang: v["code"] for lang, v in data.items()
            if lang not in skip_langs and isinstance(v, dict)}


def bar(share, width=20):
    filled = round(share * width)
    return "█" * filled + "░" * (width - filled)


def render(totals, repo_count, scope, top_n):
    ordered = sorted(totals.items(), key=lambda kv: kv[1], reverse=True)
    total = sum(totals.values())
    shown, rest = ordered[:top_n], ordered[top_n:]
    if rest:
        shown.append(("Other", sum(v for _, v in rest)))
    lines = [
        "| Language | Lines of code | Share | |",
        "|---|--:|--:|---|",
    ]
    for lang, n in shown:
        share = n / total if total else 0
        lines.append(f"| {lang} | {n:,} | {share:.1%} | `{bar(share)}` |")
    lines.append(f"| **Total** | **{total:,}** | 100% | |")
    stamp = datetime.now(timezone.utc).strftime("%Y-%m-%d")
    lines.append("")
    lines.append(f"<sub>{repo_count} {scope} repositories (forks excluded) · "
                 f"generated and vendored files ignored · updated {stamp} (UTC)</sub>")
    return "\n".join(lines)


def inject(readme_path, block):
    with open(readme_path, encoding="utf-8") as f:
        text = f.read()
    if START not in text or END not in text:
        sys.exit(f"Markers {START} / {END} not found in {readme_path}")
    head, rest = text.split(START, 1)
    _, tail = rest.split(END, 1)
    new = f"{head}{START}\n{block}\n{END}{tail}"
    with open(readme_path, "w", encoding="utf-8") as f:
        f.write(new)


def main():
    ap = argparse.ArgumentParser()
    ap.add_argument("--readme", default="README.md")
    ap.add_argument("--local", nargs="+", help="count these folders instead of calling GitHub")
    args = ap.parse_args()

    skip = {s.strip() for s in os.getenv("EXCLUDE_LANGS", DEFAULT_EXCLUDE_LANGS).split(",") if s.strip()}
    top_n = int(os.getenv("TOP_N", "8"))
    totals, count = defaultdict(int), 0

    if args.local:
        for path in args.local:
            for lang, n in run_cloc(path, skip).items():
                totals[lang] += n
            count += 1
        scope = "local"
    else:
        user, token = os.environ["GH_USER"], os.environ["GH_TOKEN"]
        include_private = os.getenv("INCLUDE_PRIVATE", "false").lower() == "true"
        exclude = {s.strip() for s in os.getenv("EXCLUDE_REPOS", "").split(",") if s.strip()}
        scope = "public + private" if include_private else "public"
        tmp = tempfile.mkdtemp()
        try:
            for repo in list_repos(user, token, include_private, exclude):
                dest = os.path.join(tmp, repo["name"])
                try:
                    clone(repo, token, dest)
                except subprocess.CalledProcessError:
                    print(f"skip (clone failed): {repo['name']}", file=sys.stderr)
                    continue
                for lang, n in run_cloc(dest, skip).items():
                    totals[lang] += n
                count += 1
                shutil.rmtree(dest, ignore_errors=True)
        finally:
            shutil.rmtree(tmp, ignore_errors=True)

    inject(args.readme, render(totals, count, scope, top_n))
    print(f"done: {sum(totals.values()):,} lines across {count} repos")


if __name__ == "__main__":
    main()
