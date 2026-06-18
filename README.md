# Trader Future AGI — CrewAI Crypto Trading Agent

A CrewAI-powered cryptocurrency trading assistant that uses RAG over historical trade data to answer queries about trading strategies and market insights. Integrated with FutureAGI for real-time evaluation of agent outputs (toxicity, tone, helpfulness, context relevance).

## Architecture

```
User query
  → Safety check (FutureAGI toxicity filter)
  → CrewAI Agent (Groq DeepSeek R1)
      └─ Trade Context Retriever tool (LlamaIndex RAG over data/trades.csv)
  → FutureAGI evaluation (tone · helpfulness · context relevance · toxicity)
  → Response
```

## Features

- **Persona detection** — classifies trading style (Meme Trader vs Technical Trader) and risk level from CSV data
- **RAG retrieval** — LlamaIndex + HuggingFace BGE embeddings over historical trade records
- **Safety gate** — FutureAGI toxicity check blocks unsafe queries before they reach the agent
- **Comprehensive evaluation** — every response scored across 4 metrics via FutureAGI

## Tech Stack

- **Agent framework** — CrewAI
- **LLM** — Groq (`deepseek-r1-distill-llama-70b`)
- **RAG** — LlamaIndex + HuggingFace `BAAI/bge-small-en-v1.5`
- **Evaluation** — FutureAGI (`fi.evals`)

## Setup

```bash
pip install -r requirements.txt

# .env
GROQ_API_KEY=...
FI_API_KEY=...
FI_SECRET_KEY=...
```

```bash
python trader_agent.py
```

Type `quit` to exit the interactive session.
