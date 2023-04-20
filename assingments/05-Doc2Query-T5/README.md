# Assigment Week 5

## Code

**Treinar um modelo seq2seq (a partir do T5-base) na tarefa de expansão de documentos usando o doc2query**

- Usar como treino o dataset "tiny" do MS MARCO na tarefa doc2query
  - https://storage.googleapis.com/unicamp-dl/ia368dd_2023s1/msmarco/msmarco_triples.train.tiny.tsv
- doc2query: A entrada é a passagem e o target é a query
- Note que apenas pares (query, passagem relevante) são usados como treino.
- O treino é relativamente rápido (<1 hora).
- Validar a cada X steps usando o sacreBLEU
- A parte lenta deste exercício é a pré-indexação: para cada documento da coleção, temos que gerar uma ou mais queries, que depois são concatenadas ao documento original, e esse documento "expandido" é indexado.
- Avaliar no TREC-COVID (171K docs), pois é menor que o MS MARCO/TREC-DL 2020 (8.8M passagens). 
- Indice invertido do Trec-covid no pyserini: beir-v1.0.0-trec-covid-flat
- Corpus e queries na HF: https://huggingface.co/datasets/BeIR/trec-covid
- qrels: https://huggingface.co/datasets/BeIR/trec-covid-qrels
- Usar nDCG@10
- Comparar com o BM25 com e sem os documentos expandidos pelo doc2query


[![google colab link](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/tcvieira/IA368-DD-012023/blob/main/assingments/05/notebook.ipynb)

[notebook](notebook.ipynb)

[code slides](code-slides.pdf)

[code notes](code-notes.pdf)

## Reading

[Document Expansion by Query Prediction](https://arxiv.org/pdf/1904.08375.pdf)

[From doc2query to docTTTTTquery](https://www.researchgate.net/profile/Rodrigo-Nogueira-19/publication/360890853_From_doc2query_to_docTTTTTquery/links/6290b0e98d19206823dfcc55/From-doc2query-to-docTTTTTquery.pdf)

[article slides pdf](article-slides.pdf)

[article slides markdown](article-slides.md)

[article notes](article-notes.md)
