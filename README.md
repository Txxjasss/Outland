# OUTLAND 🌲

> **Your next adventure starts outside.**

**Less scroll. More soul.** OUTLAND is your personal AI adventure guide. Turn spare moments into outdoor discoveries, powered by open-source AI.

Built for the Hacktoberfest 2026 Open-Source AI Challenge — Week 1: **Touch Grass**.

---

## Purpose

Screens and algorithmic feeds compete for every minute of attention. OUTLAND was created to help people spend less time on screens by generating personalized, low-pressure outdoor missions based on available time, mood, surroundings, and interests.

The design philosophy is simple: **the screen should be the shortest part of the experience**. OUTLAND delivers a concise plan, safety reminders, and clear intention—then gets out of the way so you can step outside.

---

## Architecture & Technology Stack

OUTLAND is deliberately lightweight, inspectable, and dependency-free:

- **Frontend:** Semantic HTML5, Vanilla CSS, and Vanilla JavaScript (`index.html`). No build step, bundler, or heavy framework required.
- **Design System:** Custom CSS properties featuring a signature forest-green (`#244d3a`), warm-ivory (`#f5f4eb`), and lime-accent (`#d5f36a`) palette, editorial typography, oversized headlines, and a responsive dual-column layout.
- **Local AI Engine:** [Ollama](https://ollama.com/) running locally via HTTP API (`http://localhost:11434`), configured for the open-weight `qwen2.5:3b` model.
- **Local Web Server:** Python 3 standard library HTTP server (`python3 -m http.server 8000`).
- **Privacy & Security:** All prompts and user selections stay on your local machine during local inference. No user accounts, analytics, cookies, third-party trackers, or cloud databases.

---

## Local Setup

### Prerequisites

- Python 3
- A modern web browser
- (Optional, for local AI) [Ollama](https://ollama.com/)

### Step-by-Step Instructions

1. **Install Ollama** (if you want local AI missions):
   Follow the instructions at [ollama.com](https://ollama.com/) to install Ollama for your operating system.

2. **Pull the model:**
   ```bash
   ollama pull qwen2.5:3b
   ```

3. **Start the Ollama service:**
   Ollama typically starts automatically as a system background service. You can confirm it is running by checking `http://localhost:11434/api/tags` or running `ollama list`.

4. **Start the local web server:**
   In the project folder, run:
   ```bash
   python3 -m http.server 8000
   ```

5. **Open OUTLAND:**
   Visit `http://localhost:8000` in your browser.

---

## Ollama Integration & Fallback Behavior

- **Automatic Connection Check:** On page load, OUTLAND queries `http://localhost:11434/api/tags`. If Ollama and installed models are detected, the status pill updates to confirm connection.
- **Local AI Inference:** When you click "Generate my mission", OUTLAND issues a POST request to `http://localhost:11434/api/generate` with `qwen2.5:3b` and tailored prompts enforcing concise, safe, equipment-free, and privacy-respecting activities.
- **Transparent Fallback Mode:** If Ollama is unavailable, the local service is offline, or no model is installed, OUTLAND automatically engages its built-in deterministic mission engine.
- **Clear Distinguishability:** OUTLAND never claims local AI is working unless actual model inference succeeds. Both the top status pill and the mission card badge clearly indicate whether a result is a **`LOCAL AI MISSION`** (powered by Qwen2.5 3B) or an **`OFFLINE MISSION`** (deterministic fallback).

---

## Current Scope & Features

- Configurable mission parameters: Time available (5–60 min), current vibe, destination type, and optional interest.
- Local model inference via Ollama (`qwen2.5:3b`).
- Built-in curated offline fallback missions.
- Fully responsive layout designed for mobile and desktop screens.
- Zero tracking, telemetry, or account requirements.

---

## Limitations

- Local AI generation requires Ollama installed and the `qwen2.5:3b` model downloaded (~1.9 GB).
- Browser requests to Ollama rely on localhost cross-origin request permissions (supported by default in standard local setups).
- Fallback missions are a curated fixed collection rather than dynamically generated text.
- Future work: PWA offline caching, community mission packs, accessibility audits, and optional local nature-identification models.

---

## License

MIT — see [LICENSE](LICENSE).

> *Note: Open-weight model weights are subject to their respective creators' license terms. Check the model license before commercial use or redistribution.*
