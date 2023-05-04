# Code Notes

Instruções Exercício - InPars

**Objetivo**: gerar dataset para treino de modelos de buscas usando a técnica do InPars e avaliar um modelo reranqueador treinado neste dataset no TREC-COVID:

**Entrada**: 3-5 exemplos few-shot + documento amostrado da coleção do TREC-COVID
**Saída**: query que seja relevante para o documento amostrado

É opcional fazer a etapa de filtragem usando as queries de maior prob descrita no Artigo.

Como modelo gerador, use um dos seguintes modelos:

- ChatGPT-3.5-turbo: ~1 USD para cada 1k exemplos
- FLAN-T5 (base, large ou XL), LLAMA-(7,13B), Alpaca-(7/13B), que são possiveis de rodar no Colab Pro.
- Também tem a inference-api da HF: https://huggingface.co/inference-api.

Com exceção do LLAMA, é possivel usar zero-shot ao inves de few-shot.

Dado 1k-10k pares <query sintética; documento>, treinar um modelo reranqueador miniLM igual ao da aula 2/3.

Exemplos negativos (i.e., <query sintética; doc não relevant) vem do BM25: dado a query sintetica, retornar top 1000 com o BM25, e amostrar aleatoriamente alguns documentos como negativo

Começar treino do miniLM já treinado no MS MARCO

Avaliar no TREC-COVID e comparar com o reranqueador apenas treinado no MSMARCO

Nota: Também usar o dataset dos colegas para obter diversidade de exemplos: Assim que tiver gerado o dataset sintético, favor colocar na planilha, assim outras pessoas podem usá-lo.

- Para aumentar a aleatoriedade, seed usada deve o seu número na planilha.

> Colocar dataset no formato jsonlines:
> {"query": query, "positive_doc_id": doc_id, "negative_doc_ids": [opcional]}\n 

## Refs

- Júlia Tessler - getpass() https://docs.google.com/presentation/d/1UgHVxaZ2rsSSM62mRvZdCfMfpKT11Ts4RJBOgWB2XKI/edit#slide=id.g23e0cb8d425_0_11
- chatgpt
  - > you are a prompt engineer. Give some good prompts that instruct chatgpt to generate synthetic queries for documents
    - **ChatGPT** Sure, here are some prompts that can be used to instruct ChatGPT to generate synthetic queries for documents:
      - "What are some questions someone might have after reading this document?"
      - "Can you generate queries that would help a user find information related to this document's content?"
      - "What are some alternative ways to ask for information covered in this document?"
      - "Can you generate queries that would help a user better understand a particular concept discussed in this document?"
      - "What are some common search queries that someone might use to find this document?"
      - "Can you suggest queries that would help a user identify the main points covered in this document?"
      - "What are some potential queries that would help a user evaluate the credibility of the information in this document?"
      - "Can you generate queries that would help a user connect this document to other relevant resources on this topic?"
      - "What are some queries that would help a user find examples or case studies related to the topics discussed in this document?"
      - "What are some queries that would help a user find additional information on a particular aspect of this document's content?"
