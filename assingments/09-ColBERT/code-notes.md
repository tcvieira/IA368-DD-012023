- https://medium.com/@zz1409/colbert-a-late-interaction-model-for-semantic-search-da00f052d30e
- https://github.com/terrier-org/ecir2021tutorial

- ColBERTv1 training style

https://github.com/stanford-futuredata/ColBERT

```python
from colbert.infra import Run, RunConfig, ColBERTConfig
from colbert import Trainer

if __name__=='__main__':
    with Run().context(RunConfig(nranks=4, experiment="msmarco")):

        config = ColBERTConfig(
            bsize=32,
            root="/path/to/experiments",
        )
        trainer = Trainer(
            triples="/path/to/MSMARCO/triples.train.small.tsv",
            queries="/path/to/MSMARCO/queries.train.small.tsv",
            collection="/path/to/MSMARCO/collection.tsv",
            config=config,
        )

        checkpoint_path = trainer.train()

        print(f"Saved checkpoint to {checkpoint_path}...")
```

para o ColBERTv2 teria que ajustar o ColBERTConfig, como? passando mais configs no RunSettings ou no Trainer?

https://github.com/stanford-futuredata/ColBERT/blob/main/colbert/infra/config/config.py
- ColBERTConfig

https://github.com/stanford-futuredata/ColBERT/blob/main/colbert/infra/config/base_config.py
- herda de CoreConfig

https://github.com/stanford-futuredata/ColBERT/blob/main/colbert/infra/config/settings.py
- RunSettings
  - QuerySettings: interaction line 118 `colbert`
  - TrainingSettings: config model line 154
  - IndexingSettings: kmeans line 162
  - SearchSettings: centroid score line 173

https://github.com/stanford-futuredata/ColBERT/blob/main/colbert/trainer.py
- train ignore run config model and use `bert-base-uncased`, talvez tenha q alterar aqui
- chama o Launcher

https://github.com/stanford-futuredata/ColBERT/blob/main/colbert/modeling/hf_colbert.py
- class_factory seleciona modelo
- adicionar modelo que quero usar no base_class_mapping e no model_object_mapping e ver se aparece no teste

https://github.com/stanford-futuredata/ColBERT/blob/main/colbert/modeling/base_colbert.py
- seleciona o HF_ColBERT linha 27 baseado no nome do modelo vindo do `colbert_config.model_name`

https://github.com/stanford-futuredata/ColBERT/blob/main/colbert/modeling/colbert.py
- usado para o treino tem o `forward`, `loss` e `score`

https://github.com/stanford-futuredata/ColBERT/blob/main/colbert/training/training.py
- fallback para o `bert-base-uncased` quando config não tem checkpoint
- usar config.help()

https://github.com/stanford-futuredata/ColBERT/issues/94
- Thanks for your interest! Yes, we'll release instructions for ColBERTv2 soon. (FWIW, most of the code is already there: you just need to provide distillation scores in the triples jsonl files.)

https://github.com/stanford-futuredata/ColBERT/issues/170
https://github.com/stanford-futuredata/ColBERT/issues/150
https://github.com/stanford-futuredata/ColBERT/issues/139
