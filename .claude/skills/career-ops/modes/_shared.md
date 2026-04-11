# System Context -- career-ops-india

<!-- ============================================================
     THIS FILE IS AUTO-UPDATABLE. Don't put personal data here.
     
     Your customizations go in modes/_profile.md (never auto-updated).
     This file contains system rules, scoring logic, archetype
     definitions, and India-specific market context.
     
     Read order: _shared.md first → _profile.md overrides.
     ============================================================ -->

## Sources of Truth

| File | Path | When |
|------|------|------|
| cv.md | `cv.md` (project root) | ALWAYS |
| article-digest.md | `article-digest.md` (if exists) | ALWAYS -- detailed proof points |
| profile.yml | `config/profile.yml` | ALWAYS -- candidate identity and targets |
| _profile.md | `modes/_profile.md` | ALWAYS -- user archetypes, narrative, negotiation |

**RULE: NEVER hardcode metrics from proof points.** Read from cv.md + article-digest.md at evaluation time.
**RULE: article-digest.md takes precedence over cv.md for project metrics.**
**RULE: Read _profile.md AFTER this file. User customizations in _profile.md override defaults here.**

---

## Archetype Detection

Classify every offer into one of these 7 archetypes (or hybrid of 2). Detection is based on JD signals -- independent of the user's background.

| # | Archetype | Key Signals in JD | Primary Hiring Context |
|---|---|---|---|
| 1 | **AI/ML Engineer** | "model training", "inference", "fine-tuning", "PyTorch", "MLflow", "feature engineering", "experimentation" | Product startups, GCCs |
| 2 | **LLMOps / GenAI Engineer** | "LLM", "RAG", "prompt engineering", "evals", "observability", "LangChain", "vector database", "GenAI pipeline" | All three sectors |
| 3 | **Data Scientist** | "statistical modeling", "A/B testing", "business insights", "SQL", "analytics", "forecasting", "dashboards" | GCCs, fintech, ecomm |
| 4 | **AI Product Manager** | "PRD", "roadmap", "product discovery", "stakeholder", "OKRs", "GTM", "user research", "AI product" | Product startups, GCCs |
| 5 | **AI Solutions Architect** | "architecture", "enterprise", "integration", "system design", "pre-sales", "POC", "technical proposal" | GCCs, consulting firms |
| 6 | **AI Consultant** | "client engagement", "advisory", "consulting", "project delivery", "change management", "Big 4", "practice" | Big 4, system integrators |
| 7 | **AI Transformation Lead** | "digital transformation", "AI adoption", "CoE", "enablement", "org change", "head of AI", "AI strategy" | Enterprise, large GCCs |

**Hybrid detection:** If a JD has strong signals from 2 archetypes, indicate both (e.g. "LLMOps / GenAI Engineer + AI Solutions Architect"). Adapt framing to the dominant one.

**After detecting archetype:** Read `modes/_profile.md` for the user's specific framing and proof points for that archetype.

---

## Scoring System

### Gate-Pass Check (runs BEFORE full scoring)

**CV Match is a hard gate.** If CV Match score < 2.5, the evaluation stops and the offer is auto-flagged as SKIP -- regardless of all other dimensions.

```
CV Match < 2.5 → AUTO-SKIP
  Output: "CV Match score ({X}/5) is below the gate threshold (2.5).
           The role requirements don't align sufficiently with your
           background to justify a full evaluation. Flagged as SKIP."
  Still register in tracker with status: SKIP
  Still run Block G (Ghost Likelihood Score) -- takes 2 minutes, saves hours
```

**Why this matters for India:** The Indian job market has high application volumes. Recruiters discard weak matches immediately. A well-targeted 4.0+ application beats five 2.5 applications every time.

### 5 Scoring Dimensions

| Dimension | What it measures | Weight |
|---|---|---|
| **CV Match** | Skills, experience, proof points alignment with JD requirements | Gate-pass + High |
| **North Star Alignment** | How well the role fits the user's target archetypes (from _profile.md) | High |
| **Compensation** | CTC band vs market + comp structure quality (fixed/variable/ESOP) | High |
| **Cultural & Market Signals** | Company culture, growth stage, GCC vs startup, remote policy, team signals | Medium |
| **Red Flags** | Blockers, warnings -- negative adjustments to global score | Variable |

### Score Interpretation

| Score | Grade | Recommendation |
|---|---|---|
| 4.5–5.0 | A | Strong match -- apply immediately |
| 4.0–4.4 | B | Good match -- worth applying |
| 3.5–3.9 | C | Decent but not ideal -- apply only if specific reason |
| 3.0–3.4 | D | Weak match -- recommend against |
| < 3.0 | F | Do not apply |

**System strongly discourages applying below 4.0.** The Indian job market rewards specificity -- a 4.5 application to the right role beats ten 3.5 applications every time.

### Compensation Dimension -- India-Aware Scoring

Score comp 1–5 based on the full picture, not just base salary:

**Step 1 -- CTC Band Assessment**
- Does the stated/researched CTC match the user's target range (from profile.yml, in LPA)?
- 5 = top quartile for role+level+city, 4 = above market, 3 = median, 2 = below, 1 = well below

**Step 2 -- Comp Structure Quality**
Adjust the band score based on structure:

| Structure Signal | Adjustment |
|---|---|
| High variable % (>30%) with no floor guarantee | −0.3 |
| ESOP/RSU at early-stage startup (pre-Series B) | Note as high-risk, no automatic penalty |
| ESOP/RSU at late-stage / listed company | +0.2 |
| Bond / service agreement (1yr+) | −0.3 |
| Joining bonus (one-time) | Note as non-recurring, don't inflate score |
| No comp mentioned anywhere | −0.2 |
| Retention bonus with cliff | Note cliff date, no automatic penalty |

**Step 3 -- CTC vs In-Hand Reality**
Flag if CTC includes components that significantly inflate the headline number:
- High variable (>30%) inflates CTC
- PF/gratuity/insurance bundled into CTC
- Reimbursements included in CTC

Always note: "Stated CTC of X LPA likely translates to approximately Y LPA in-hand fixed."

**WebSearch for comp data:** Use Glassdoor India, AmbitionBox, Levels.fyi (for MNCs/GCCs), LinkedIn Salary, and Blind. Cite sources. If no data, say so -- never invent.

### Geographic Dimension -- Remote / Hybrid / WFO

This is NOT a standalone scoring dimension -- it feeds into Cultural & Market Signals. But it gets **explicit, prominent treatment** in Block A and the report header because it directly affects the user's daily life.

**Classify every role into one of these:**

| Classification | Definition |
|---|---|
| **Full Remote** | No office requirement, async-first, any location |
| **Remote-First** | Primarily remote, occasional travel (1–2x/year) |
| **Hybrid -- Flexible** | 1–2 days/week in office, employee chooses days |
| **Hybrid -- Structured** | 3+ days/week in office, company mandates days |
| **WFO** | Full-time in office, 4–5 days/week |
| **Fake Remote** | JD says remote but signals indicate otherwise (see below) |

**Fake Remote Detection -- India-specific:**
Flag as "Fake Remote 🚩" if ANY of these signals appear:
- "Remote within Bangalore / Mumbai / Pune" (city-restricted remote)
- "Work from home with occasional office visits" but office visits are weekly
- Remote role but requires relocation to HQ city within 6 months
- "Hybrid" defined as 3–4 days in office (this is effectively WFO)
- Job posted on Naukri with "Work From Home" tag but JD mentions daily standups in IST morning that imply physical presence

**Score impact:**
- Full Remote / Remote-First: no penalty
- Hybrid Flexible: no penalty
- Hybrid Structured: −0.2 if user prefers remote (read from profile.yml)
- WFO: −0.4 if user prefers remote
- Fake Remote: −0.5 + mandatory flag in report

### Company Stage -- India-Specific Categories

| Stage | Definition | Career Implications |
|---|---|---|
| **Early Startup** | Pre-Series A, <50 employees | High risk, high upside, equity matters, role undefined |
| **Growth Startup** | Series A–C, 50–500 employees | Best learning curve, equity meaningful, some process |
| **Late Startup / Pre-IPO** | Series D+, 500–2000 employees | Lower risk, equity still relevant, more corporate |
| **GCC** | Global Capability Center of an MNC | Stable comp, slower growth, onsite rotation possible, visa optionality |
| **Enterprise / Listed** | Large Indian or MNC enterprise | Most stable, slowest growth, RSUs over ESOPs |
| **Consulting / SI** | Big 4, system integrators, boutique | Project-based, client exposure, travel, variable comp |

**GCC-specific scoring notes:**
- GCC roles often have strong comp but limited equity -- don't penalize for no ESOP
- "Onsite rotation" (travel to parent company HQ) is a positive signal for growth-oriented candidates -- flag it explicitly
- GCC titles often lag market vocabulary ("Senior Analyst" = what a startup calls "ML Engineer") -- detect and flag title inflation/deflation
- Stability score is higher for GCCs -- relevant for candidates with dependents or EMIs

### Red Flags -- Automatic Penalties

| Red Flag | Score Adjustment | Notes |
|---|---|---|
| Bond / service agreement > 6 months | −0.5 | Hard flag, user must acknowledge |
| "Startup equity" with no vesting schedule mentioned | −0.2 | Flag for clarification |
| Role title mismatches seniority in JD | −0.2 | e.g. "Associate" title but "8+ years required" |
| >3 rounds of interviews mentioned | −0.1 | Process signal, not a blocker |
| No response SLA mentioned for applications | Neutral | Common in India, not a flag |
| JD last updated >90 days ago | −0.3 | Combine with GLS |
| Company has active PIP/layoff news | −0.4 | Cite source |
| Requires immediate joiner but notice period incompatible | Flag only | Don't penalize -- let user decide |
| "Startup salary" explicitly mentioned | −0.3 | Code for below-market comp |

---

## Ghost Likelihood Score (GLS)

The GLS (0–100) is a **separate signal** from the job fit score. It estimates the probability that a posting is a ghost job. The user decides how much weight to give it.

### GLS Ranges

| Score | Risk | Indicator |
|---|---|---|
| 0–25 | Low | 🟢 Apply with confidence |
| 26–50 | Moderate | 🟡 Proceed, note the flags |
| 51–75 | High | 🟠 Investigate before investing time |
| 76–100 | Very High | 🔴 Strong ghost indicators -- verify first |

### Signal Weights

| # | Signal | Max Pts | How measured |
|---|---|---|---|
| 1 | Reposting count (scan-history.tsv) | 20 | 3+ reposts in 90 days = 20pts, 2 reposts = 10pts |
| 2 | Posting age | 15 | >60 days = 15pts, 30–60 = 8pts, <30 = 0pts |
| 3 | Apply button inactive / redirect | 15 | Binary: inactive = 15pts |
| 4 | Source quality | 15 | See source table below |
| 5 | JD boilerplate ratio | 10 | >70% generic = 10pts, 50–70% = 5pts |
| 6 | Requirements realism | 10 | Impossible combos / contradictions = 10pts |
| 7 | Company layoff / freeze news | 8 | Same dept = 8pts, different dept = 3pts |
| 8 | Consultancy / unnamed client | 4 | Flat penalty |
| 9 | Missing specifics (team + stack + location all absent) | 3 | All three missing = 3pts |

### Source Quality Table

| Source | Ghost Risk | GLS Points |
|---|---|---|
| Company careers page (direct) | Low | 0 |
| Greenhouse / Ashby / Lever / Workable | Low | 0 |
| LinkedIn India | Low–Medium | 5 |
| iimjobs / Instahire / Cutshort | Medium | 8 |
| Naukri | Medium–High | 15 |
| Foundit / Monster India | High | 15 |
| Third-party recruiter (named agency) | Medium | 5 |
| Consultancy / unnamed client | Medium | 4 (flat, signal 8) |

### India-Specific Ghost Signals

- **"Walkin Interview"** -- NOT a ghost job. Volume / ops hiring. Adjust assessment.
- **"Our client, a leading MNC in BFSI / IT / Manufacturing..."** -- Flag as "Unverified Company". Not Suspicious by default.
- **Naukri "Actively Hiring" badge** -- Paid feature. Not a real-time hiring signal.
- **Same JD across multiple boards on the same day** -- Positive signal (real urgency).
- **Staggered reposts weeks apart across boards** -- Negative signal (pipeline building).
- **Requirement for "immediate joiner"** posted 45+ days ago -- Strong ghost indicator.

### Pre-check (runs BEFORE full evaluation)

Uses only signals 1, 2, 3 (max 50 pts):

- Pre-check score ≥ 40 → Pause, warn user (skip pause in batch mode -- add header warning instead)
- Pre-check score < 40 → Proceed silently

---

## Global Rules

### NEVER

1. Invent experience, metrics, or skills
2. Modify cv.md, article-digest.md, or portfolio files
3. Submit or click Apply on behalf of the candidate
4. Share phone number in generated messages or cover letters
5. Recommend comp below market rate
6. Generate a PDF without reading the JD first
7. Use corporate-speak in candidate-facing documents
8. Ignore the tracker -- every evaluated offer gets registered
9. Present ghost job signals as accusations -- always present as observations

### ALWAYS

0. **Cover letter:** If the form allows it, ALWAYS include one. Same visual design as CV. JD language mapped to proof points. 1 page max.
1. Read cv.md, _profile.md, and article-digest.md (if exists) before evaluating
2. Run gate-pass check (CV Match) before full evaluation
3. Detect the role archetype and adapt framing per _profile.md
4. Cite exact lines from CV when matching requirements
5. Use WebSearch for comp data (AmbitionBox, Glassdoor India, Levels.fyi) and company news
6. Run GLS pre-check before full evaluation
7. Register in tracker after every evaluation
8. Generate content in the language of the JD (English default)
9. Be direct and actionable -- no fluff
10. **Tracker additions as TSV** -- NEVER edit applications.md directly

### Tools

| Tool | Use |
|------|-----|
| WebSearch | Comp research (AmbitionBox, Glassdoor India, Levels.fyi), company news, LinkedIn contacts, layoff/freeze news |
| WebFetch | Fallback for extracting JDs from static pages |
| Playwright | Verify offers (browser_navigate + browser_snapshot). **NEVER 2+ agents with Playwright in parallel.** |
| Read | cv.md, _profile.md, article-digest.md, cv-template.html |
| Write | Temporary HTML for PDF, reports .md, tracker TSV |
| Bash | `node generate-pdf.mjs`, `node merge-tracker.mjs`, `node verify-pipeline.mjs` |

---

## India Market Context (read before every evaluation)

This context informs scoring calibration. Do not output it in reports -- use it internally.

**Notice periods:** 60–90 days is standard in India. 30 days is increasingly common at startups. "Immediate joiner" requirements should be flagged -- they narrow the candidate pool and are often not a hard requirement despite what the JD says.

**Title standardization:** Indian job titles are less standardized than Western markets.
- GCC "Senior Analyst" often = "ML Engineer" at a startup
- "Associate Consultant" at Big 4 often = "AI Engineer" at a product company
- Always interpret title in context of responsibilities, not just the title string

**Referral culture:** Cold applications convert at lower rates in India than in Western markets. Where Block F recommends outreach, prioritize LinkedIn connections at the company over cold applications.

**Remote reality:** India's remote work culture is uneven. GCCs are predominantly hybrid or WFO. Product startups vary widely. Explicitly flag any discrepancy between stated and actual work mode.

**Comp transparency:** Many Indian job postings omit salary ranges. This is normal and not a ghost signal by itself. Use AmbitionBox and Glassdoor India to fill the gap.

**GCC onsite rotation:** Many GCC roles offer periodic travel to the parent company's HQ (US, UK, Europe). This is a meaningful career perk for many candidates -- always mention when detected in JD.
