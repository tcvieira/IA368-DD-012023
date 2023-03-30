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

# Facebook/OPT-125M-Portuguese LLM

## [![google colab link](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/tcvieira/IA368-DD-012023/blob/main/assingments/04/notebook.ipynb)

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

# 2. Conceitos

**Perplexity** is closely related to the cross entropy that is directly minimized during training (intrinsic). Another metrics are **BLEU** and **ROUGE** that are more related to, e.g., classification accuracy (extrinsic). **BLEU** is a precision-like score to evaluate the quality of a translated text. **ROUGE** is a recall-like score to evaluate summarized text.

A high perplexity indicates that a language model is worse at predicting the next word in a sequence, implying greater uncertainty in its predictions. Therefore a lower perplexity indicates better performance in predicting the next word in a sequence, reflecting a more accurate understanding of language patterns and context.

- Ou seja, se o seu modelo de linguagem tem perplexidade de N, significa que ele é igual a uma classificador aleatório de N classes

---

# 2.1 Conceitos

- por que usar PPL ao invés de entropia cruzada? https://towardsdatascience.com/perplexity-intuition-and-derivation-105dd481c8f3 ver no chatgpt tbm
- Diferença entre logits e probabilidades
  - logits são valores numéricos não normalizados brutos produzidos pelo modelo na saída da sua última camada
  - probabilidades são valores normalizados dos logits que indicam a probabilidade relativa de cada palavra na sequência ou outro tipo de tarefa, caracterizando uma distribuição de probabilidade
  - Ambas as medidas podem ser usadas para avaliar a qualidade de um modelo de linguagem e para gerar previsões de palavras futuras em uma sequência.

---

# 3. Problemas e soluções no desenvolvimento

- primeira vez treinando/finetuning um LLM
- `Dataset` do HF é muito bom. Customização deles pra fazer preprocessing e outras coisas
- notebooks/apresentações interessantes
  - `Mirelle` e outros colegas
    - dataset de teste para overfitting
  - `Marcos Vieira`
    - truques de código
    - tempo gasto artigo + notebook (meu caso foi por parecido também, com ~20h de estudo na semana)
  - `Eduardo Olivieira`
    - treino com length de 2048
    - batchs em disco

---

# 3.1 Problemas e soluções no desenvolvimento

- calcular perplexidade inicial do dataset = número de palavras no vocabulário
- HF facilita demais o uso de transformers, mas é importante fica atendo a outros aspectos do modelo e tokenizador
- usei T4 16Gb no Colab Pro
  - treino demorado
  - +1 epoch = +2h-3h de treino
- no final consegui pegar um A100 pra treinar. ~~40 créditos que valem do que dinheiro~~ 💸💸💸💸
- teste de overfit com dataset pegando os 100 primeiros textos
- salvar `tokenized dataset` no disco

---
# 4. Resultados

split train/validation 80/20 (200.000, 50.000)

<center>

| seq length | epochs | batch size |    gpu    | time/epoch | val_ppl |
|:----------:|:------:|:----------:|:---------:|:----------:|:-------:|
|     256    |    1   |      4     |  T4 16GB  |     ~2h    |  31.67  |
|     512    |    1   |      4     |  T4 16GB  |     OOM💥   |    -    |
|     512    |    1   |      8     | A100 40GB |    45min   |  10.96  |
|     512    |   1+1  |      8     | A100 40GB | colab fail🤔 |    -    |
|     512    |    2   |      8     | A100 40GB |     ~2h    | **9.67** 🏆|
|    1024    |    1   |     16     | A100 40GB |     OOM💥  |    -    |

| epoch | train loss | val loss |
|:-----:|:----------:|:--------:|
|   1   |  2.571000  | 2.339543 |
|   2   |  2.327500  | 2.269327 |

</center>

--- 

# 4.1 Resultados

[transformer generation config](https://huggingface.co/docs/transformers/main_classes/text_generation#transformers.GenerationConfig)

`max_length=50, do_sample=True`

<span style="font-size: 18px;">Era uma vez na fazenda </span> <span style="font-size: 20px; color: RGB(93,11,113);">irmã, e seu vizinho e o vizinho que comanda o salão de restaurantes com a cachoeira e a borboleta. Na frent</span>
<span style="font-size: 18px;">Era uma vez na fazenda </span> <span style="font-size: 20px; color: RGB(93,11,113);">irmão o destacando e os dias de hoje fomei meus olhos de manho que a chuva deu conta de que meu am</span>
<span style="font-size: 18px;">Era uma vez na fazenda </span> <span style="font-size: 20px; color: RGB(93,11,113);">irmão de Paulo que, no início dos anos 90, tanto na família do empresário, como na família dos comerci</span>
<span style="font-size: 18px;">Era uma vez na fazenda </span> <span style="font-size: 20px; color: RGB(93,11,113);">irmão que desafiu a vida para poder se dedicar ao povo que ele tinha. Ele, por sua vez, foi um grande</span>
<span style="font-size: 18px;">Era uma vez na fazenda </span> <span style="font-size: 20px; color: RGB(93,11,113);">ilesa do sossego Zey, um pediatra que fez a reativação dos dentes fazendo parte da rotina com as crian</span>
<span style="font-size: 18px;">Era uma vez na fazenda </span> <span style="font-size: 20px; color: RGB(93,11,113);">irmã do casal que pessoas de coração amada e muito amadora deu àquelas que gostavam de se amare</span>
<span style="font-size: 18px;">Era uma vez na fazenda </span> <span style="font-size: 20px; color: RGB(93,11,113);">ilegal a mãe de um filho que estava comercialando seus produtos. A mãe da menina sentiu-se aos dentes</span>

---

# 4.2 Resultados

`max_length=50, do_sample=True, num_beams=5, early_stopping=True, no_repeat_ngram_size=2`

<span style="font-size: 18px;">Era uma vez na fazenda </span> <span style="font-size: 20px; color: RGB(93,11,113);">Ângela, na cidade de Santo Antônio de Jesus, no Rio de Janeiro, que se encontrava com a família de um homem</span>
<span style="font-size: 18px;">Era uma vez na fazenda </span> <span style="font-size: 20px; color: RGB(93,11,113);">irmã de um grupo de amigos que estavam na cidade de Florianópolis, nos Estados Unidos. Eles se encontrav</span>
<span style="font-size: 18px;">Era uma vez na fazenda </span> <span style="font-size: 20px; color: RGB(93,11,113);">irmã de um grupo de pessoas que trabalhavam como lanchonete. Eles tinham um grande público, que</span>
<span style="font-size: 18px;">Era uma vez na fazenda </span> <span style="font-size: 20px; color: RGB(93,11,113);">Ângela, no bairro São João, que eu tinha oportunidade de conhecer um pouco mais sobre a histó</span>
<span style="font-size: 18px;">Era uma vez na fazenda </span> <span style="font-size: 20px; color: RGB(93,11,113);">irmã de um jovem de 19 anos que acabou de morar em um apartamento na cidade de São José dos Campos, no interior de</span>
<span style="font-size: 18px;">Era uma vez na fazenda </span> <span style="font-size: 20px; color: RGB(93,11,113);">irmã de um jovem de 16 anos que, após a morte de sua mãe, decidiu seguir para a cidade de</span>
<span style="font-size: 18px;">Era uma vez na fazenda </span> <span style="font-size: 20px; color: RGB(93,11,113);">irmã de um amigo que eu tinha ouvido falar sobre o assunto. Não sabia o que fazer, mas acho que quando</span>
<span style="font-size: 18px;">Era uma vez na fazenda </span> <span style="font-size: 20px; color: RGB(93,11,113);">Ângela, no bairro de São Bento, que se encontrava com um grupo de moradores que estavam próximos de</span>


---

# 5. Questões/Dúvidas para discussão

- concatenação de sentenças para evitar padding e melhorar uso da gpu? discussão do slack
- não precisaria ajustar o vocab_size da config do modelo para o novo dataset tokenizado?
- salvar processamento/tokenizer e outras coisas em disco para depois habilitar gpu e treinar - salvei o dataset tokenizado
- como calcular a perplexidade sem treino?
  - vi no notebook do `Thiago Laitz` que ele usa a loss da primeira iteração do finetunning
- como faria pra ajustar a função de custo pra usar ppl?
