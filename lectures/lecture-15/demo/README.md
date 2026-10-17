# RAG demo: ask the course about itself

A minimal retrieval-augmented generation pipeline in one file, `rag.py`. It answers questions about the Markdown files in `corpus/`, which are copies of this course's own READMEs. It has four steps: split the files into paragraphs, embed them with Ollama and store them in [Chroma](https://github.com/chroma-core/chroma), find the three paragraphs closest to your question, and ask a small local chat model to answer from them.

## Setup

Warning: the downloads total about 2.3 GB (two models and the `chromadb` package). Use a good connection.

1. Install Ollama from [ollama.com](https://ollama.com/).
2. Run `ollama pull embeddinggemma`.
3. Run `ollama pull llama3.2:1b`.
4. Run `pip install ollama chromadb`.

## Run it

1. Open a terminal inside this folder, so that Python finds `corpus/`.
2. Run `python rag.py` and type your question when asked.
3. The script prints the number of chunks stored, the source file of each of the three closest paragraphs, their similarity scores, and the model's answer.

Then experiment:

- Ask something the corpus can answer, such as "Which tutorials does the course have?", and check the answer against its sources.
- Ask something the corpus cannot answer ("What is the capital of Nepal?") and compare the similarities.
- Change `n_results=3` to `n_results=1` in `rag.py` and see which questions get worse.
- Change `"corpus"` in `rag.py` to a folder of your own notes.

If `ollama pull embeddinggemma` fails, update Ollama, or pull `nomic-embed-text` and change the model name in both `ollama.embed` calls.

The lecture slides (`../15-rag-finetuning.qmd`) walk through the script step by step, and Appendix 03 has an OpenRouter variant for laptops that cannot run local models.
