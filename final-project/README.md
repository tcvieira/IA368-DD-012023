# Final Project

## Selection

- queria pegar o problema 1 e usar um llama index nos docs buscados/extraídos e ranqueados + gpt4 pra gerar titulo/seções
  - usar llama index pra pegar o resultado dos artigos pesquisados e ficar fácil de pesquisar
  - usar langchain de repente pra fazer esse browsing com ações, tipo o Visconde faz
  - se não, usar o langchain direto pra controlar/refinar/gerar os prompts para o gpt4 fazendo tipo o visconde pra ter as referencias de onde tirou
  - tudo em um streamlit em uma interface tipo chat ou direta msm, cuspindo as seções com título em markdown
    - com escolhas de pedir pra escrever em tom mais cientifico, leman terms, for a child
  - https://github.com/jerryjliu/llama_index
  - https://www.youtube.com/watch?v=b-aCPBNG1do
  - olhar meus artigos anotados com relação a isso

## Background

- PLM - pretrained language models
- SPLADE sparse model family objectives
  - effective
  - efficient
  - interpretable
  - robust
- uso do Bert implicitamente aprende a realizar expansão: topk logits para para query expansion
- SPLADE representa queries e documents no espaço de vocabulário usando a MLM head, inspirado pelo SpaTerm2020
- seguir com a explicacao dos slides do phd...passo a passo explicando a arquitetura
  - emb
  - mlm head
  - maxpooling - log saturation on term weights: prevent some terms to dominate
- splade model learn term expansion and also term weighting
  - given a **query** its representations from splade has
    - its weights for each term
    - generate new terms and its weights
    - remove non important terms
  - given a **document** its representations from splade has
    - same as the query
    - but perform compression on the representations as it remove non important terms
- treinado no MSMARCO
- minimize negative likehood...
  - exp_positive docs over exp_sum_negative docs from BM25 + in-batch negatives
- FLOPS2020 makes representations sparse and spread - sparse regularization (ask gpt4)
  - there a hyperparam to control sparsity (check on code?)

### Intro

SPLADE [Formal et al., 2021b] is a transformer-based retrieval model, that relies on the Masked Language Modeling (MLM) head and max pooling over the tokens to represent documents and queries. Thus, the document (or query) representation has the same number of dimension as the amount of words in the transformer vocabulary (in this case BERT [Devlin et al., 2018], with |V | ≈ 30000). The model is trained by jointly optimizing ranking and regularization losses; consequently, retrieval can be done in a sparse fashion, as only a few dimensions are activated by the SPLADE model for a given document (or query) [3].

The training of SPLADE is done via optimization of a contrastive loss (InfoNCE) using hardnegatives (from BM25) and in-batch negatives, constrained by a regularization that aims at reducing
the amount of expected floating-point operations during retrieval [3].

We embed all queries, positive_passages, and negative_passages into the vector space. The matching (query_i, positive_passage_i) should be close, while there should be a large distance between a query and all other (positive/negative) passages from all other triplets in a batch. For a batch size of 64, we compare a query against 64+64=128 passages, from which only one passage should be close and the 127 others should be distant in vector space.

One way to improve training is to choose really good negatives, also know as hard negative: The negative should look really similar to the positive passage, but it should not be relevant to the query.

### Metodology

- download mmarco-pt
- create/check dataset format for training
- build/download bm25 inverted index for mmarco-pt and store - https://github.com/unicamp-dl/mMARCO#bm25-baseline-for-portuguese
- train bertimbau on mmarco-pt - https://github.com/unicamp-dl/mMARCO/blob/main/scripts/train_minilm.py
- select which approach will be used
  - from naver/splade - forked https://github.com/tcvieira/splade
    - SPLADE v2 modify the pooling mechanism and introduce models trained with distillation 
    - create config files for experiments and train
- initially finetune + evaluate
- then pretrain + evaluate
- results

### Future work

- distillation with the work [Hofstatter et al., 2020], and train SPLADE with the MarginMSE loss1 (thus replacing the InfoNCE loss using the provided cross-encoder teacher scores from https://github.com/
sebastian-hofstaetter/neural-ranking-kd) [3].
- Analysed Queries [3]
  - Worst performing queries : text + ndcg@10 (baseline spladev2 msmarco en: ?; Median: ?; new spladev2 mmarco pt: ?)
    - Top-5 passages retrieved by baseline and new

## SPLADEv2

- começar com o bertimbau pq é menor
- verificar se o albertina com 128 tokens vai atrapalhar
- se vai indexar os documentos todos ou as passagens, ou documento truncado (perco informacao). indexar com passagem tem mais informação
- treinar somente 10 epochs (~10% dos dados msmarco pt das 40M de linhas) no qrels nas primeiras 4M do dataset pq o q varia é o negativo amostrado do bm25
- testa primeiro só com o dataset pt...e depois vê se usa o ingles (pq tem q usar de outro jeito pra pegar os negativos)

## Refs

- [1] https://www.youtube.com/watch?v=E57rb10buTY
- [2] https://cadurosar.github.io/
  - https://twitter.com/cadurosar/status/1653379205453824009
- [3] https://europe.naverlabs.com/wp-content/uploads/2022/05/NLE-SPLADE-at-TREC-1.pdf
- [4] https://github.com/cadurosar/learned-sparse-retrieval
  - https://github.com/cadurosar/learned-sparse-retrieval/blob/main/lsr/configs/experiment/splade_asm_tripclick_multiple_negative_l1_0.001_0.00001.yaml
  - https://github.com/cadurosar/learned-sparse-retrieval/blob/main/lsr/configs/experiment/splade_msmarco_multiple_negative.yaml
- [5] sbert - MS MARCO Cross-Encoders https://www.sbert.net/docs/pretrained-models/ce-msmarco.html
  - https://github.com/UKPLab/sentence-transformers/tree/master/examples/training/ms_marco
- [6] https://www.pinecone.io/learn/splade/
- [7] mRobust - https://arxiv.org/pdf/2209.13738.pdf
- [8] mMARCO is a multilingual version of the MS MARCO passage ranking dataset - https://github.com/unicamp-dl/mMARCO
- [9] https://huggingface.co/datasets/sentence-transformers/msmarco-hard-negatives
- [10] From Distillation to Hard Negative Sampling: Making Sparse Neural IR Models More Effective https://arxiv.org/pdf/2205.04733.pdf
- [11] SPLADE – a sparse bi-encoder BERT-based model achieves effective and efficient first-stage ranking https://europe.naverlabs.com/blog/splade-a-sparse-bi-encoder-bert-based-model-achieves-effective-and-efficient-first-stage-ranking/
- [12] SPLADE video https://vimeo.com/723352803
- [13] SPLADE models - https://europe.naverlabs.com/research/machine-learning-for-robotics/splade-models/
- [14] An Experimental Study on Pretraining Transformers from Scratch for IR https://arxiv.org/pdf/2301.10444.pdf
- [15] BERTimbau - Portuguese BERT https://github.com/neuralmind-ai/portuguese-bert
  - https://huggingface.co/neuralmind/bert-base-portuguese-cased
