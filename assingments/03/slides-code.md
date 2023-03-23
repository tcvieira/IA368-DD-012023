---
marp: true
theme: gaia
_class: lead
backgroundColor: #fff
backgroundImage: url('https://marp.app/assets/hero-background.svg')
style: |
    section {
    font-size: 1.5rem;
    }

    img[alt~="center"] {
        display: block;
        margin: 0 auto;
    }

    section{
        justify-content: flex-start;
    }

    section.title {
    --title-height: 130px;
    --subtitle-height: 70px;

    overflow: visible;
    display: grid;
    grid-template-columns: 1fr;
    grid-template-rows: 1fr var(--title-height) var(--subtitle-height) 1fr;
    grid-template-areas: "." "title" "subtitle" ".";
    }

    section.title h1,
    section.title h2 {
    margin: 0;
    padding: 0;
    text-align: center;
    height: var(--area-height);
    line-height: var(--area-height);
    font-size: calc(var(--area-height) * 0.28);

    border: 0px dashed gray; /* debug */
    }

    section.title h1 {
    grid-area: title;
    --area-height: var(--title-height);
    }

    section.title h2 {
    grid-area: subtitle;
    --area-height: var(--subtitle-height);
    }

    section.split {
    overflow: visible;
    display: grid;
    grid-template-columns: 600px 600px;
    grid-template-rows: 100px auto;
    grid-template-areas: 
        "slideheading slideheading"
        "leftpanel rightpanel";
    }
    /* debug */
    section.split h3, 
    section.split .ldiv, 
    section.split .rdiv { border: 0pt dashed dimgray; }
    section.split h3 {
        grid-area: slideheading;
        font-size: 50px;
    }
    section.split .ldiv { grid-area: leftpanel; }
    section.split .rdiv { grid-area: rightpanel; }
---

<!-- _class: title -->

# Zero-Shot and Few-Shot with OpenAPI and SetFit on IMDB
## [![google colab link](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/tcvieira/IA368-DD-012023/blob/main/assingments/03/notebook.ipynb)

---
<!-- paginate: true -->

# 1. Questões

1. **Explicação de conceitos importantes do exercício feito**
2. ~~Técnicas para garantir que a implementação está correta~~
3. ~~Truques de código que funcionaram~~
4. **Problemas e soluções no desenvolvimento**
5. ~~Resultados interessantes/inesperados~~
6. **Uma dúvida "básica" que você ou os colegas possam ter**
7. ~~Um tópico "avançado" para discutirmos~~

---

# 2. Explicação de conceitos importantes do artigo

[**SetFit**](https://github.com/huggingface/setfit) is an efficient and prompt-free framework for few-shot fine-tuning of Sentence Transformers. Based on the Customer Reviews sentiment datasets benchmark, SetFit is competitive and achieve comparable performance with only 8 labeled examples per class compared to fine-tuning RoBERTa Large with datasets of 3k labeled examples.

[**Sentence Transformers**](https://sbert.net/) SentenceTransformers is a Python framework for state-of-the-art sentence, text and image embeddings - **Based on embeddings, no prompts are required and supports multilingual text classification**

**Constrative Learning** puts similar embeddings together and try to spread apart the differences using loss functions like cosine similarity and others.

**Few-Shot Learning** is the practice of training a machine learning model with a small amount of data.

---

# 2.1 SetFit

![center](setfit.png)

---

# 3. Problemas e soluções no desenvolvimento

- first time using hf datasets
- discovered about langchain
- tutorial setFit https://huggingface.co/blog/setfit
- how to use setFit for zero-shot (notebook do Gustavo Bartz Guedes)

---
# 4. Resultados
<!-- _class: split -->
<div class=ldiv>

## SetFit
zero-shot
![w:500 h:180](setfit-zero-shot.png)

few-shot
![w:500 h:180](setfit-few-shot.png)

</div>
<div class=rdiv>

## GPT-3.5 OpenAPI

zero-shot
![w:500 h:180]()

few-shot
![w:500 h:180]()

</div>

---

# 4. Uma dúvida "básica" que você ou os colegas possam ter

- zero-shot do SetFit não parece zero-shot pela definição do artigo do GPT-3 (mas é usado os embeddings do corpus como se fosse o LM...faz sentido)
- few-shot no setfit overfit pois só tem 8 amostras para cada label (é possivel fazer otimizar hyperparametros para dataset maiores)
- como o contexto é guardado em um um diálogo/conversa com chatgpt? ele guarda toda conversa naquele estilo da api que manda o diálogo, papéis (role) e conteúdo todo?
