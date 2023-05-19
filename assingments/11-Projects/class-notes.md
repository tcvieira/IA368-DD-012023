# Class 11 Notes 18/05/2023

## APRESENTAÇÕES NOTEBOOK MULTI-DOC-QA

- usar pygaggle em notebook diferente ou instalar git com `pip install git+https://github.com/castorini/pygaggle.git -q`
- cohere reranker opção (marcos piau) co.rerank retorna textos ranqueados com score
- usar o mono-t5 do InPars: https://github.com/zetaalphavector/inPars
- gustavo bartz usou splade aula 7/8 pra criar o indice invertido + cohere + prompt estático
- Injecting the BM25 Score as Text Improves BERT-Based Re-rankers - https://arxiv.org/pdf/2301.09728.pdf
- llama parece melhor com o llama pra gerar as explicações (rerank o prof n testou)
- usar o T5 grande ou vai para o minilmv2(BERT-distill 20-30M imita os scores de attention e não só a saída dele)
- usar gpt-3.5/4 para analisar se as respostas são semanticamente equivalentes n hora de avaliar ao invés de usar f1/exact-match
- "uso haystack (library python) e base elastic com meta dados no documento.
Daí, na etapa do retrieval, posso aplicar filtros usando campos dos metadados: result = pipeline_embedding_retrieval_sts_ranker_minilm_bilingual.run(query=parm_query, params={"Retriever": {"top_k": 15,"classe": ["Termo"]}, "Ranker": {"top_k": 10}})"
- leonardo bernardi conseguiu um bom f1 e usou o pipeline vanila (como o text-davinci-002 é usado pra gerar texto, talvez explique melhor resultado que o gpt-3.5 pq ele é tunado pra chat?)
- thiago laitz decompose query using prompt zero-shot

## Projects

1) sumarizador/agregador de diversos documentos (científicos) para gerar survey (completo ~50 páginas) data uma query (neural information retrieval)
   - poderia começar pelo abstract/title pra buscar mais
   - usar um query unica ou decompor/gerar em subqueries por seção, por exemplo
   - usando somente dados de buscadores (google scholar por exemplo e pegar os tpok-50/100)
   - passar para o gpt eles pra escrever a seção (de repente ir fatiando as seções)
   - como avaliar?
   - gera sobre uma subseção de seção e compara com o ground-truth perguntando ao gpt
- discussões:
  - O wordtune da ai21 labs faz algo parecido .. mas com um artigo
  - Ia sugerir isso que o jayr falou dividir o artigo em pedacos do tamanho da janela maxima do modelo , usar o bert topic para calssificar os segmentos em tópicos e depois apresentar pro modelo sumarizar segmentos agrupados por topicos e e finalmente sintetizar a apresentacao dos topicos organizando o survey pelos topicos

2) Dataset UNICAMP-IR
   -  

3) treinar MSMARCO traduzindo pt + original en e fazer o finetuning no ColBERTv2 multi vector dense retrievers ou Spladev2
   - bertimbau, albertinapt-pt, t5multilingual
   - muda a loss no treinamento de cada um e a inferencia no pipeline
   - sao estados da arte de um estágio
   - colbertv1 em pt só pegou o v1 e colocar no msmarco em pt
