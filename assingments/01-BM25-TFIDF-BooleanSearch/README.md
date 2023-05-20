# Assigment Week 1

## Code

> 1. Usar o BM25 implementado pelo pyserini para buscar queries no TREC-DL 2020 - **DONE**
> 
> Documentação referencia: 
> 
> https://github.com/castorini/pyserini/blob/master/docs/experiments-msmarco-passage.md
> https://microsoft.github.io/msmarco/TREC-Deep-Learning-2020.html#passage-ranking-task
>
> 2. Implementar um buscador booleano/bag-of-words. - **WIP**
> 3. Implementar um buscador com TF-IDF - **WIP**
> 4. Avaliar implementações 1, 2, e 3 no TREC-DL 2020 e calcular o nDCG@10
>
> Nos itens 2 e 3:
> Fazer uma implementação que suporta buscar eficientemente milhões de documentos.
> Não se pode usar bibliotecas como sklearn, que já implementam o BoW e TF-IDF.

[![google colab link](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/tcvieira/IA368-DD-012023/blob/main/assingments/01-BM25-TFIDF-BooleanSearch/notebook.ipynb)

> **TODO** mentions were added throughout the notebook to indicate some point of lack of understanding or improvements
>
> TREC-DL 2020 corresponds to real-world scenarios where  the number of training queries with at least one positive label is at least in the tens of thousands, if not hundreds of thousands or more.

### ChatGPT Q&A

> **what is TREC Deep Learning Track**
>
> The TREC (Text Retrieval Conference) Deep Learning Track is an annual research competition that focuses on advancing the state of the art in information retrieval (IR) using deep learning techniques.
>
> The track provides a platform for researchers and practitioners to explore the application of deep learning models in IR tasks, such as document ranking and classification, question answering, and entity recognition. Participants are provided with large datasets, and their models are evaluated on various metrics such as precision, recall, and F1-score.
>
> The TREC Deep Learning Track aims to encourage the development of innovative and effective techniques for improving the efficiency and effectiveness of information retrieval systems. It also provides an opportunity for researchers to collaborate and exchange ideas, thereby advancing the field of IR as a whole.

> **what is the MSMARCO dataset**
> 
> The MSMARCO (Microsoft MAchine Reading COmprehension) dataset is a large-scale collection of web passages and their associated queries, designed to facilitate research on machine reading comprehension and information retrieval. It was created by Microsoft Research in collaboration with the academic community.
>
> The dataset consists of two parts: MSMARCO Passage Ranking and MSMARCO Question Answering.
>
> The MSMARCO Passage Ranking dataset contains over 8 million web passages, each with an associated query. The goal is to rank the passages in order of their relevance to the query. This task is typically tackled using information retrieval techniques, such as neural ranking models.
>
> The MSMARCO Question Answering dataset consists of over 100,000 questions and their corresponding answers, extracted from the same web passages used in the passage ranking task. The goal is to answer the questions based on the information in the passages. This task requires both reading comprehension and information retrieval skills.
>
> The MSMARCO dataset has become a popular benchmark for evaluating the performance of machine reading comprehension and information retrieval systems, and it has spurred significant research advances in these fields.

## Reading

[Pretrained Transformers for Text Ranking: BERT and Beyond - Chapter 1] (https://arxiv.org/abs/2010.06467)

[mindmap do artigo](https://mm.tt/map/2632463217?t=Sc3uBhKfwT)

**Probably next time I will use the mindmap as a starting point to produce a slideshow presentation.**
