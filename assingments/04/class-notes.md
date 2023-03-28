# Class notes

- próxima leitura - GPT-2 (causal language modeling - prever próximo token)
  - menos params e zero-shot mais rudimentar
  - atualmente parece que decoder escala mais
  - MLM 20B (T5 que é encoder) e next token pred 150B (decoder-GPT) params
  - parece ser mais eficiente a arquitetura decoder prevendo o próximo token
- usar zero-shot pra lógica/resolução/tableaux (lhama, gpt-3, alpaca)
- instruction tunning pra entender e ter distinção da task e exemplos (possivelmente) - aquele campo de descrição/task. feito como finetuning após o pretreino seguindo um template instrução + exemplo e retorna o target (completion)
- passando o prompt com descrição funciona como um filtro e não como learning porque os pesos do modelo não são ajustados

## GPT-2 article

- curadoria dos dados importante
- avaliação feita, capacidade de few-shot
