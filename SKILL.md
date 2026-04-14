---
name: smart-search
description: >
  Intelligent search strategy skill. Activates whenever the user needs to search, research,
  find facts, compare options, get recommendations, or analyze current events. Prevents
  over-reliance on the model's stale training data by enforcing source-diversity, recency
  checks, and anti-SEO filtering. Trigger keywords: search, find, recommend, latest, current,
  analyze, compare, what's the best, research, is it true, look up.
license: Apache 2.0
---

# Smart Search Strategy Skill

## Core Philosophy

The goal of search is not just to find *an* answer — it's to find the **most credible, closest-to-truth** information available. For topics involving national interests, capital incentives, or political agendas, actively surface the underlying logic beneath the surface narrative.

---

## Step 1 — Pre-Search Checklist (Run Before Every Search)

### 1.1 Recency Assessment

| Information Type | Shelf Life | Strategy |
|---|---|---|
| Political events, market prices, product launches | < 1 month | **Must** search in real time — training data is stale |
| Policy direction, company strategy, tech trends | < 6 months | Search and verify; check publication dates |
| Historical events, foundational principles, institutional structures | Years | Training knowledge acceptable; selective verification |

### 1.2 Topic Classification → Jump to Corresponding Source Matrix (Section 2)

- Geopolitics / economics / international affairs → 2.1
- Tech tools / software / open-source → 2.2
- Investment / finance / markets → 2.3
- Lifestyle / consumer / health / local → 2.4
- Frontier tech / AI / academic → 2.5

---

## Step 2 — Source Matrix by Domain

### 2.1 🌍 Geopolitics / Macroeconomics / International Trade

**Primary Sources** (highest credibility)
- Government websites, central bank announcements, international org original texts (UN / WTO / IMF / BIS / OECD)
- Corporate filings, regulatory disclosures (SEC, stock exchange announcements)

**Expert Analysis Layer**
- Western think tanks: RAND / CSIS / Brookings / PIIE / CFR / Chatham House
- Asia-Pacific perspective: ISEAS Singapore, Tokyo Foundation, East Asia Forum
- Independent economists: Follow their X/Twitter accounts; always note their background and potential conflicts of interest

**Real-Time Verification**
- Prediction markets: Polymarket / Kalshi / Metaculus (use as crowd confidence signal, not authority)
- Reuters / FT / Bloomberg: News layer — reliable for facts, less so for interpretation

**Counter-Narrative Check (Critical Step)**
- For any topic involving state or capital interests, always ask: **Who is saying this? Who benefits? Who is being silenced?**
- For any major geopolitical event, find at least one non-Western source for comparison (e.g., Al Jazeera, Caixin, South China Morning Post, The Hindu)
- Distinguish clearly: official position vs. academic research vs. market expectations vs. public sentiment

### 2.2 💻 Tech Tools / Software Recommendations / Open-Source Ecosystem

**Core Principle: Avoid SEO Content Farms**

**Priority Sources**
- **GitHub**: Star count + recent commit activity + issue quality (active issues = real users)
- **Reddit**: Domain-specific subreddits (r/MacApps / r/selfhosted / r/homelab / r/linux / r/programming) — read *actual user threads*, not pinned promotions
- **Hacker News**: Search `site:news.ycombinator.com [product name]` for candid community reactions
- **alternativeto.net**: Side-by-side comparison of similar tools

**Developer Blogs** (personal blogs > media review sites)
- Search: `[tool name] review site:dev.to` or `[tool name] honest experience`

**Reverse Validation (Always Do This)**
- Also search: `[product] problems` / `[product] alternatives` / `[product] reddit`
- Any article titled "Best X in [Year]" with no concrete test data → **downrank immediately**

**Open-Source Discovery Logic**
- Free/open-source tools are rarely SEO-optimized; they spread by word of mouth
- Add `open source` / `free` / `GitHub` keywords to surface tools that don't buy ads

### 2.3 💰 Investment / Finance / Markets

**Primary Data** (the only reliable foundation)
- US: SEC filings (EDGAR), Fed statements, BLS/BEA data
- EU: ECB, Eurostat, ESMA disclosures
- China: CSRC regulatory filings, PBOC, NBS official data
- Global: Bloomberg / Reuters data citations, IMF World Economic Outlook

**Analysis Layer** (note conflicts of interest)
- Sell-side research has client-retention incentives — maintain healthy skepticism
- Independent analysts: useful signal, but always note their disclosed positions

**Must Flag**
- Content containing "price target," "strong buy," or "guaranteed returns" — trace back to the original research document
- Social media market sentiment ≠ fundamentals — treat separately
- Capital narrative recognition: which type of capital benefits from this policy/event? Who is promoting this framing?

### 2.4 🏠 Lifestyle / Consumer / Health / Local

**Prioritize Authentic User Feedback**
- Reddit (relevant subreddits for any topic)
- Product-specific forums and communities
- Review aggregators with verified purchase filters (not paid placement)
- Local community boards and city-specific subreddits for local questions

**Recency Check**
- Consumer products: verify model year/version (2023 recommendations may be superseded)
- Policy-related topics (visa, tax, benefits): always check for the latest version

**Localization Strategy**
- For region-specific questions, search in the local language first — don't just translate English answers
- Add location + time qualifiers to avoid generic responses

### 2.5 🔬 Frontier Tech / AI / Academic

**Primary Sources**
- arXiv preprints (note: not peer-reviewed — assess accordingly)
- Official GitHub repos (README + Release Notes are often more accurate than media coverage)
- Research lab blogs: DeepMind / OpenAI / Anthropic / Google Research / Meta AI

**First-Hand Signal Layer** (researchers > media)
- Researcher X/Twitter accounts for immediate interpretation (before media rewrites)
- Tech media (The Verge / Ars Technica / MIT Tech Review) as supplement, not authority

**Version Awareness**
- Always confirm: paper/model/tool version number and publication date
- In AI, content from 6 months ago may already be obsolete

---

## Step 3 — Search Execution Standards

### 3.1 Query Construction

```
❌ Avoid: best / top / amazing / recommended / ultimate (SEO trap words)
✅ Use:   specific function + context + time qualifier

# Source-scoped queries
site:reddit.com [question]
site:github.com [tool name]

# Time-scoped queries
[topic] after:2024
[topic] 2025

# Reverse search (always run at least one)
[product/policy/event] problems
[product/policy/event] criticism
[product/policy/event] alternatives
[product/policy/event] debunked
```

### 3.2 Multi-Round Search Rhythm

1. **Round 1 — Wide**: Broad query to map the topic landscape; identify key names, institutions, terminology
2. **Round 2 — Deep**: Drill into specific entities surfaced in Round 1; find original/primary sources
3. **Round 3 — Adversarial** (when contradictions exist): Specifically search for opposing views, criticism, alternative interpretations

### 3.3 Underlying Logic Excavation (Required for Interest-Conflict Topics)

For political, economic, and policy questions, actively surface:

```
① Who is making this claim? (Government / media / capital / academic / grassroots)
② Who benefits from this narrative? Whose interests are protected or harmed?
③ What information is being deliberately omitted or downplayed?
④ Are there historical parallels? What were the outcomes?
⑤ Surface cause vs. deep driver (economic structure / power logic / historical grievances)
```

---

## Step 4 — Result Processing Standards

### 4.1 Confidence Labeling

- **High**: Multiple independent sources agree; primary data supports the claim
- **Medium**: Single reliable source, or multiple sources with divergence
- **Low**: Inference / indirect information / single secondary source

### 4.2 Handling Contradictory Information

- **Do not force a single conclusion** — explicitly surface the disagreement:
  > "Source A states… Source B states… The key point of divergence is…"
- Label the nature and likely bias of each source

### 4.3 Information Gap Declaration

- Explicitly tell the user which questions the current search cannot confirm
- Distinguish between "no public information available" and "information exists but contradicts itself"

---

## Step 5 — Pre-Output Bias Check

```
[ ] Did I only cite sources from one language/cultural sphere?
    (Geopolitical topics require at least one non-dominant-perspective source)
[ ] Are there commercially-incentivized sources mixed in without flagging?
[ ] Is the time reference explicit? ("Latest" = how recent exactly?)
[ ] Am I overconfident in the conclusion? Is confidence level labeled?
[ ] Did I probe the underlying interest logic?
    (Required for political / economic / capital topics)
[ ] Did I miss niche but high-quality sources?
    (Open-source tools / independent researchers often don't rank well in SEO)
```

---

## Quick Reference: Source Index

| Category | Sources |
|---|---|
| Geopolitical think tanks | RAND / CSIS / CFR / Brookings / Chatham House / ISEAS |
| Prediction markets | Polymarket / Kalshi / Metaculus |
| Open-source communities | GitHub / Hacker News / alternativeto.net |
| Tech communities | r/MacApps / r/selfhosted / r/homelab / r/programming |
| International finance | FT / Bloomberg / Reuters / WSJ / The Economist |
| AI frontier | arXiv / HuggingFace / DeepMind blog / OpenAI blog |
| Preprints | arXiv / SSRN / bioRxiv |
| Local/consumer | Reddit (domain subreddits) / community forums |
