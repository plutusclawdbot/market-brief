# BRIEF.md — Daily Market Overview (Stanley Druckenmiller Style)

## Objective
Produce a **complete but succinct** market overview covering:
- What is happening now
- Current market regime
- Regime shifts underway
- Key risks and opportunities
- What to watch next (high-signal triggers)

Write in a **direct, high-conviction, PM-ready** style:
- No fluff
- Prioritize signal over narrative
- Separate facts, interpretation, and positioning implications
- Keep concise, but comprehensive enough for portfolio decisions

---

## Output Format (Required)

### 1) Executive Snapshot (5–10 bullets)
- Most important cross-asset developments in last 24–72h
- One-line "so what" for each

### 2) Market Regime Assessment
- Growth / inflation regime call (e.g., disinflationary slowdown, reacceleration, stag risk)
- Liquidity backdrop (Fed, Treasury issuance, QT/QE proxies, dollar liquidity)
- Volatility regime (suppressed, transitioning, unstable)
- Confidence level: High / Medium / Low

### 3) Cross-Asset Read
Cover these with 2–5 bullets each:
- **Rates** (front-end, long-end, curve, real yields, implied policy path)
- **FX** (USD broad, key crosses, EM stress signals)
- **Equities** (index internals, breadth, leadership, cyclicals vs defensives)
- **Credit** (IG/HY spreads, refinancing stress, defaults)
- **Commodities** (oil, gas, metals; macro implications)
- **Crypto** (if macro-relevant, especially BTC as liquidity/risk proxy)

### 4) Positioning & Flow
- Consensus positioning and crowded trades
- Dealer/gamma/CTA/systematic flow context if available
- Sentiment extremes and squeeze risk

### 5) Regime Shifts / Inflections to Watch
List 5–10 specific shifts:
- What is changing
- Why it matters
- Observable confirmation signal

### 6) Risk Radar
- Top 5 upside risks
- Top 5 downside risks
- Explicit trigger levels/events where possible

### 7) Polymarket Signal Check (Required)
Run this query and summarize notable signal from top markets:

```bash
curl -s "https://gamma-api.polymarket.com/events?active=true&closed=false&limit=200&offset=0&order=volume&ascending=false" \
| jq '[ .[] as $e | ($e.markets // [])[] | { title: (($e.title // "Untitled Event") + " - " + (.question // "Untitled Market")), volume24h: ((.volume24hr // .volume_24h // 0) | tonumber), liquidity: ((.liquidity // 0) | tonumber), slug: $e.slug } ] | sort_by(-.volume24h) | .[:10]'
```

Then provide:
- Top 10 by 24h volume (clean list)
- 3–5 interpretation bullets: what this flow implies about attention/risk narrative
- Flag when market activity is event-driven noise vs durable macro signal

### 8) Actionable Watchlist (Next 1–2 Weeks)
- 10–15 high-signal catalysts (data, central bank, auctions, geopolitics, earnings clusters)
- For each: expected market sensitivity and likely cross-asset reaction map

### 9) Bottom Line (PM Decision Layer)
Provide:
- Base case (55–65%)
- Alternative case (20–30%)
- Tail case (5–15%)
- For each: what to overweight / underweight / hedge

---

## Style Constraints
- Target length: **900–1500 words**
- Crisp, information-dense, no generic textbook explanations
- Prefer bullets over long paragraphs
- Use confidence tags: **[High] [Med] [Low]**
- Mark unverified claims explicitly
- No moralizing/disclaimers unless essential to risk framing

---

## Data Freshness
- Prefer latest available data at runtime
- Timestamp the brief at top as: `Generated: YYYY-MM-DD HH:MM (Europe/London)`
- If data is stale or missing, state gaps explicitly in one short section: `Data Caveats`

---

## Deliverable Naming
- Save final output as: `market-overview-YYYY-MM-DD.md`
- Also print directly in chat for quick read/edit.
