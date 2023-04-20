# Class 6 Notes 13/04/2023

- **APRESENTAÇÕES ARTIGO DOC2QUERY E DOCTTTTTQUERY**

- **APRESENTAÇÕES NOTEBOOK**
  - PEDRO GABRIEL
    - setar env pytorch memory
    - usar accelarator
      - gerencia memoria, backwards, model, optimizers...
  - THIAGO LAITZ
  - LEANDRO CARISIO
    - bons resultados
      - olhar apresentação
      - tunning k1 e b no trec-covid (modelo pode ficar mais frágil com queries semanticas um pouco mais diferentes - testar pra verificar)
      - usou top-p
      - uso do top-k + top-p ponderá a intercerção deles...caso top-p seja alcançada com menos de k então retorna
        - https://huggingface.co/blog/how-to-generate
        - While in theory, Top-p seems more elegant than Top-K, both methods work well in practice. Top-p can also be used in combination with Top-K, which can avoid very low ranked words while allowing for some dynamic selection.
  - MONIQUE
    - bons resultados
      - olhar apresentação
    - amostragem com diferentes métodos para combinar as queries - juntar predições de diferentes formas de decoding

> Sobre o k1 e o b:
>
>        The interesting part is the parameter  k1
>        , which determines the term frequency saturation characteristic. The higher the value, the slower the saturation.
>
>        If  b
>        is bigger, the effects of the document length compared to the average length are more amplified. We can imagine if we set  b  to 0, the effect of the length ratio would be completely nullified.

- **MELHORIAS**
  - modelos pretreinados precisa de poucas épocas (5-20)
  - se precisar de muitas épocas pode ser pq a LR ta muito baixa
  - adicionado nos slides da aula instruçòes para criação de um mvp pipeline
  - adicionado nos slides da aula resumo do doc2query e trabalhos futuros

- **PRÓXIMAS ATIVIDADES**
  - estudar os notebooks do PEDRO GABRIEL e THIAGO LAITZ

- **TODO**

- **Refs**
  
## article

- representar texto com vetores e compará-los no espaço (dot product or cossine-sim)

- refs
  - relacionado Retrieval-Augmented Generation (RAG) https://www.youtube.com/watch?v=dzChvuZI6D4

## code assignment

- loss constrativa - deixa queries proximas dos docs relevantes (passagens) e longe das docs não relevantes
- dificuldade deverá ser implementar a loss com os hard negatives
- usar um rankeador já pronto (procurar no HF)
