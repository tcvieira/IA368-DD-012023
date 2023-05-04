---
marp: true
theme: gaia
_class: lead
math: mathjax
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

# InPars

## [![google colab link](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/tcvieira/IA368-DD-012023/blob/main/assingments/08-InPars/notebook.ipynb)

---
<!-- paginate: true -->

# 1. Tricks

- used getpass() (didn't know)
- used chatgpt do generate some prompts that would generate good queries
  - Sure, here are some prompts that can be used to instruct ChatGPT to generate synthetic queries for documents:
    1. "Can you generate queries that would help a user find information related to this document's content?"
    2. "What are some alternative ways to ask for information covered in this document?"
    3. "Can you generate queries that would help a user better understand a particular concept discussed in this document?"
    4. "What are some common search queries that someone might use to find this document?"
    5. "Can you suggest queries that would help a user identify the main points covered in this document?"
    6. "Can you generate queries that would help a user connect this document to other relevant resources on this topic?"

---

# 3. Problems and workarounds

- chatgpt was unable to generate good code snippets for langchain since it doesn't know about it

---

# 4. Prompt

**prompt:** `Generate a short and objective query in the way a human user would in search engines (based on trec-covid dataset) that would help him find more information about the main topic on the following document:`

**title:** Automatic Detection and Quantification of Tree-in-Bud (TIB) Opacities from CT Scans

**text:** This study presents a novel computer-assisted detection (CAD) system for automatically detecting and precisely quantifying abnormal nodular branching opacities in chest computed tomography (CT), termed tree-in-bud (TIB) opacities by radiology literature. ...

**query from gpt-3.5-turbo:** `What is the Automatic Detection and Quantification of Tree-in-Bud (TIB) Opacities from CT Scans and how does the developed CAD system work?`

<small>**ps:** tried changing the prompt so it would generate queries more similar to the trec-covid dataset by adding "(based on trec-covid dataset)", generate longer queries in general.</small>
