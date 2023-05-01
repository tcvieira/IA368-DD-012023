# Notes [InPars](https://arxiv.org/pdf/2202.05144.pdf)

## InPars

- presented a method to generate synthetic training data for IR tasks using large LMs in a few-shot manner.
- demonstrated that generate synthetic training data with LM can improve neural IR systems
- Future works
  - Finetuning dense retrievers on the generated synthetic data
  - Using “bad questions” as negative training examples
  - Scale up our synthetic datasets to millions of examples (ideia: maybe use something like recaptcha or crowdsourcing + gamefication)
  - More sophisticated methods to select (question, relevant document) pairs (WHICH ONES?)

- interesting
  - approach to eval if gtp-3 was trained on supervised IR data
    - experiment: "measuring the number of questions produced by GPT-3 that match those in the MS MARCO dataset"
    - these low percentages are evidence that the models were not finetuned on MS MARCO, or at least, they did not memorize it
  - gpt-3 model size increase
    - As the GPT3 model size used to generate synthetic questions were increased, the IR metric keeps increasing, although very slowly.
    - bigger models brings more complex and spefic questios which helps the reranker

## Refs
