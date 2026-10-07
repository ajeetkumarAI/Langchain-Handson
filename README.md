# LangChain Hands-on: From Basics to Agents in 10 Days

A practical, step-by-step LangChain course in Jupyter notebooks. Each day builds on the previous one, and every notebook ends with a small project you can run and modify.

Trainer: Ajeetkumar

## How the notebooks are written

- Small code cells, one idea per cell, with comments explaining what each line does
- A plain-English explanation and a flow diagram before every concept
- **Pause and predict** questions with click-to-reveal answers
- Charts to make ideas visible: token usage, embeddings maps, similarity heatmaps, chunk sizes, latency and cost dashboards
- **Your turn** cells to practise, plus a "common mistakes" table each day
- All examples use one fictional company, **NovaTech**, so the story carries from day to day

## Course plan

| Day | Notebook | Topics | Mini project |
|-----|----------|--------|--------------|
| 1 | `Day01_LangChain_Basics_Chat_Models.ipynb` | Setup, `ChatOpenAI`, messages, temperature, invoke / stream / batch, `init_chat_model` | Python tutor |
| 2 | `Day02_Prompts_Parsers_Structured_Output.ipynb` | Prompt templates, few-shot, output parsers, `with_structured_output` | Customer review analyser |
| 3 | `Day03_LCEL_Runnables_Chains.ipynb` | LCEL, `RunnableLambda`, `RunnablePassthrough`, `RunnableParallel`, routing, fallbacks, retries | Content pipeline that reviews itself |
| 4 | `Day04_Memory_Conversation_History.ipynb` | Chat history, `RunnableWithMessageHistory`, sessions, trimming, summarising, persistent history | StudyBuddy chatbot |
| 5 | `Day05_Documents_Embeddings_VectorStores.ipynb` | Loaders (TXT, PDF, CSV), text splitters, embeddings, cosine similarity, InMemory / Chroma, retrievers, MMR | Policy semantic search |
| 6 | `Day06_RAG_Retrieval_Augmented_Generation.ipynb` | RAG chain, grounding, sources and citations, conversational RAG, multi-query, LLM-as-judge evaluation | HR helpdesk bot |
| 7 | `Day07_Tools_and_Tool_Calling.ipynb` | `@tool`, `bind_tools`, tool calls, `ToolMessage`, errors, writing the tool loop | Customer support assistant |
| 8 | `Day08_Agents_create_agent_Middleware.ipynb` | `create_agent`, streaming steps, checkpointer memory, `response_format`, runtime context, middleware, human-in-the-loop | NovaTech HR agent |
| 9 | `Day09_Production_Essentials.ipynb` | Async, caching, token and cost tracking, callbacks, debugging, LangSmith, rate limiting, guardrails, FastAPI | Production support chain with dashboard |
| 10 | `Day10_Capstone_NovaTech_Assistant.ipynb` | Everything together, evaluation, monitoring, optional Gradio UI | NovaTech AI Assistant |

## Setup

1. **Create a virtual environment** (recommended)

   Windows:
   ```
   python -m venv .venv
   .venv\Scripts\activate
   ```
   macOS / Linux:
   ```
   python -m venv .venv
   source .venv/bin/activate
   ```

2. **Install the packages**
   ```
   pip install -r requirements.txt
   ```
   (Day 1 also has a cell that does this from inside Jupyter.)

3. **Add your API key**: copy `.env.example` to `.env` and paste your OpenAI key:
   ```
   OPENAI_API_KEY=sk-...
   OPENAI_MODEL=gpt-4.1-nano
   ```
   `.env` is in `.gitignore`, so it is never pushed to GitHub.

4. **Open the notebooks** in Jupyter or VS Code, start with Day 1 and run the cells from top to bottom.

### About the model

The series uses OpenAI's low-cost nano model. `gpt-4.1-nano` supports every feature used here, including `temperature`. To switch models, change `OPENAI_MODEL` in `.env`. If you pick a reasoning model such as `gpt-5-nano`, remove the `temperature=` arguments, because those models only accept the default temperature.

## Project structure

```
Langchain-Handson/
|-- Day01 ... Day10 notebooks
|-- data/
|   |-- policies/
|   |   |-- leave_policy.txt
|   |   |-- it_security_policy.txt
|   |   |-- travel_expense_policy.txt
|   |   |-- product_faq.md
|   |   |-- code_of_conduct.pdf
|   |-- employees.csv
|   |-- orders.csv
|-- requirements.txt
|-- .env.example
|-- README.md
```

All data is fictional (NovaTech Solutions and its CloudDesk product) and was created for this course.

Some notebooks create local folders while you run them (`chroma_db/`, `chroma_capstone/`, `chat_histories/`) and the file `serve_app.py`. They are safe to delete; the notebooks re-create them.

## Package versions

Written for the LangChain 1.x line (`langchain`, `langchain-core`, `langchain-openai` 1.x, `langgraph` 1.x). If an import fails, upgrade with `pip install -U -r requirements.txt`.

## Troubleshooting

| Problem | Fix |
|---------|-----|
| `API key found? False` | `.env` must be in the same folder as the notebooks; on Windows check it is not saved as `.env.txt`. Restart the kernel. |
| `AuthenticationError` | The key is wrong or has no credit. |
| `Unsupported value: temperature` | You are using a reasoning model. Remove `temperature`. |
| `RateLimitError` / 429 | Lower `max_concurrency` in `batch()`, or use the rate limiter from Day 9. |
| `print_ascii` fails | `pip install grandalf` |
