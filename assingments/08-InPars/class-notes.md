# Class 8 Notes 27/04/2023

- **APRESENTAÇÕES ARTIGO SPLADE**

- **APRESENTAÇÕES NOTEBOOK**
  
- **Refs**

## article

- InPars - https://arxiv.org/pdf/2202.05144.pdf
- generate 100k queries in 100k docs, select top10k using the same model and than train
- InPars v2 some improvement using the reranker to select the generate queries

## code assignment

- choose 1k-10k doc to generate queries with few-zero-shot from LLM (sample from dataset because it's 170k docs)
  - 10 queries to 100 docs
  - 1 queries to 1000 docs - sounds better in this case
- using openapi from langchain https://python.langchain.com/en/latest/modules/models/llms/getting_started.html
  - Gustavo Bartz Guedes used in the few/zero-shot assingment
- test on chatgpt web to test the method
- maybe use hg https://huggingface.co/inference-api to use flan-t5 xl and others from their API
