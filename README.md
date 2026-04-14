# smart-search

> A search strategy skill for Claude that turns vague queries into rigorous, multi-source research — with built-in bias detection and anti-SEO filtering.

[![Agent Skills](https://img.shields.io/badge/Agent%20Skills-compatible-blue)](https://agentskills.io)
[![Works with Claude Code](https://img.shields.io/badge/Claude%20Code-native-blueviolet)](https://code.claude.ai)
[![Works with Cursor · Gemini CLI · Codex](https://img.shields.io/badge/Cursor%20%7C%20Gemini%20CLI%20%7C%20Codex-compatible-green)](https://agentskills.io)
[![License: Apache 2.0](https://img.shields.io/badge/license-Apache%202.0-brightgreen)](LICENSE)

[中文文档 → README.zh.md](README.zh.md)

---

## The Problem

Claude is a brilliant analyst — but it has a structural blind spot: **it defaults to its training data**, even when that data is 12–24 months out of date. Worse, when it does search, it often retrieves:

- 📰 SEO-optimized "Best X of 2024" listicles with no real testing behind them
- 🔄 Circular citations where every article references the same single source
- 🌐 Only English-language, Western-perspective sources — missing critical alternative viewpoints
- 📣 Surface-level narratives without questioning *who benefits* from the framing
- ❌ A confident single conclusion when the reality is genuinely contested

If you've ever asked Claude about a software tool and got a generic review-site summary, or asked about a geopolitical event and got a single-perspective answer without any alternative analysis — that's this problem in action.

---

## What This Skill Does

`smart-search` is a **strategy layer** that activates before Claude answers any research question. It doesn't add new tools — it changes *how Claude thinks* about searching.

Install it once. It activates automatically whenever Claude detects a search-type request.

### Before vs. After

| Without smart-search | With smart-search |
|---|---|
| Uses stale training data by default | Triages by recency — forces live search for fast-changing info |
| Retrieves top SEO results | Routes to GitHub, Reddit, HN, and primary sources |
| Cites one or two sources | Cross-verifies across ≥2 independent sources |
| Presents a single confident answer | Surfaces contradictions explicitly with labeled positions |
| Accepts the dominant narrative | Asks: *who benefits from this framing? what's being omitted?* |
| Generic keyword queries | Structured query patterns + adversarial reverse-search |

---

## Five Core Behaviors

**1. Recency triage** — Before every search, Claude assesses information shelf life. Political events need same-day sources. Tech trends need 6-month freshness. Historical principles can use training data. No more stale answers dressed up as current.

**2. Domain-specific source routing** — Five source matrices covering: geopolitics (RAND/CFR/Polymarket), tech tools (GitHub stars/Reddit/HN), finance (SEC/regulatory filings), lifestyle (community forums), and AI/academic (arXiv/lab blogs). The right sources for each domain, every time.

**3. Anti-SEO query construction** — Explicitly avoids "best / top / recommended" query patterns. Always appends reverse-search queries (`[topic] problems`, `[topic] criticism`, `[topic] alternatives`) to surface what promotional content hides.

**4. Interest-layer analysis** — For geopolitical and economic topics, Claude is instructed to probe: *Who is saying this? Who benefits? What is being omitted? Are there historical parallels?* Most AI tools answer the surface question. This skill makes Claude answer the deeper one.

**5. Confidence labeling + contradiction surfacing** — High/medium/low confidence labels on every major claim. Contradictory sources are presented side-by-side with their positions labeled, not silently reconciled into false consensus.

---

## Installation

### Claude Code (Recommended)

```bash
# Global install — applies to all your Claude Code sessions
git clone https://github.com/YOUR_USERNAME/smart-search ~/.claude/skills/smart-search

# Project-level install — applies only to current project
git clone https://github.com/YOUR_USERNAME/smart-search .claude/skills/smart-search
```

Claude Code auto-discovers the skill after cloning. No restart needed.

### Claude.ai (Web / Desktop App)

1. Download this repo as a ZIP (GitHub → **Code** → **Download ZIP**)
2. Unzip, then re-zip just the inner `smart-search/` folder
3. Open Claude.ai → **Settings → Features → Custom Skills → Upload**

> Requires Pro, Max, Team, or Enterprise plan.

### Cursor

```bash
cp -r smart-search ~/.cursor/skills/smart-search
```

### Gemini CLI

```bash
cp -r smart-search ~/.gemini/skills/smart-search
```

### OpenAI Codex CLI

```bash
cp -r smart-search ~/.codex/skills/smart-search
```

---

## When It Activates

Claude auto-loads this skill on any request that signals research or information retrieval:

```
"Search for..."            "What's the latest on..."      "Is it true that..."
"Find me a tool for..."    "Compare X vs Y"               "Analyze the situation in..."
"Recommend..."             "Research..."                   "What are people saying about..."
"Look up..."               "What's happening with..."     "Why did X happen?"
```

No slash command needed. It's model-invoked based on context.

---

## Skill Structure

```
smart-search/
├── SKILL.md        ← Instructions Claude loads at runtime
├── README.md       ← English documentation (this file)
├── README.zh.md    ← 中文文档
└── LICENSE         ← Apache 2.0
```

**Inside SKILL.md:**

| Section | Content |
|---|---|
| Step 1 — Pre-search checklist | Recency triage; when to search vs. use training knowledge |
| Step 2 — Source matrix (×5) | Trusted sources by domain: geopolitics, tech, finance, lifestyle, AI/academic |
| Step 3 — Search execution | Query construction patterns; anti-SEO keywords; multi-round rhythm |
| Step 4 — Result processing | Confidence labeling; contradiction handling; information gap declaration |
| Step 5 — Bias check | 6-point pre-output checklist: source diversity, overconfidence, interest-layer analysis |
| Quick reference | Source index table covering all 5 domains |

---

## Compatibility

| Tool | Support |
|---|---|
| Claude Code | ✅ Native — filesystem-based, auto-discovered |
| Claude.ai (Pro / Max / Team / Enterprise) | ✅ Upload via Settings → Features |
| Cursor | ✅ SKILL.md standard |
| Gemini CLI | ✅ SKILL.md standard |
| OpenAI Codex CLI | ✅ SKILL.md standard |
| Antigravity IDE | ✅ SKILL.md standard |
| Claude API | ✅ Via Skills API (`/v1/skills`) |

This skill follows the [Agent Skills open standard](https://agentskills.io) established by Anthropic in December 2025 and adopted by OpenAI for Codex CLI. The same `SKILL.md` file works across all compatible tools.

---

## No Dependencies

- No API keys
- No external services  
- No scripts or executables — pure instruction text
- Fully auditable: the entire skill is readable Markdown

---

## Contributing

Issues and PRs welcome. If you add a new domain-specific source matrix (legal research, medical literature, local language sources, etc.), please open a PR.

---

## License

[Apache 2.0](LICENSE) — free to use, modify, and redistribute. Attribution appreciated but not required.
