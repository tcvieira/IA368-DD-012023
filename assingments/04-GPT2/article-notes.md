# Notes from GPT-2 - Language Models are Unsupervised Multitask Learners

## Article

https://d4mucfpksywv.cloudfront.net/better-language-models/language_models_are_unsupervised_multitask_learners.pdf

### Description

- GPT-2 is a transformers model pretrained on a very large corpus of English data in a self-supervised fashion. This means it was pretrained on the raw texts only, with no humans labelling them in any way (which is why it can use lots of publicly available data) with an automatic process to generate inputs and labels from those texts. More precisely, it was trained to guess the next word in sentences.
- More precisely, inputs are sequences of continuous text of a certain length and the targets are the same sequence, shifted one token (word or piece of word) to the right. The model uses internally a mask-mechanism to make sure the predictions for the token i only uses the inputs from 1 to i but not the future tokens.
- This way, the model learns an inner representation of the English language that can then be used to extract features useful for downstream tasks. The model is best at what it was pretrained for however, which is generating texts from a prompt.
- GPT-2 is a direct scale-up of GPT, with more than 10X the parameters and trained on more than 10X the amount of data.
- When a large language model is trained on a sufficiently large and diverse dataset it is able to perform well across many domains and datasets. GPT-2 zero-shots to state of the art performance on 7 out of 8 tested language modeling datasets. The diversity of tasks the model is able to perform in a zero-shot setting suggests that high-capacity models trained to maximize the likelihood of a sufficiently varied text corpus begin to learn how to perform a surprising amount of tasks without the need for explicit supervision.
- https://jalammar.github.io/illustrated-gpt2/
- GPT-2 consists of solely stacked decoder blocks from the transformer architecture. In the standard transformer architecture, the decoder is fed a word embedding concatenated with a context vector, both generated by the encoder. In GPT-2 the context vector is zero-initialized for the first word embedding (presumably?).
- Furthermore, in the standard transformer architecture self-attention is applied to the entire surrounding context, e.g. all of the other words in the sentence. In GPT-2 masked self-attention is used instead: the decoder is only allowed (via obfuscation masking of the remaining word positions) to glean information from the prior words in the sentence (plus the word itself).
- Besides that GPT-2 is a close copy of the basic transformer architecture.
- The word vectors used for the first layer of GPT-2 are not simple one-hot tokenizations but byte pair encodings (BPE). The byte pair encoding scheme compresses an (arbitrarily large?) tokenized word list into a set volcabulary size by recursively keying the most common word components to unique values (e.g. 'ab'=010010, 'sm'=100101, 'qu'=111100, etecetera).
- GPT-2 is trained in the standard transformer way, with a batch size of 512, a well-defined sentence length, and a volcabulary size of 50,000. At evaluation time, the model switches to expecting input one word at a time. This is done by temporarily saving the necessary past context vectors as object properties.
- GPT-2 is trained on the standard task: given a sequence of prior words, predict the next word.
- How to get meaning from text with language model BERT | AI Explained - https://www.youtube.com/watch?v=-9vVhYEXeyQ

**Transformers**

https://github.com/yandexdataschool/nlp_course/blob/2022/week08_llm/lecture_llm.pdf

### Disclaimer

> Because large-scale language models like GPT-2 do not distinguish fact from fiction, we don’t support use-cases that require the generated text to be true.
>
> Additionally, language models like GPT-2 reflect the biases inherent to the systems they were trained on, so we do not recommend that they be deployed into systems that interact with humans > unless the deployers first carry out a study of biases relevant to the intended use-case. We found no statistically significant difference in gender, race, and religious bias probes between 774M and 1.5B, implying all versions of GPT-2 should be approached with similar levels of caution around use cases that are sensitive to biases around human attributes.

- pretty biased

### Dataset

- The OpenAI team wanted to train this model on a corpus as large as possible. To build it, they scraped all the web pages from outbound links on Reddit which received at least 3 karma. Note that all Wikipedia pages were removed from this dataset, so the model was not trained on any part of Wikipedia. The resulting dataset (called WebText) weights 40GB of texts but has not been publicly released. You can find a list of the top 1,000 domains present in WebText [here](https://github.com/openai/gpt-2/blob/master/domains.txt).

### Training

**Preprocessing**

The texts are tokenized using a byte-level version of Byte Pair Encoding (BPE) (for unicode characters) and a vocabulary size of 50,257. The inputs are sequences of 1024 consecutive tokens.

The larger model was trained on 256 cloud TPU v3 cores. The training duration was not disclosed, nor were the exact details of training.

**Evaluation results**

The model achieves the following results without any fine-tuning (zero-shot):

## ChatGPT

**QUESTION**

> ANSWER