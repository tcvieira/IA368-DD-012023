# Code Notes

- **TODO**  [class notes](class-notes.md)
  - assistir novamente parte de explicação da tarefa
  - usar neptune/wandb para guardar as métricas de treino
  - https://huggingface.co/docs/transformers/v4.18.0/en/performance#gradient-checkpointing
  - começar de novo o treino, guardar a LR do final do treino. uma coisa importante também quando reiniciar o treino é tentar evitar de passar dados repetidos (ex: se modelo treinou 10% de época, na hora de recomeçar pular esses 10% de dados)
  - overflowing para evitar truncagem (trunc do hf por default é False). Utilizar os tokens de overflow o hf faz isso
  - gera a palavra-palavra a query para o documento selecionado (inverso do dada a query eu acho o doc). Gera as perguntas que o doc responde.
  - documento expandido é o texto dele + as queries (geralmente só 1 - usando greedy decoding e usar só a primeira - ou várias concatenadas..50-100 tokens) do doc2query que é colocado no índice. Quanto mais gerar, melhor...mas começa com 1 e depois vai subindo até 10
  - não precisa alterar a infra de busca
  - a expansão com doc2query é pré-offline, antes da indexação até que é offline
  - na prática não aumenta a latência do buscador (buscador normal bm25, por exemplo)
  - treinamento do doc2query usando métricas para avaliar modelos de tradução ou sumarização (bleu - sacreBleu e rouge, respectivamente)
  - documentos grandes, usa chunks do doc para gerar as queries e depois concatena tudo para o bm25
  - aprender a usar o t5 para outras tarefas já que ele é seq2seq

  - pegar o t5 seq2seq fazer o finetunning no ms marco tiny
    - input: passagem relevante e target:query
  - conjunto de validação separada
  - pra cada modelo precisará pegar e 
  - avaliar no trec-covid usar somentes os primeiros 200 tokens

  - no code do chatgpt ele n constroi o indice de novo...tem vários erros
  - nos slides colocar a diferencia do t5 (os embeddings de entrada influenciam nos embeddings do decoder), gpt (tokens do futuro **não influenciam** na representacao dos tokens do passado), bert (tokens do futuro **influenciam** na representacao dos tokens do passado) e pq usa essa arquitetura nessa tarefa...e pq?

  - não expandir textos muito pequenos - achar um tamanho para realizar esse passo

## Refs

- https://github.com/castorini/docTTTTTquery
- https://huggingface.co/BeIR/query-gen-msmarco-t5-large-v1
- https://github.com/UKPLab/sentence-transformers/tree/master/examples/unsupervised_learning/query_generation
- Symmetric and asymmetric semantic search - https://github.com/UKPLab/sentence-transformers/tree/master/examples/applications/semantic-search
- A Survey of Large Language Models - https://arxiv.org/pdf/2303.18223.pdf
