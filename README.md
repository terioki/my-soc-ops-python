# 🎱 Soc Ops

> **Social Bingo for in-person mixers.** Find people around the room who match each square — first to get 5 in a row wins!

[![Python 3.13+](https://img.shields.io/badge/python-3.13%2B-blue?logo=python&logoColor=white)](https://www.python.org/downloads/)
[![FastAPI](https://img.shields.io/badge/FastAPI-0.115%2B-009688?logo=fastapi&logoColor=white)](https://fastapi.tiangolo.com/)
[![uv](https://img.shields.io/badge/uv-package%20manager-8A2BE2)](https://docs.astral.sh/uv/)
[![Ruff](https://img.shields.io/badge/linted%20by-ruff-FCC21B)](https://docs.astral.sh/ruff/)

🎮 **[Play the Game](https://madebygps.github.io/vscode-github-copilot-agent-lab/)** &nbsp;•&nbsp; 📚 **[View Lab Guide](https://madebygps.github.io/vscode-github-copilot-agent-lab/docs/)**

---

## What is Soc Ops?

Soc Ops turns any gathering — meetups, conferences, onboarding days, team offsites — into a lively icebreaker. Each player gets a unique 5×5 bingo board filled with prompts like *"has a pet"* or *"speaks more than 2 languages"*. Walk around, chat with people, mark off matching squares, and shout **BINGO** when you hit five in a row. 🎉

### ✨ Features

| Feature | Description |
|---|---|
| 🔀 **Unique boards** | Every player gets a freshly shuffled board — no two are alike |
| 🆓 **Free space** | The centre square is always free, just like classic bingo |
| ⚡ **No page reloads** | Squares toggle instantly via HTMX — zero JavaScript written by hand |
| 🏆 **Bingo detection** | Rows, columns, and diagonals are all checked automatically |
| 🔄 **Reset anytime** | Start a brand-new game with one click |

---

## 🛠 Tech Stack

| Layer | Technology |
|---|---|
| **Backend** | [FastAPI](https://fastapi.tiangolo.com/) + [Uvicorn](https://www.uvicorn.org/) |
| **Templating** | [Jinja2](https://jinja.palletsprojects.com/) |
| **Interactivity** | [HTMX](https://htmx.org/) (no hand-written JS) |
| **Styling** | Custom CSS utility classes (à la Tailwind) |
| **Package manager** | [uv](https://docs.astral.sh/uv/) |
| **Linter** | [Ruff](https://docs.astral.sh/ruff/) |

---

## 🚀 Quick Start

### Prerequisites

- [Python 3.13+](https://www.python.org/downloads/)
- [uv](https://docs.astral.sh/uv/) package manager

### Install & run

```bash
# 1. Install dependencies
uv sync

# 2. Start the dev server
uv run uvicorn app.main:app --reload
```

Open **http://localhost:8000** in your browser and start playing!

### Devcontainer / Codespaces

This repository ships with a pre-configured devcontainer — no local setup required.

- **VS Code**: Clone the repo and choose **Reopen in Container** when prompted.
- **GitHub Codespaces**: Click **Code → Codespaces → Create codespace on main** in your fork.

---

## 🧪 Test & Lint

```bash
# Run the test suite
uv run pytest

# Lint & format
uv run ruff check .
uv run ruff format .
```

---

## 🗂 Project Structure

```
app/
├── main.py          # FastAPI routes (HTMX partial responses)
├── models.py        # Pydantic models: GameState, BingoSquareData, BingoLine
├── game_logic.py    # Pure functions: generate_board, toggle_square, check_bingo
├── game_service.py  # Session management
├── data.py          # Bingo prompts & FREE_SPACE constant
├── templates/       # Jinja2 templates (base, home, components)
└── static/css/      # Custom CSS utility classes
tests/               # API tests (TestClient) + game logic unit tests
workshop/            # Offline lab guide
```

---

## 📚 Lab Guide

This project is also a hands-on workshop for learning GitHub Copilot agent mode. Work through the steps below to build the game from scratch.

| Part | Title |
|------|-------|
| [**00**](https://madebygps.github.io/vscode-github-copilot-agent-lab/docs/step.html?step=00-overview) | Overview & Checklist |
| [**01**](https://madebygps.github.io/vscode-github-copilot-agent-lab/docs/step.html?step=01-setup) | Setup & Context Engineering |
| [**02**](https://madebygps.github.io/vscode-github-copilot-agent-lab/docs/step.html?step=02-design) | Design-First Frontend |
| [**03**](https://madebygps.github.io/vscode-github-copilot-agent-lab/docs/step.html?step=03-quiz-master) | Custom Quiz Master |
| [**04**](https://madebygps.github.io/vscode-github-copilot-agent-lab/docs/step.html?step=04-multi-agent) | Multi-Agent Development |

> 📝 Lab guides are also available in the [`workshop/`](workshop/) folder for offline reading.

---

## State Flow

```
START ──/start──▶ PLAYING ──/toggle/:id──▶ BINGO ──/dismiss-modal──▶ PLAYING
  ▲                  │                                                    │
  └──────────────────┴─────────────/reset──────────────────────────────--┘
```

---

Deploys automatically to GitHub Pages on push to `main`.
