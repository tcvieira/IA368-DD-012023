# Notes from Document Expansion by Query Prediction and doc2query to docTTTTTquery

## Document Expansion by Query Prediction

> https://arxiv.org/pdf/1904.08375.pdf

- Simple Idea
  - The idea behind doc2query a form of document expansion, is to train a model, that when given  an input document, generates questions that the document might answer. These predicted questions are then appended to the original documents, which are then indexed as before.
- The model can be used for query generation to learn semantic search models without requiring annotated training data: Synthetic Query Generation.

- add somenthing about Symmetric and asymmetric semantic search - https://github.com/UKPLab/sentence-transformers/tree/master/examples/applications/semantic-search

- alucina gerando queries q n tem nada a ver
- usam ranking pra saber quais queries sintéticas vão para o índice
- doc2query com reranqueador para filtrar queries: https://arxiv.org/pdf/2301.03266.pdf
- recomendado para docs não muito grandes pq a indexação é lenta

## Article From doc2query to docTTTTTquery

> https://www.researchgate.net/profile/Rodrigo-Nogueira-19/publication/360890853_From_doc2query_to_docTTTTTquery/links/6290b0e98d19206823dfcc55/From-doc2query-to-docTTTTTquery.pdf

- ficou melhor só com as queries do que somente com o texto. Melhor resultado com o doc + queries
- follows the idea of `Document Expansion by Query Prediction` but using T5-base as a seq2seq expansion model
- T5 is a full transformer with encoder-decoder structure with a objective train like BERT to predict the next word of a sequence
- train the model with the MSMARCO passage and ask to generate the question
- trained the model with a constant learning rate of 10−4 for 4k iterations with batches of 256, which corresponds to 2 epochs with the MS MARCO training set. A maximum of 512 input tokens and 64 output tokens
- none of the MSMARCO dataset inputs or outputs have to be truncated when using these lengths
- found that the top-k (used k=10) sampling decoder produces more effective queries than beam search - **check with top-p on code assignment**
- the expanded queries are appended to the original documents, but not specially delimited. All expanded documents are then indexed with the Anserini.
- For evaluation, dev/test questions are issued against the index as “bag of words” queries, using the BM25 ranking function with Anserini’s default parameters.
- We also evaluate the queries produced by the models against the ground truth dev queries in terms of BLEU: docTTTTTquery scores 0.21 BLEU, which is much higher than doc2query, 0.088 BLEU. We attribute this large difference in output quality to pretraining and not to the size of the model itself, as even the T5-small model, which has a similar number of parameters as the doc2query model, achieves 0.18 BLEU.
- the latency on doctttttquery is better than bm25 + bert, bit the MRR@10 is worse.
- copying terms in expansion has the effect of term re-weighting while expanding with new terms mitigates the vocabulary mismatch problem, thus increasing recall.

## TODO

- articles/videos about document expansion
- articles/videos T5

## ChatGPT

**what is Synthetic Query Generation**

> Synthetic Query Generation refers to the process of generating queries or search requests artificially, often using machine learning techniques, rather than relying on queries submitted by actual users.
>
> In this process, algorithms are trained on a large corpus of data, such as web pages, documents, or other sources of information, to learn how to generate relevant and useful queries. The generated queries can then be used to retrieve information from a database or search engine.
>
> Synthetic Query Generation can be useful in various applications, such as improving the accuracy of search results, generating training data for machine learning models, or automating the process of creating queries for complex information retrieval tasks.

**how can build a model for Synthetic Query generation to be used on a corpus of documents to build a FAQ?**

>Building a model for Synthetic Query Generation to create a FAQ involves the following steps:
>
>Data Preparation: Collect a corpus of documents related to the topic of the FAQ. Preprocess the data by removing stopwords, stemming, and lemmatizing the text.
>
>Query Generation Model: Train a machine learning model to generate queries based on the input document. You can use techniques such as neural networks or deep learning to create the model.
>
>Query Ranking: Rank the generated queries based on their relevance to the document. You can use techniques such as semantic similarity or cosine similarity to measure the similarity between the query and the document.
>
>Answer Extraction: Extract the answers from the document for the generated queries. You can use techniques such as Named Entity Recognition (NER) or Part of Speech (POS) tagging to extract the relevant information.
>
>Build FAQ: Compile the generated queries and their corresponding answers into a Frequently Asked Questions (FAQ) document.
>
>Evaluation: Evaluate the performance of the model using metrics such as precision, recall, and F1-score. This will help you to improve the performance of the model by fine-tuning the parameters or adding more training data.
>
>By following these steps, you can build a model for Synthetic Query Generation that can be used to create a comprehensive FAQ document.
