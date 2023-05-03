# Code Notes

Instruções Exercício - InPars

Objetivo: gerar dataset para treino de modelos de buscas usando a técnica do InPars e avaliar um modelo reranqueador treinado neste dataset no TREC-COVID:

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

**Dicas:**

## Refs
