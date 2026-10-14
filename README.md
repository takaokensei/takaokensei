# Cauã Vitor Figueredo Silva

**Inteligência Artificial aplicada a documentos · PLN · RAG · LLMs**
Graduando em Engenharia Elétrica (UFRN) · Pesquisador PIBIC/UFRN · Técnico em Eletrônica (IMD/UFRN)

[![Lattes](https://img.shields.io/badge/Lattes-CNPq-2c4c7c?style=flat-square)](http://lattes.cnpq.br/6248557957222073)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-0A66C2?style=flat-square&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/caua-vitor-7bb072286)
[![E-mail](https://img.shields.io/badge/E--mail-EA4335?style=flat-square&logo=gmail&logoColor=white)](mailto:cauavitorfigueredo@gmail.com)

---

## Sobre

Desenvolvo sistemas de IA para extração, busca e verificação de informação em documentos, com ênfase em textos jurídicos. Na iniciação científica (PIBIC/UFRN), construo pipelines de **RAG** sobre **PostgreSQL + pgvector**, com reranking e validação de fundamentação das respostas para reduzir alucinações. Fora da pesquisa, uso aprendizado de máquina clássico e redes neurais (PyTorch) em projetos acadêmicos com avaliação quantitativa.

**Foco atual**
- RAG com busca semântica, reranking e checagem de fundamentação
- Extração de entidades (NER) e GraphRAG sobre textos em português
- Avaliação de embeddings e modelos de classificação/agrupamento
- Boas práticas de engenharia: testes, CI/CD, Docker e documentação

---

## Stack

| Área | Tecnologias |
|---|---|
| **Linguagens e backend** | Python, Django, FastAPI, Celery, Redis, TypeScript/Node.js, JavaScript, SQL, Rust |
| **IA generativa e LLMs** | RAG, reranking, validação de fundamentação, NER, GraphRAG, engenharia de prompts, CrewAI, Ollama (Llama 3), Groq, OpenAI, Anthropic, Gemini |
| **PLN e Machine Learning** | PyTorch, scikit-learn, Transformers, Sentence-BERT, BGE-M3, GTE, TF-IDF, SVM, XGBoost, Random Forest, k-NN, K-Means, DBSCAN, mapas de Kohonen (SOM) |
| **Dados e infraestrutura** | PostgreSQL + pgvector, Neo4j, Pandas, NumPy, Docker / Docker Compose, GitHub Actions, pytest, Git |
| **Frontend e visualização** | React, TypeScript, Vite, Streamlit |
| **Avaliação** | Validação cruzada K-Fold, otimização bayesiana (Optuna), F1, ARI, NMI, Purity, MSE |

---

## Projetos em destaque

<table>
  <tr>
    <td width="50%" valign="top">
      <a href="https://github.com/takaokensei/jurix">
        <img src="https://readme-stats-mocha-xi.vercel.app/api/pin/?username=takaokensei&repo=jurix&theme=tokyonight&hide_border=true&bg_color=0D1117&title_color=4A6FA5&icon_color=4A6FA5&text_color=9CA3AF&v=1" alt="Jurix"/>
      </a>
      <br/>
      <b>Jurix (PIBIC/UFRN, 2025–2026)</b><br/>
      Plataforma de consolidação normativa e rastreabilidade jurídica da legislação municipal de Natal/RN. RAG sobre PostgreSQL/pgvector, busca com reranking, versionamento temporal das normas, extração de referências e entidades (NER) e validação de fundamentação. Backend em Django com Celery e Redis; inferência local (Ollama) ou em nuvem; Docker Compose e CI/CD.
    </td>
    <td width="50%" valign="top">
      <a href="https://github.com/takaokensei/newslens-classifier">
        <img src="https://readme-stats-mocha-xi.vercel.app/api/pin/?username=takaokensei&repo=newslens-classifier&theme=tokyonight&hide_border=true&bg_color=0D1117&title_color=4A6FA5&icon_color=4A6FA5&text_color=9CA3AF&v=1" alt="NewsLens Classifier"/>
      </a>
      <br/>
      <b>NewsLens Classifier (ELE 606, 2025)</b><br/>
      Classificação de 315 notícias em 6 categorias com SVM e XGBoost. O TF-IDF alcançou 96,8% do desempenho do BERT, com cold start cerca de 28× mais rápido. Servido por API REST em FastAPI, com CI/CD.
    </td>
  </tr>
  <tr>
    <td width="50%" valign="top">
      <a href="https://github.com/takaokensei/nlp-clustering-benchmark">
        <img src="https://readme-stats-mocha-xi.vercel.app/api/pin/?username=takaokensei&repo=nlp-clustering-benchmark&theme=tokyonight&hide_border=true&bg_color=0D1117&title_color=4A6FA5&icon_color=4A6FA5&text_color=9CA3AF&v=1" alt="NLP Clustering Benchmark"/>
      </a>
      <br/>
      <b>NLP Clustering Benchmark (2025)</b><br/>
      Comparação de TF-IDF+SVD, SBERT, GTE-Base e BGE-M3 em 20 Newsgroups e textos curtos em português. Melhor resultado em português: ARI 0,94 e NMI 0,93.
    </td>
    <td width="50%" valign="top">
      <a href="https://github.com/takaokensei/news-clustering-llm">
        <img src="https://readme-stats-mocha-xi.vercel.app/api/pin/?username=takaokensei&repo=news-clustering-llm&theme=tokyonight&hide_border=true&bg_color=0D1117&title_color=4A6FA5&icon_color=4A6FA5&text_color=9CA3AF&v=1" alt="News Clustering LLM"/>
      </a>
      <br/>
      <b>Clustering de notícias com rotulagem por LLMs (2026)</b><br/>
      Pipeline não supervisionado sobre 315 notícias em português, avaliado com ARI, NMI e Purity. Rótulos gerados por LLMs (Gemini e Ollama) e dashboard interativo com busca semântica.
    </td>
  </tr>
</table>

### Outros projetos

- **[NewsGraph](https://github.com/takaokensei/newsgraph)**: extração de entidades com LLMs (saída estruturada em JSON) e construção de grafo de conhecimento no Neo4j.
- **[VerbaFlow](https://github.com/takaokensei/VerbaFlow)**: sistema multiagente para classificação de texto com CrewAI, Llama 3.3 70B (Groq) e interface em Streamlit (Capstone da Formação Cientista de Dados, DSA).
- **[IntraSOM Kohonen](https://github.com/takaokensei/intrasom-kohonen)**: dashboard em React, TypeScript e Vite para mapas auto-organizáveis em séries temporais e agrupamento semântico de textos.
- **[Redes neurais para regressão](https://github.com/takaokensei/ufrn-ele-neural-regression)** (ELE 604): MLP em PyTorch com K-Fold, dropout, regularização L2 e otimização bayesiana (redução de 3,3% no MSE).

---

## Formação e pesquisa

- **Engenharia Elétrica (Bacharelado), UFRN**: 9º período, conclusão prevista para 2027.2. Disciplinas de destaque: Redes Neurais Artificiais e Tópicos Especiais em Inteligência Artificial.
- **Técnico em Eletrônica, IMD/UFRN**: concluído (2020.1 – 2021.1).
- **Iniciação Científica (PIBIC/UFRN)**: PLN e RAG aplicados ao domínio jurídico, sob orientação do Prof. José Alfredo Costa.
- **Certificações**: Formação Cientista de Dados (DSA, 96h), Introdução à Ciência de Dados: Modelos de Classificação (ENAP, 8h), cursos de Python (80h).

---

## Estatísticas do GitHub

<p align="center">
  <img width="49%" src="https://readme-stats-mocha-xi.vercel.app/api?username=takaokensei&show_icons=true&theme=tokyonight&hide_border=true&bg_color=0D1117&title_color=4A6FA5&icon_color=4A6FA5&text_color=9CA3AF&include_all_commits=true&count_private=true&v=1" alt="Estatísticas do GitHub"/>
  <img width="40%" src="https://readme-stats-mocha-xi.vercel.app/api/top-langs/?username=takaokensei&layout=compact&theme=tokyonight&hide_border=true&bg_color=0D1117&title_color=4A6FA5&text_color=9CA3AF&icon_color=4A6FA5&hide=jupyter%20notebook&langs_count=8&v=1" alt="Linguagens mais usadas"/>
</p>

---

## Contato

- E-mail: [cauavitorfigueredo@gmail.com](mailto:cauavitorfigueredo@gmail.com)
- LinkedIn: [caua-vitor-7bb072286](https://www.linkedin.com/in/caua-vitor-7bb072286)
- Lattes: [6248557957222073](http://lattes.cnpq.br/6248557957222073)
