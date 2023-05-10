# Class 9 Notes 04/05/2023

- **APRESENTAÇÕES ARTIGO InPars**

- **APRESENTAÇÕES NOTEBOOK**
  
- **Refs**

## article

- ColBERTv2: Effective and Efficient Retrieval via Lightweight Late Interaction

## code assignment

Exercício desta semana: Trade-offs de eficiência e qualidade

O objetivo do exercício desta semana é construir alguns pipelines de busca e analisá-los em termos das seguintes métricas:

- Qualidade dos resultados: nDCG@10;
- Latência (seg/query);
- USD por query assumindo utilização "perfeita": assim que terminou de processar uma query, já tem outra para ser processada;
- USD/mês para deixar o sistema rodando para poucos usuários (ex: 100 queries/dia);
- Custo de indexação em USD;

Iremos avaliar os pipelines no TREC-COVID. 

- A latência precisa ser menor que 2 segundos por query. 
- Não assumir processamento de queries em batch.

Considerar:

- 1,50 USD/hora por A100 ou 0,21 USD/hora por T4 ou 0,50 USD/hora por V100
- 0,03 USD/hora por CPU core
- 0,005 USD/hora por GB de CPU RAM

Dicas:

- Utilizar modelos de busca "SOTA" já treinados no MS MARCO como parte do pipeline, como:

- o SPLADE distil (esparso),
- contriever (denso),
- Colbert-v2 (denso),
- miniLM (reranker), 
- monoT5-3B (reranker), 
- doc2query minus-minus (expansão de documentos + filtragem com reranqueador na etapa de indexação)

> Pode usar API's como Cohere, OpenAI Embeddings

Variar parâmetros como número de documentos retornados em cada estágio:

- Por exemplo, BM25 retorna 1000 documentos, um modelo denso ou esparso pode ranqueá-los, e passar os top 50 para o miniLM/monoT5 fazer um ranqueamento final.
