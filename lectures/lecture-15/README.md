# Lecture 15 - Retrieval-Augmented Generation and Fine-Tuning

The last lecture of the AI module. Lecture 12 put a model on your laptop, lecture 14 called one from your own code, and this one answers the question both left open: how do you make a model answer questions about documents it has never read?

[View the slides](https://danilofreire.github.io/datasci350/lectures/lecture-15/15-rag-finetuning.html)

## What we cover

- Embeddings for whole passages, and cosine similarity
- Getting embeddings from Ollama with `embeddinggemma`
- The five stages: chunk, embed, store, retrieve, generate, and where each one fails
- Why retrieval beats pasting everything in: the cost arithmetic, and "lost in the middle"
- A working pipeline in about 40 lines (`demo/rag.py`), using Ollama and the [Chroma](https://github.com/chroma-core/chroma) vector database
- Measuring retrieval with test questions and a hit rate
- Hybrid search, BM25, and rerankers, for the questions embeddings get wrong
- Prompt injection through a poisoned corpus, and three partial defences
- Fine-tuning: context versus weights, training data, LoRA, QLoRA and Unsloth
- Distillation, and the dispute it started
- The ladder: prompt, then RAG, then fine-tune, climbed only when the step below fails

## Before class

Warning: the downloads total about 2.3 GB (two models and the `chromadb` package). Do not attempt them on classroom wifi.

1. Install or update Ollama from [ollama.com](https://ollama.com/).
2. Run `ollama pull embeddinggemma`.
3. Run `ollama pull llama3.2:1b`.
4. Run `pip install ollama chromadb`.

If `ollama pull embeddinggemma` fails, your Ollama is too old. Update the application, or use `nomic-embed-text` (274 MB) and change the model name in both `ollama.embed` calls in `rag.py`. If you cannot run local models, use the OpenRouter variant in Appendix 03 with your key from lecture 14.

## The demo folder

`demo/rag.py` is the whole pipeline in one file, in four steps, and `demo/corpus/` holds eight of this course's own READMEs, which split into 132 paragraphs. Run it from inside `demo/` and type your question when asked:

```bash
python rag.py
```

It prints the number of chunks stored, the files the three closest paragraphs came from, their similarity scores, and the answer. Read the sources and scores before the answer: when an answer is wrong, they tell you whether retrieval or generation failed.

## What the evaluation found

Of seven test questions, five retrieved the right file in the top three. The two misses are both gaps in the corpus:

- "How much is the final project worth?" fails because no file gives the project's weight. The best match (0.38) is a quiz that is "worth 6%".
- "When is Quiz 02?" misses the quiz's own file, and no paragraph gives a date anyway. Its top match scored 0.58, almost as high as the best successful question (0.59), so a confidence threshold would have passed it straight to the model.

A high similarity means the topic matched, not that the answer is present. Retrieval also repeats and generation does not: run the script several times and the similarities stay the same, while the written answer can change.

## Practice

Run the pipeline with "What does Quiz 02 cover?", then with two questions of your own, and check each answer against its sources. Ask "What is the capital of Nepal?" and compare its similarities with the others. Retrieval always returns three paragraphs, because there is always a top three, and only the model can say that the data has no answer. Finally, change `n_results=3` to `n_results=1` in `rag.py` and find which questions break first.

Notes are in Appendix 01 and troubleshooting in Appendix 04.

## Before the next class

1. Finish the exercise.
2. Keep Ollama and both models on the laptop you will bring.

Next class starts the cloud module. Every computer in this course has been yours so far, and next we borrow someone else's. Quiz 03 covers the AI module and the cloud module.

## Using AI in this course

You may use AI for the assignments in this course. Cite the tool you used, check everything it gives you, and remember that the fluency of an answer tells you nothing about whether it is correct.

Using AI tools in a manner prohibited in this course syllabus constitutes Cheating under the Emory Honour Code and is thus a form of academic misconduct.
