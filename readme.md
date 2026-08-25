# ResearchMind 🔬

A multi-agent AI research pipeline built with LangChain. Four specialized agents work in sequence — searching, scraping, writing, and critiquing — to turn a single topic into a polished, sourced research report.

## How it works

```
Topic
  │
  ▼
1. Search Agent   → finds recent, reliable info via Tavily web search
  │
  ▼
2. Reader Agent    → scrapes the most relevant URL for deeper content
  │
  ▼
3. Writer Chain    → drafts a structured report (Intro / Findings / Conclusion / Sources)
  │
  ▼
4. Critic Chain    → scores the report and gives strengths + areas to improve
```

## Project structure

| File | Purpose |
|---|---|
| `agents.py` | Builds the search & reader agents, and defines the writer/critic chains |
| `tools.py` | `web_search` (Tavily) and `scrape_url` (requests + BeautifulSoup) tools |
| `pipeline.py` | CLI entry point — runs the full 4-step pipeline for a given topic |
| `app.py` | Streamlit UI for the pipeline, with live step-by-step progress |
| `requirements.txt` | Python dependencies |

## Setup

1. **Clone & install**
   ```bash
   pip install -r requirements.txt
   ```

2. **Set environment variables** — create a `.env` file in the project root:
   ```
   OPENAI_API_KEY=your_openai_key
   TAVILY_API_KEY=your_tavily_key
   ```

## Usage

**CLI:**
```bash
python pipeline.py
```
You'll be prompted for a research topic, then each step prints its output as it completes.

**Web UI (Streamlit):**
```bash
streamlit run app.py
```
Enter a topic, hit "Run Research Pipeline," and watch the four agents run live. The final report can be downloaded as a `.md` file.

## Tech stack

- **LangChain** (`create_agent`) for the search/reader agents
- **ChatOpenAI (gpt-4o-mini)** as the underlying LLM
- **Tavily** for web search
- **BeautifulSoup** for content scraping
- **Streamlit** for the front-end

## Notes

- The reader agent scrapes only the top result from search (`[:800]` chars of search context is passed in).
- Scraped content is truncated to 3000 characters to keep the writer chain's context manageable.
- `.env` is gitignored — never commit API keys.