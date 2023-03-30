# Class Notes 30/03/2023

- **APRESENTAÇÕES ARTIGO GPT-2**
  - qual seria a intuição do fato de ser multitask (virou context learning) é uma característica da arquitutra do modelo, da task, dos dados, da quantidade no contexto do gpt2. Essa característica aparece em outros conjunto de dados, arquiteturas...GPT não tinha isso muito, GPT começou a parecer e GPT-3
    - a tarefa de prever a próxima palavra é muito poderosa e foi ela junto com os dados e capacidade de processamento permitiram explorá-la
    - ficou tão bom em prever a próxima palavra com o contexto dado o modelo consegue fazer o in-context-learning como um "filtro" para a próxima previsão.
    - o modo de treino de LLM não tem loss, não tem target ele preve a próxima palavra (auto supervisionado)
    - perplexidade é métrica pra ajustar os pesos e não métrica para avaliar o treinamento
  - antes tinha muitas palavras no vocab e raras. usar um embeddings de caracteres, mas a seq fica maior. BPE é subword o vocab fica menor e o input também

- `usar uma base fechada para validar o modelo está aprendendo (reduzindo a perplexidade, bits per word)`
- `estudos em prever o quanto o modelo vai melhorar com treinamento antes de treinar (ROI)`

- **APRESENTAÇÕES NOTEBOOK**
  - `geralmente treinamos por steps (10000) e aí valida`
  - `geralmente é feito somente 1 epoch`
  - `usar validação pequena < 5%`
  - `voca size com múltiplos de 8, melhora a performance`
  - `concatenar todas as strings e vai picotando no max_length_size mesmo que misture assuntos...parece ser melhor pq os batchs não tem pad. Os pads são ignorados no cálculo da loss, mas ainda passam por processamento gpu/tpu. Ou não concatena, mas descarta a última parte do texto que não completa o max_length_size`
  - `melhor usar fp16 ao invés de fp32 em gpu mais novas nos treinamentos`
  - `pra inferência posso usar até fp menores`
  - `batch muito pequeno faz o treino ficar instável (sair de 128 pra 32, ok...mas as vezes é preciso 1)`
  - `gradient accumulation é como treinar com batch maiores, ele atualiza os pesos e zera eles em steps específicos - https://huggingface.co/docs/transformers/v4.18.0/en/performance#gradient-checkpointing`
  - `usar NaN ao invés de 0 pra economizar memória (pytorch fará isso por default)`
  - `top_p ou top_k parece melhores. O do_sample é muito aleatório`
  - `em caso de few-shot de classificaçào não faz sentido usar o top_p, o greedy decode (probabilidade máxima) é mais indicado. Em predição de classes hierarquicas no few-shot e mostrar a superior e depois menores talvez seja melhor o beam search tbm ao invés de top_p`
  - `treino com sequências maiores parece melhorar mesmo`
  - `no resultado da Monique ficou mostrado que o aumento do block_size e mantendo o numero de dados (256 * 16, 512 * 8, 1024 * 4 - o sinal de treino den4000 tokens é o mesmo) melhorou a ppl`
  - `https://huggingface.co/docs/accelerate/v0.18.0/en/usage_guides/memory#findexecutablebatchsize`

- **MELHORIAS**
  - usar neptune/wandb para guardar as métricas de treino
  - https://huggingface.co/docs/transformers/v4.18.0/en/performance#gradient-checkpointing
  - começar de novo o treino, guardar a LR do final do treino. uma coisa importante também quando reiniciar o treino é tentar evitar de passar dados repetidos (ex: se modelo treinou 10% de época, na hora de recomeçar pular esses 10% de dados)
  - overflowing para evitar truncagem (trunc do hf por default é False). Utilizar os tokens de overflow o hf faz isso

- **PRÓXIMAS ATIVIDADES**
  - doc2query pode ser incorporado em infraestrutura existente
    - enriquece a query
  - T5 (encoder-decoder like) é melhor pra finetunning que modelos gpt (decoder like)

- **TODO**
  - assistir novamente parte de explicação da tarefa

## article

- Document Expansion by Query Prediction. (https://arxiv.org/pdf/1904.08375.pdf)
  - alucina gerando queries q n tem nada a ver
  - usam ranking pra saber quais queries sintéticas vão para o índice
  - doc2query com reranqueador para filtrar queries: https://arxiv.org/pdf/2301.03266.pdf
  - recomendado para docs não muito grandes pq a indexação é lenta

- From doc2query to docTTTTTquery (https://www.researchgate.net/profile/Rodrigo-Nogueira-19/publication/360890853_From_doc2query_to_docTTTTTquery/links/6290b0e98d19206823dfcc55/From-doc2query-to-docTTTTTquery.pdf)
    - ficou melhor só com as queries do que somente com o texto. Melhor resultado com o doc + queries

## code assignment

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
