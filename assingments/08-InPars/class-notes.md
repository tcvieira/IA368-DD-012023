# Class 7 Notes 20/04/2023

- **APRESENTAÇÕES ARTIGO DPR - Dense Passage Retriever + ColBERT**

- combinação com BM25 piorou, pq?
  - combinação de um classificador forte e outro fraco, de maneira geral piora o modelo com ensemble
- buscadores densos (um vetor só para q e d) tem problemas com siglas ou palavras que não foi vista apesar de ter o contexto.
- loss ColBERT
  - score_pos = 5.1
  - score_neg = 1.0
  - loss = -log (exp(score_pos) / (exp(score_pos) + exp(score_neg))) (mais próximo de 1 melhor, mais próximo de o pior. descontado pelo score do neg)
- ColBERT melhor para paralelizar (tenta casar os embeddings de modelo denso com sim por tokens com o documento)
- ColBERT tem os beneficios das representacoes densas e contextualizadas + a representação por token (semelhantes entre q e d) que melhora a granularidade.
- no DPR documentos maiores podem estar mais ruidosos com relação ao ColBERT
- BERT >> W2V. pq W2V não é contextualizado (semântica) e vocab limitado, no BERT palavras iguais em contexto diferentes tem diferentes representações também.
- ColBERT precisa de mt ram pra ter os embeddings na memoria em comparação com o DPR, vide print
  - ColBERTv2 tenta melhorar esse ponto
- ColBERT tem tipo uma query expansion ao fazer padding em queries pequenas com [MASKS], o que pode acabar contribuindo nos position embeddings apesar desses [MASKS] não trazerem informação nova.

- **APRESENTAÇÕES NOTEBOOK**

- slides do Leandro Carisio - explicações e implementação da loss
- loss usada no DPR https://github.com/facebookresearch/DPR/blob/main/dpr/models/biencoder.py#L254
- loss do sentence transformers - https://www.sbert.net/docs/package_reference/losses.html?highlight=loss
- eval lib - https://pypi.org/project/rank-eval/
- usar médias dos embeddings ou o cls (qual melhor? parece ser o cls e é mais fácil)
- slides da Monique explicação e análises
- marcos piau - ajuste no max length melhora performance
- CONCLUSOES DO SLIDE DO CURSO
  
- **Refs**

- Contriever: https://huggingface.co/facebook/contriever
- colbert-v2: https://arxiv.org/pdf/2112.01488.pdf
- para ensemble de ranqueadores (sistema de busca) - RRF reciprocal rank fusion
  
## article

- SPLADE busca esparsa e SPLADE v2
  - troca do binarizer do sparterm por uma função ao invés de um PLM (BERT) que naturalmente garante a esparcidade (como?)
  - SPLADE: Sparse Lexical and Expansion Model
  - a representação esparsa é como um BOsubW "contextualizada" apesar da entrada a ordem dos tokens importarem
  - pq quero ter um vetor esparso?
    - assim posso usar o indice invertido para filtrar os doc que contém os tokens
    - diferente do BM25 tentam resolver o problema do vocab onde os termos da query n casam com os termos do vocab
for First Stage Ranking - https://arxiv.org/pdf/2107.05720.pdf
  - SPLADE v2: Sparse Lexical and Expansion Model for
Information Retrieval - https://arxiv.org/pdf/2109.10086.pdf
- vetores do tamanho do vocab
- pode ser entendido como uma expansão de docs
- produto escalar otimizado é a implementacao da função de busca + rank
- indice invertido é um dict ie: "restaur" = (doc2222, 0.5)
- melhor pra integrar com infraestrutura existente elastic em comparação com o denso
- estado da arte em zero-shot - eval.ai leaderboard

## code assignment

- busca igual ao tf-idf da aula 2 + passos de encoding da query + calculo da score do query_doc para os doc trazidos pelo indice invertido
- medir latencia sec/query
