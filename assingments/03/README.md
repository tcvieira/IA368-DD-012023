# Assigment Week 3

## Code

O aluno irá escolher uma tarefa para resolver de maneira zero ou few-shot. Sugestões:

- Classificação de textos (ex: análise de sentimos (IMDB))
- Predizer se uma passagem/parágrafo é relevante para uma pergunta/query
- Se uma resposta predita por um sistema de QA ou sumarizador é semanticamente igual à resposta ground-truth

É importante ter uma função de avaliação da qualidade das respostas do modelo few-shot. Por exemplo, acurácia.

É possível criar um pequeno dataset de teste manualmente (ex: com 10 à 100 exemplos)

- Usar a API do LLAMA fornecida por nós (licença exclusiva para pesquisa). Colab demo da API do LLAMA (obrigado, Thales Rogério)
- Opcionalmente, usar a API do code-davinci-002, que é de graça e trás resultados muito bons.
CUIDADO: NÃO USAR O TEXT-DAVINCI-002/003, que é pago

- Opcionalmente, usar a API do ChatGPT (gpt-3.5-turbo) que é barata: ~1 centavo de real por 1000 tokens (uma página)
- Opcionalmente, usar o Alpaca: https://alpaca-ai.ngrok.io/

Dicas:

- Teste com zero-shot E few-shot.
- No few-shot, faça testes com e sem instruções no cabeçalho (explicação da tarefa, ex: "Traduza de Ingles para Portugues"). Pode ser que sem a instrução o modelo até funcione melhor.
- Siga sempre um padrão ao criar os exemplos few-shot. Aqui tem uma pagina com dicas para prompt engineering: https://help.openai.com/en/articles/6654000-best-practices-for-prompt-engineering-with-openai-api

[![google colab link](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/tcvieira/IA368-DD-012023/blob/main/assingments/03/notebook.ipynb)

[notebook](notebook.ipynb)

## Reading

[Language Models are Few-Shot Learners] (https://arxiv.org/pdf/2005.14165.pdf)

[slides pdf](article-slides.pdf)

[slides markdown](article-slides.md)

[notes](article-notes.md)
