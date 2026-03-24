# Copilot Workspace Instructions

## Mandatory Development Checklist

Before committing, all three must pass:

- [ ] `uv run ruff check .` — lint, no errors
- [ ] `uv run uvicorn app.main:app --port 8000` — app starts cleanly
- [ ] `uv run pytest` — all tests green

## Project

**Soc Ops** — Social Bingo game (FastAPI + Jinja2 + HTMX). Players mark squares matching people they find; 5-in-a-row wins.

## Architecture

```
app/
├── main.py          # FastAPI routes (HTMX partial responses)
├── models.py        # Pydantic: GameState, BingoSquareData, BingoLine
├── game_logic.py    # Pure functions: generate_board, toggle_square, check_bingo
├── game_service.py  # GameSession dataclass + _sessions: dict[str, GameSession]
├── data.py          # QUESTIONS list, FREE_SPACE constant
├── templates/       # base.html, home.html, components/
└── static/css/app.css  # Custom Tailwind-like utilities
tests/               # test_api.py (TestClient), test_game_logic.py (unit)
```

## Rules

- Python 3.13+: modern syntax, type hints on all functions
- Immutable models: mutate via `.model_copy(update={})`, never direct assignment
- POST routes return **partial HTML** (components only), never full pages
- No JS — logic lives in Jinja2 + HTMX attributes only
- CSS: use classes from `app.css` only — no inline styles, no Tailwind CDN

## State Flow

`START` → `/start` → `PLAYING` → `/toggle/:id` (bingo) → `BINGO` → `/dismiss-modal` → `PLAYING`
Any state → `/reset` → `START`
