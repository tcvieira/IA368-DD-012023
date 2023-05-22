# Code Notes

Implementar um pipeline multidoc QA: dado uma pergunta do usuário, buscamos em uma grande coleção as passagens mais relevantes e as enviamos para um sistema agregador, que irá gerar uma resposta final.

- Avaliar no dataset do IIRC
- Métrica principal: F1
- **Limitar dataset de teste para 50 exemplos para economizar.**
- Usar o gpt-3.5-turbo como modelo agregador. Usar vicuna-13B como alternativa open-source:
  - https://huggingface.co/helloollel/vicuna-13b
  - https://chat.lmsys.org/

Dicas:
Se inspirar no pipeline do Visconde: https://github.com/neuralmind-ai/visconde

## Slack

>Essa chave "text" é o texto principal no qual o anotador se baseou para compor a pergunta. Assim, é necessário indexar ele também, uma vez que ele deve conter informações relevantes para responder às perguntas.
>
>O campo "context" contem os contextos ground-truth que contém (ou não no caso de perguntas sem resposta) as informações necessárias para responder à pergunta. Você vai ver que em algum casos o campo passage está com o valor main . Isso significa que aquele trecho específico foi retirado do texto principal usado para compor a pergunta.

## Refs

- IIRC dataset - https://aclanthology.org/2020.emnlp-main.86/
- https://slideslive.com/38939237/iirc-a-dataset-of-incomplete-information-reading-comprehension-questions
