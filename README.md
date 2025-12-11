# Research_agent

A compact research assistant that searches the web, extracts short passages from top results, ranks them with semantic embeddings, and produces an extractive summary of the most relevant sentences.

Built with:

DuckDuckGo search (ddgs)

requests + BeautifulSoup for page scraping

sentence-transformers for embeddings (semantic ranking)

NumPy for similarity ranking

Features

Query web via DuckDuckGo (no API key required).

Fetch and clean HTML text from top URLs.

Chunk long pages into short passages.

Embed passages and the query with a SentenceTransformer model.

Rank passages by cosine similarity and extract top sentences.

Produce a brief extractive summary with source attribution.

Simple, configurable constants for results count, passage size, and model.

Quick Demo
python short_research_agent.py
# or
python3 short_research_agent.py


Sample run (prints top passages and a short extractive summary):

Running query: What are the most recent and significant developments in the field of AI from the past 2-3 years?

Top passages:
- score 0.842 src https://...
  ...transformers and large language models (LLMs) have advanced...

--- Extractive summary ---
Large language models have advanced state-of-the-art results in many tasks (Source: https://...). Transformer architectures and scaling laws enabled better performance (Source: https://...). Diffusion models and multimodal learning expanded generative AI capabilities (Source: https://...).
--------------------------
Done in 8.7s

Requirements

Python 3.8+

pip packages:

ddgs (duckduckgo_search renamed)

requests

beautifulsoup4

sentence-transformers

numpy

Install quickly:

pip install ddgs requests beautifulsoup4 sentence-transformers numpy


The first run will download the SentenceTransformer model (sentence-transformers/all-MiniLM-L6-v2) which may take a minute and some disk space.

Files

short_research_agent.py — main script (the code you provided).

README.md — this file.

Configuration (constants inside the script)

You can tune search/summary behavior by editing top-level constants:

SEARCH_RESULTS = 6        # number of URLs to check
PASSAGES_PER_PAGE = 4     # passages pulled from each URL
EMBEDDING_MODEL = "sentence-transformers/all-MiniLM-L6-v2"
TOP_PASSAGES = 5          # how many passages to consider for summary
SUMMARY_SENTENCES = 3     # number of sentences in final summary
TIMEOUT = 8               # requests timeout for webpages (seconds)

How it works (high level)

Search — use DuckDuckGo to find SEARCH_RESULTS links for the query.

Fetch — download each URL and extract clean text from <p> tags (and fallbacks).

Chunk — split fetched text into passages of ~max_words (default 120).

Embed — encode passages and the query using SentenceTransformer embeddings.

Rank — compute cosine similarity between query and passage embeddings.

Select — pick top TOP_PASSAGES passages, split them into sentences.

Summarize — embed sentences, choose SUMMARY_SENTENCES most similar sentences, de-duplicate and output summary with source links.

Usage / Example

Run a one-off query from the command line. Edit the q variable at the bottom or change the script to accept CLI args:

agent = ShortResearchAgent()
out = agent.run("What are the major trends in renewable energy in 2024?")
print(out["summary"])


Or make it accept user input by replacing the bottom __main__ block with CLI parsing.

License & Credits

MIT-style: feel free to reuse and adapt.

Built using open-source libraries:

DuckDuckGo search via ddgs

BeautifulSoup for HTML parsing

sentence-transformers for embeddings
