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
    --title-height: 80px;
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

    /* SPLIT */
    section.split {
    overflow: visible;
    display: grid;
    grid-template-columns: 600px 600px;
    grid-template-rows: 50px auto;
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

# [WebGPT](https://arxiv.org/pdf/2112.09332.pdf) and [Visconde](https://arxiv.org/pdf/2212.09656.pdf)

## Thiago Coelho Vieira - thiagotcvieira@gmail.com
---
<!-- paginate: true -->

<!-- # 1. Questions

1. **main concepts**
2. **contributions**
3. **interesting/unexpected results**
4. ~~basic doubts~~
5. ~~advanced topics for discussion~~ -->

# 1.1 main concepts WebGPT

- **imitation learning**
 - submits search queries, follows links, and scrolls up and down web pages
- **human preferences** approach from fine-tuning [GPT-2](https://openai.com/research/fine-tuning-gpt-2) to produce answers more human-like
- **long-form question-answering (LFQA)** : paragraph-length answer is generated in response to an open-ended question
- **factual accuracy** : support answers references (mitigate model "*hallucination*")
- **demonstrations**: examples of humans using the browser to answer questions
- **comparisons**: pairs of model-generated answers to the same question, and asked humans which one they preferred to optimize answers quality (*better, worse or equally good overall*)

---

# 2.1 contributions WebGPT

- leverage existing information retrieval (Bing Web Search API) and synthesis (GPT3 fine tunned) to solve LFQA
- optimize answer quality using human feedback (**comparisons**) 
- provide answers with citation from the articles of the retrieval step as a factual proof
- developed a end-to-end open-ended Q/A system using a text-based web browser [WebGPT Answer Viewer](https://openaipublic.blob.core.windows.net/webgpt-answer-viewer/index.html)

---

# 2.2 WebGPT

- GPT-3 to use a text-based web-browser trained on 6000 **demonstrations** and 21500 **comparisons** and 4 different training methods (BC, RM, RL and best-of-$n$)
- the model is provided with an open-ended question and a summary of the browser state and must issue commands (search, find in page, quote, scroll...)
- trained a reward model to predict human preferences, and optimizing against it using either reinforcement learning (based on reward model) or rejection sampling (reranking)

![bg right:45% 95%](training.png)

---

# 3.1 interesting/unexpected results WebGPT

- retrieve 64 hits (Bing)
- fine tuned *GPT-3* 760M, 13B and 175B
- post-processing dataset, demonstration interface, comparison denoising (appendixes)
- use moslty *ELI5* dataset of open-ended questions scraped from the "Explain Like I'm Five" subreddit
- answers are factually accurate as those written by our human demonstrators
- best model produced answers that were **prefered 56%** of time against the ones written by humans.
- do not work very well in *OOD* questions from *ELI5* dataset
- *TruthfulQA* an adversarially-constructed dataset of short-form questions (scored on *truthfulness* and *informativeness*)
- model answers are **true 75% of the time**, and are **both true and informative 54% of the time**
  
---
# 4. basic doubts WebGPT

- what are the human *demonstrations*? examples of humans using the browser to answer questions
- what passages from the site are picked? simply picked passages with the term on it
- how to cherry-pick the best sources? (Bing, Google, private IR)

---
# 5. advanced topics WebGPT

- bring light to the challenges and risks of allowing general-purpose AI system like this to access and work directly on information from the web.
  - what sources are reliable
- it's something like plugins of the ChatGPT and AgentGPT does nowadays
- answers with citations can obscure the fact that our model still makes basic errors

---

# 1.1 contributions Visconde

- open-domain QA system pipeline (IR Google + Reader/Aggregator GPT-3.5)
- "show that current multi-document QA systems are close to human-level performance *as long as ground truth contexts are provided as input to the reader*".
- show that future work on multi-document QA should focus on improving retrievers, because of its bad perfomance when selecting the context.
- each dataset has different approaches for pre-processing and procedure based on its nature

---

# 1.2 Visconde

1) **question decomposition**: using few-shot with GPT3;
2) **document retrieval**, using BM25 (pyserini index) and monoT5 (top-1k reranker); and
3) **aggregation**, using GPT-3 (reader) with a chain of thought (CoT) to reason over the retrieved records and produce answers.
   1) **CoT** is used for asking the model to explain how the evidence documents can answer the question
   2) **prompt**: list of context documents (e.g., [Document 1]), a question, an evidence paragraph, and the answer

![bg right:50% 95%](visconde-qa-flow.png)

---

# 1.3 Visconde

- The context documents of the **target** example are the top-k documents from the retriever step
- if the question is decomposed, the top-k documents from each subquestion are used
- for the **target** example, an evidence paragraph is not provided and LLM must generate it with the final answer
- prompt
  - static: pre-defined list of examples
  - dynamic: selected in-context examples that are similar to the test example (using *KNN* algorithm to find the k most similar to the test question)

---

# 1.1 interesting/unexpected results Visconde

- current retrievers are the main bottleneck
- readers are already performing at the human level as long as relevant passages are provided (from the retriever)
- the system is also shown to be more effective when the model is induced to give explanations before answering a question (CoT). ie. arithimetic questions
- in some cases the system answers questions marked as unanswerable by the human annotators
- outperforms the baselines in different settings:
  1) using the gold context searched by humans (Gold Ctx);
  2) searching for context in the links the dataset provides (Linked pages); and;
  3) searching for contexts in the entire dataset

<p><small>the model name is a homage to Visconde de Sabugosa</small></p>