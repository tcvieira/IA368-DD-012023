# Class 1

> notes from the class of 03/09/23

- ML system we have targets for all inputs and in IR systems we don't have for each query
- remove stopwords from index creation or at the time you add the document and use at the search
- choose tokenizer wisely. Lucene analyzer is much better than nlkt tokenizer
- BoW looks worse than boolean because words with higher freq in docs may be not so important for the query after all.
- create a small dataset to use as test case for the course implementations
- run grid search on BM25 params (is it overfitting for you dataset. is it worth it? maybe in a competition)
- at least 3 slides for the notebook (choose from the 7 questions)
- slides for the article (check instructions)

## TODO

- review IR pipeline (texts -> inverted index -> retriever -> re-rank -> ranked list)
- review MSMARCO and TREC-DL
- what is ndcg ?
