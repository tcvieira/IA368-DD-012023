# Final Project

## ColBERTv2

- https://github.com/terrier-org/ecir2021tutorial - IR From Bag-of-words to BERT and Beyond through Practical Experiments

## Ideas

- build a Google/NXAi like search engine with selectable ranking and search algorithms. (class 10)
  - https://towardsdatascience.com/elasticsearch-meets-bert-building-search-engine-with-elasticsearch-and-bert-9e74bf5b4cf2
  - https://github.com/jina-ai/clip-as-service

- build a FAQ questions generator
  - doc2query

- eval weak/small reranker models
  - hypothesis: multiple weak/small reranker perfom better on cost/efficiency/time than a big reranker. Is it a good trade-off?

- Finetuning dense retrievers on the generated synthetic data InPars

- build a Q/A chatbot with gpt-index https://gpt-index.readthedocs.io/en/latest/getting_started/starter_example.html
  - GPT4All: Running an Open-source ChatGPT Clone on Your Laptop https://betterprogramming.pub/gpt4all-running-an-open-source-chatgpt-clone-on-your-laptop-71ebe8600c71
  - compare results against Visconde

- build a interface with streamlit like https://github.com/nomic-ai/gpt4all-ui

- create a technical writer Q/A over markdown knowledge base - https://llamahub.ai/l/file-markdown
  - dataset?

- connect a LLM direct to a database for doc2query o create knowledge base

- replicate exercices from the class like, use LLM to answers and create slides in markdown using https://llamahub.ai/l/papers-arxiv

- make something like that https://twitter.com/s_jobs6/status/1618346125697875968?s=20&amp;t=RJhQu2mD0-zZNGfq65xodA (upload a long doc and enable chatting about it..check other examples on the thread) with leis, documentos jurídicos (senteças, petição, hc, etc...), artigos, notícias
  - this can be used to analyse terms of use/services of social media platforms too - https://twitter.com/s_jobs6/status/1619063620104761344

- evaluate some vector databases - https://python.langchain.com/en/latest/modules/indexes/vectorstores.html
  - https://github.com/chroma-core/chroma
  - pinecone
  - vespa
  - redis
  - faiss

- using crafted prompt in different prompt techniques with llms to generate/replace queries on MSMARCO or another dataset and evaluate the result
  - like cot and others
  - some examples https://huyenchip.com/2023/04/11/llm-engineering.html#search_and_recommendation
  - AugGPT: Leveraging ChatGPT for Text Data Augmentation https://arxiv.org/abs/2302.13007

## References

- https://vicuna.lmsys.org/
- https://github.com/nomic-ai/gpt4all
- Locally run an Instruction-Tuned Chat-Style LLM - https://github.com/antimatter15/alpaca.cpp
- https://github.com/tloen/alpaca-lora
- https://llamahub.ai/
- https://gpt-index.readthedocs.io/en/latest/guides/primer.html
- langchain example Q/A https://github.com/hwchase17/notion-qa and https://python.langchain.com/en/latest/use_cases/question_answering.html
- https://www.llmparser.com/
- use a pipeline like https://towardsdatascience.com/build-reliable-machine-learning-pipelines-with-continuous-integration-ea822eb09bf6 with neptune or wb for example

## What is the task?

## What pre-trained SOTA model can be used for the task?

## Fine tunning on own data will be needed?
