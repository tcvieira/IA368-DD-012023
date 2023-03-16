# Assigment Week 2

## Code

**cross-encoder**

Reranqueamento usando um modelo estilo-BERT com o treinamento no dataset do MS MARCO e avaliação no TREC-DL 2020
O treinamento é igual ao de um classificador binário, que será feito por vocês.
O que muda é a forma de avaliação: reranqueadores precisam ser alimentados com documentos candidatos (ex: trazidos pelo BM25 - exercício aula 1)

**Sugestão**: usar este dataset reduzido do MS MARCO como treinamento, com 10k triplas (query, passagem relevante, passagem não-relevante):
https://storage.googleapis.com/unicamp-dl/ia368dd_2023s1/msmarco/msmarco_triples.train.tiny.tsv

**Sugestão**: usar miniLM (modelo BERT pequeno, 5x mais rapido) para começar o finetuning: https://huggingface.co/nreimers/MiniLM-L6-H384-uncased pois oferece um bom compromisso entre qualidade e velocidade.

**Sugestão**: usar este notebook como base
Análise de sentimentos (dataset IMDB) usando um modelo estilo BERT: https://colab.research.google.com/drive/10etP7Lb915EC-uEuf1IKC8DYkyg_om6-?usp=sharing

**Sugestão de debug**: usar este minilm para ver se consegue ndcg ~0.70: https://huggingface.co/cross-encoder/ms-marco-MiniLM-L-6-v2

**Sugestão**: fazer overfit em um batch: treinar por 200 epocas um unico batch, e ver se consegue loss=0, e accuracia=100%, ou ndcg=1


[![google colab link](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/tcvieira/IA368-DD-012023/blob/main/assingments/02/notebook.ipynb)

## Reading

[Pretrained Transformers for Text Ranking: BERT and Beyond - Chapter 3 till section 3.2.2] (https://arxiv.org/abs/2010.06467)

[slides pdf](slides-article.pdf)
[slides markdown](slides-article.md)

### Questions

- **what is DCG - Discount Cumulative Gain**
  - Discounted Cumulative Gain is used for tasks with graded relevance, i.e. when the true score y of a document d is a discrete value in a scale measuring the relevance w.r.t. a query q. A typical scale is 0 (bad), 1 (fair), 2 (good), 3 (excellent), 4 (perfect).
  - For a given query q and corresponding documents D = {d₁, …, dₙ}, we consider the the k-th top retrieved document. The gain Gₖ = 2^yₖ – 1 measures how useful is this document (we want documents with high relevance!), while the discount Dₖ = 1/log(k+1) penalizes documents that are retrieved with a lower rank (we want relevant documents in the top ranks!).
  - The sum of the discounted gain terms GₖDₖ for k = 1…n is the Discounted Cumulative Gain (DCG). To make sure that this score is bound between 0 and 1, we can divide the measured DCG by the ideal score IDCG obtained if we ranked documents by the true value yₖ. This gives us the Normalized Discounted Cumulative Gain (NDCG), where NDCG = DCG/IDCG.

## ChatGPT Q&A

