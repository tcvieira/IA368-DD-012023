# Notes from Language Models are Few-Shot Learners

## GPT-3 - Language Models are Few-Shot Learners

- by the time was the lagerst LLM ever created 175B params (size does matter)
- demonstrated that LLM can be use to NLP tasks that it never seen
- BERT is not a LLM, it's just the encoder half of the entire encoder-decoder transformer architecture
- consistent definition of zero-shot, one-shot and few-shot learning, i.e. the number of examples provided at inference time (in the prompt), without any inference-time weight updates.
- GPT3 does not include any bidirectional architecture
- GPT-3 learn tasks in-context (zero/few shot - description + examples + prompt)
- authors found a bug in removing overlaps between train/test data. But the cost of retraining was prohibitive and they didn't retrain the whole thing because of that!
- The same model and architecture as GPT-2 is used, with the exception that alternating dense and locally banded sparse attention patterns are used in the layers of the Transformer, similar to the Sparse Transformer.
- 8 different sizes of model are trained, ranging over three orders of magnitude from 125 million (125M) parameters to 175 billion (175B) parameters, with the last being the model called GPT-3.
- All models use a context window of nctx=2048 tokens.

- BERT Document Classification Tutorial with Code https://www.youtube.com/watch?v=_eSGWNqKeeY

## ChatGPT

**how the fact that bert is the encoder part of the transformer architecture and gpt is the decoder correlate to both been able to build LM?**

> BERT and GPT are both based on the transformer architecture, but they use different parts of the architecture to build language models.
>
> BERT is based on the encoder part of the transformer architecture, which is responsible for processing the input sequence and producing a sequence of hidden representations. The final hidden representation of the [CLS] token, which is added to the input at the beginning of the sequence, is used as an input to downstream tasks. In other words, BERT learns a general representation of the input text, which can then be used for a wide range of tasks.
>
> GPT, on the other hand, is based on the decoder part of the transformer architecture, which is responsible for generating the output sequence based on the hidden representations produced by the encoder. GPT uses a left-to-right language modeling objective, where the model is trained to predict the next word in a sequence given the previous words.
>
> Despite the fact that BERT and GPT use different parts of the transformer architecture, they are both able to build powerful language models. BERT is particularly effective for tasks that require understanding of the entire input sequence, such as question answering and natural language inference. GPT, on the other hand, is particularly effective for tasks that involve generating coherent and fluent text, such as text completion and text generation.
>
> Overall, the transformer architecture provides a powerful framework for building language models, and both BERT and GPT demonstrate the effectiveness of this approach. The choice of whether to use the encoder or decoder part of the architecture depends on the specific task and the nature of the input and output sequences.
