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

## Refs

- https://slideslive.com/38939237/iirc-a-dataset-of-incomplete-information-reading-comprehension-questions
