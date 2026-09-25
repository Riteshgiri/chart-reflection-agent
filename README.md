# Chart Reflection Agent

An agentic AI workflow that uses the **reflection pattern** to generate and improve data visualizations.

1. **Generate (V1)** — a fast LLM writes matplotlib code for a chart request.
2. **Execute** — the code is extracted from `<execute_python>` tags and run to produce `*_v1.png`.
3. **Reflect** — a stronger multi-modal LLM reviews the chart image and code, and returns feedback plus improved code.
4. **Regenerate (V2)** — the refined code is run to produce `*_v2.png`.

Example request: *"Create a plot comparing Q1 coffee sales in 2024 and 2025 using the data in coffee_sales.csv."*

## Setup

Requires Python 3.10+.

```bash
python -m venv venv
source venv/bin/activate
pip install -r requirements.txt
```

Create a `.env` file with your API key(s):

```
ANTHROPIC_API_KEY=...
# OPENAI_API_KEY=...   # only if using OpenAI models
```

## Run

```bash
python chart_generation.py
```

Edit `user_instructions`, the models, and `image_basename` at the bottom of `chart_generation.py` to try other charts. By default, `claude-haiku-4-5` generates the first draft and `claude-sonnet-4-6` does the reflection.

## Files

| File | Purpose |
|---|---|
| `chart_generation.py` | The end-to-end reflection workflow |
| `utils.py` | Data loading, LLM calls, and display helpers |
| `coffee_sales.csv` | Coffee vending machine sales data |
| `drink_sales_v1.png`, `drink_sales_v2.png` | Example output: first draft and reflected chart |
