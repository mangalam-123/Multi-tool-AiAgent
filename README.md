# Cricket Stats Agent (Google ADK + Gemini)

A **multi-tool agent** built with **Google Agent Development Kit (ADK)** and **Gemini** that describes international cricketers' **stats** (ODI, Test, T20) and **bio** (nationality, place of birth).

## Features

- **International stats**: Test, ODI, and T20 (matches, runs, batting average, wickets).
- **Bio**: Nationality and place of birth.
- **Multi-tool**: The agent chooses among `get_cricketer_international_stats`, `get_cricketer_bio`, and `list_available_cricketers`.

## Prerequisites

- Python 3.10+
- [Gemini API key](https://aistudio.google.com/app/apikey)

## Setup

1. **Create and activate a virtual environment (recommended):**

   ```bash
   python -m venv .venv
   source .venv/bin/activate   # macOS/Linux
   # .venv\Scripts\activate    # Windows
   ```

2. **Install dependencies:**

   ```bash
   pip install -r requirements.txt
   ```

3. **Set your Gemini API key:**

   ```bash
   cp cricket_agent/.env.example cricket_agent/.env
   # Edit cricket_agent/.env and set GOOGLE_API_KEY="your_key"
   ```

## Run the agent

From the **project root** (the folder that contains `cricket_agent/`):

**CLI:**

```bash
adk run cricket_agent
```

**Web UI (dev only):**

```bash
adk web --port 8000
```

Then open http://localhost:8000, select **cricket_stats_agent**, and chat.

## Example prompts

- "What are Virat Kohli's ODI and Test stats?"
- "Where was Sachin Tendulkar born and what is his nationality?"
- "Give me full stats and bio for Babar Azam."
- "Which cricketers can you look up?"

## Project layout

```
Ai-Agents/
  cricket_agent/
    __init__.py
    agent.py          # ADK agent + tools
    cricket_data.py   # Player data (stats + bio)
    .env.example
    .env              # GOOGLE_API_KEY (create from .env.example)
  requirements.txt
  README.md
```

Data is bundled in `cricket_data.py` for demo; you can extend it or plug in an external cricket API later.

## Rate limits (429 RESOURCE_EXHAUSTED)

If you see **429 RESOURCE_EXHAUSTED** or "quota exceeded":

- **Free tier**: The agent uses `gemini-2.5-flash`, which has free-tier limits (e.g. requests per minute/day). If you hit the limit, wait a few minutes or try again the next day.
- **Check usage**: [Google AI Studio – Rate limit](https://ai.dev/rate-limit) and [Gemini API rate limits](https://ai.google.dev/gemini-api/docs/rate-limits).
- **Other model**: In `cricket_agent/agent.py` you can change `model=` to e.g. `gemini-2.5-flash-preview` or another [supported model](https://ai.google.dev/gemini-api/docs/models) that has quota on your plan.
