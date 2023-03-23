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
---

# Few-Shot with OpenAPI and SetFit on IMDB

---
<!-- paginate: true -->

# 1. Questões

1. **Explicação de conceitos importantes do exercício feito**
2. ~~Técnicas para garantir que a implementação está correta~~
3. ~~Truques de código que funcionaram~~
4. **Problemas e soluções no desenvolvimento**
5. **Resultados interessantes/inesperados**
6. **Uma dúvida "básica" que você ou os colegas possam ter**
7. ~~Um tópico "avançado" para discutirmos~~

---

# 2. Explicação de conceitos importantes do artigo

[**SetFit**](https://github.com/huggingface/setfit) is an efficient and prompt-free framework for few-shot fine-tuning of Sentence Transformers. Based on the Customer Reviews sentiment datasets benchmark, SetFit is competitive and achieve comparable performance with only 8 labeled examples per class compared to fine-tuning RoBERTa Large with datasets of 3k labeled examples.

[**Sentence Transformers**](https://sbert.net/) SentenceTransformers is a Python framework for state-of-the-art sentence, text and image embeddings - **Based on embeddings, no prompts are required and supports multilingual text classification**

**Few-Shot Learning** is the practice of training a machine learning model with a small amount of data.

---

# 2.1 SetFit

![center](setfit.png)
