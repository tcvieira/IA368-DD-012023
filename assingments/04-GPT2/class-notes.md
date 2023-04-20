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

## Code Assingment

https://github.com/huggingface/transformers/blob/main/examples/pytorch/language-modeling/run_clm.py

>Aproveito e mostro aqui uma receita para estimar a velocidade de modelos decoder-only, como o GPT, OPT e LLAMA. 
>
>Normalmente medimos a velocidade em tokens/sec, pois outras medidas como exemplos/sec ou batch/sec são mais complicadas pois o comprimento dos exemplos e tamanho do batch pode mudar em cada experimento.
>
>Os cálculos a seguir foram extraidos do artigo do PALM.
>
>Suponha um treinamento de um modelo com N parametros e um hardware com X FLOPs.
>
>Por exemplo, em 16-bit, uma A100 tem 312 TFLOps teoricos = 312e12
>Um modelo de N parametros precisa de 6N flops/token (a explicação para o 6 está no artigo do PALM)
>Ou seja, para o OPT-125M, precisamos de 6 * 125e6 = 7.5e8 FLOPs/token
>
>Assim, para treinar o OPT-125M em uma A100, é esperado que cheguemos à tokens/sec = flops hardware / flops por token = 312e12 / 7.5e8 = 416000 tokens/sec
>
>Na prática, conseguimos uns 40% de eficiencia, ou seja, é esperado termos 166400 tokens/sec durante o treinamento.
>
>Como o dataset tem um 1GB, e cada token em portugues tem aproximadamente 3 caracteres, teremos 330M tokens para treinamento.
>
>Assim, 330M tokens / 166400 tokens/sec = 33 minutos para dar uma epoca nesse dataset.
>
> https://twitter.com/stephenroller/status/1579993017234382849
