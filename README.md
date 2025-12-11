🌐 Research Agent

A lightweight web research assistant that searches the internet, extracts meaningful passages, ranks them using semantic embeddings, and generates a concise extractive summary of the most relevant information.

🚀 Features

✔ DuckDuckGo Web Search (no API key required)
✔ Extract and clean text from webpages
✔ Break long text into short, meaningful passages
✔ Embed passages using Sentence Transformers
✔ Rank passages using cosine similarity
✔ Generate a short extractive summary with source links
✔ Highly configurable: results count, passage size, model, timeout, etc.

🛠️ Built With

🦆 DuckDuckGo Search (ddgs)

🌐 Requests + BeautifulSoup4 for webpage scraping

🧠 Sentence-Transformers (all-MiniLM-L6-v2)

🔢 NumPy for similarity scoring

📦 Requirements
Python Version
Python 3.8+

Install Dependencies
pip install ddgs requests beautifulsoup4 sentence-transformers numpy


⏳ The first run downloads the SentenceTransformer model — may take ~50–100MB.

▶️ Quick Demo
python main.py

Example Output
Running query: What are the most recent and significant developments in the field of AI from the past 2-3 years?

Top passages:
- score 0.842 src https://...
  ...transformers and large language models (LLMs) have advanced...

--- Extractive summary ---
Large language models have advanced state-of-the-art results in many tasks (Source: https://...). 
Transformer architectures and scaling laws enabled better performance (Source: https://...). 
Diffusion models and multimodal learning expanded generative AI capabilities (Source: https://...).
--------------------------
Done in 8.7s

⚙️ Configuration (Editable in Code)
SEARCH_RESULTS = 6
PASSAGES_PER_PAGE = 4
EMBEDDING_MODEL = "sentence-transformers/all-MiniLM-L6-v2"
TOP_PASSAGES = 5
SUMMARY_SENTENCES = 3
TIMEOUT = 8

🧠 How It Works
1️⃣ Search

DuckDuckGo returns the top URLs for the query.

2️⃣ Fetch

Each URL is downloaded and cleaned (scripts, ads, navbars removed).

3️⃣ Chunk

Text is split into small passages (~120 words each).

4️⃣ Embed

Passages and query are converted into high-dimensional vectors.

5️⃣ Rank

Cosine similarity determines which passages best match the query.

6️⃣ Summarize

Top sentences across passages are selected + source links included.

📌 Usage Example
agent = ShortResearchAgent()
out = agent.run("What are the major trends in renewable energy in 2024?")
print(out["summary"])

📁 Project Structure
├── maint.py   # Main script
└── README.md                 # Documentation

📄 License

MIT License — free to use, modify, and distribute.

💡 Credits

🔍 DuckDuckGo Search via ddgs

🧠 Sentence Embeddings via sentence-transformers

🌐 HTML parsing via BeautifulSoup4
