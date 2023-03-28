# Assigment Week 4

## Code

Treinar um modelo de linguagem em dados em portugues.

Avaliar o modelo usando a perplexidade, que é simplesmente a exponencial de todas as losses do dataset de validação

Iremos treinar o modelo para prever o próximo token dado os anteriores (também conhecido como Causal Language Modeling). Não confundir com o Masked Language Modeling (MLM), que consiste em prever tokens mascarados em uma dada sequência (ex: BERT's MLM)

**Dicas:**
Usar como ponto de partida o modelo [OPT-125M](https://huggingface.co/facebook/opt-125m), que já foi treinado em 300B de tokens (maioria em Inglês)
Usar este dataset reduzido do mc4 portugues, com ~300M de tokens: gs://unicamp-dl/ia025a_2022s1/aula9/sample-1gb.txt

[![google colab link](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/tcvieira/IA368-DD-012023/blob/main/assingments/04/notebook.ipynb)

[notebook](notebook.ipynb)

## Reading

[Language Models are Unsupervised Multitask Learners] (https://d4mucfpksywv.cloudfront.net/better-language-models/language_models_are_unsupervised_multitask_learners.pdf)

[slides pdf](article-slides.pdf)

[slides markdown](article-notes.md)

[notes](article-notes.md)
