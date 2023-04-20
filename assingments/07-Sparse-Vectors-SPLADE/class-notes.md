# Class 7 Notes 20/04/2023

- **APRESENTAÇÕES ARTIGO DPR - Dense Passage Retriever + ColBERT**

- combinação com BM25 piorou, pq?
  - combinação de um classificador forte e outro fraco, de maneira geral piora o modelo com ensemble
- buscadores densos (um vetor só para q e d) tem problemas com siglas ou palavras que não foi vista apesar de ter o contexto.
- loss ColBERT
  - score_pos = 5.1
  - score_neg = 1.0
  - loss = -log (score_pos / (score_pos + score_neg)) (mais próximo de 1 melhor, mais próximo de o pior. descontado pelo score do neg)
- ColBERT melhor para paralelizar (tenta casar os embeddings de modelo denso com sim por tokens com o documento)
- ColBERT tem os beneficios das representacoes densas e contextualizadas + a representação por token (semelhantes entre q e d) que melhora a granularidade.
- no DPR documentos maiores podem estar mais ruidosos com relação ao ColBERT
- BERT >> W2V. pq W2V não é contextualizado (semântica) e vocab limitado, no BERT palavras iguais em contexto diferentes tem diferentes representações também.
- ColBERT precisa de mt ram pra ter os embeddings na memoria em comparação com o DPR, vide print
  - ColBERTv2 tenta melhorar esse ponto
- ColBERT tem tipo uma query expansion ao fazer padding em queries pequenas com [MASKS], o que pode acabar contribuindo nos position embeddings apesar desses [MASKS] não trazerem informação nova.

- **APRESENTAÇÕES NOTEBOOK**
  
- **Refs**
  
## article

- SPLADE busca esparsa e SPLADE v2
  - SPLADE: Sparse Lexical and Expansion Model
for First Stage Ranking - https://arxiv.org/pdf/2107.05720.pdf
  - SPLADE v2: Sparse Lexical and Expansion Model for
Information Retrieval - https://arxiv.org/pdf/2109.10086.pdf
- vetores do tamanho do vocab
- pode ser entendido como uma expansão de docs

## code assignment
