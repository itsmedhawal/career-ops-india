# Mode: oferta -- Complete Evaluation A-G

When the candidate pastes an offer (text or URL), ALWAYS deliver all 7 blocks (A–G). Run in this exact order: Pre-checks → Blocks A–G → Post-evaluation.

---

## Pre-check 1 -- Ghost Likelihood Score (Fast Check)

Before any evaluation, run the 3-signal GLS pre-check (signals 1, 2, 3 only -- max 50 pts):

1. Check `data/scan-history.tsv` -- how many times has this company+role appeared in the last 90 days?
2. Extract posting age from Playwright snapshot -- is it under 60 days?
3. Is the apply button active (not redirecting to generic careers page)?

**Scoring:**
- Signal 1: 3+ reposts = 20pts, 2 reposts = 10pts, 0–1 = 0pts
- Signal 2: >60 days = 15pts, 30–60 = 8pts, <30 = 0pts
- Signal 3: Inactive/redirect = 15pts, active = 0pts

**If pre-check score ≥ 40:**
> "This posting shows ghost job indicators (GLS pre-check: {score}/50).
> Signals: {list reasons}.
> Want me to run the full evaluation anyway?"
> 
> If user says yes → proceed. If no → register in tracker as SKIP with GLS noted.

**If pre-check score < 40:** Proceed silently.

---

## Pre-check 2 -- Gate-Pass (CV Match)

Before full scoring, do a rapid CV Match assessment:

1. Read `cv.md` and `article-digest.md`
2. Extract the top 5 hard requirements from the JD
3. Score CV Match on those 5 requirements (1–5)

**If CV Match < 2.5:**
> "CV Match score ({X}/5) is below the gate threshold (2.5).
> The role requirements don't align sufficiently with your background.
> Auto-flagged as SKIP.
> 
> Key gaps: {list top 3 mismatches}
> 
> Want me to run the full evaluation anyway to understand the gaps?"

Still register in tracker with status: `SKIP` and score noted.
Still run full Block G (GLS) -- takes 2 minutes, saves hours on a dead end.

---

## Step 0 -- Archetype Detection

Classify the offer into one of the 7 archetypes (see `_shared.md`). If hybrid, indicate the 2 closest. This determines:
- Which proof points to prioritize in Block B
- How to rewrite the summary in Block E
- Which STAR stories to prepare in Block F
- How to frame the CV in the PDF

---

## Block A -- Role Summary

Table with:

| Field | Value |
|---|---|
| Archetype | {detected -- or hybrid} |
| Domain | platform / agentic / LLMOps / ML / data / consulting / transformation |
| Function | build / consult / manage / deploy / advise |
| Seniority | {level detected} |
| Work Mode | {Full Remote / Remote-First / Hybrid Flexible / Hybrid Structured / WFO / Fake Remote 🚩} |
| Company Stage | {Early Startup / Growth Startup / Late Startup / GCC / Enterprise / Consulting} |
| Location | {city or remote} |
| Notice Period Fit | {compatible / tight / incompatible -- based on profile.yml notice period} |
| Team Size | {if mentioned} |
| GCC Onsite Rotation | {yes / no / not mentioned} |
| TL;DR | {1 sentence -- what this role actually is} |

**Fake Remote flag:** If work mode is classified as "Fake Remote", add a prominent warning:
> 🚩 **Fake Remote Detected:** JD states remote but signals suggest {reason}. Verify before applying.

---

## Block B -- CV Match

Read `cv.md`. Create a table mapping each JD requirement to exact lines from the CV.

**Adapted to archetype:**
- AI/ML Engineer → prioritize model training, experimentation, production deployment proof points
- LLMOps / GenAI → prioritize RAG, evals, observability, pipeline proof points
- Data Scientist → prioritize statistical work, business impact, SQL, A/B testing
- AI PM → prioritize product discovery, PRDs, metrics, cross-functional delivery
- AI Solutions Architect → prioritize system design, integrations, enterprise POCs
- AI Consultant → prioritize client delivery, advisory, project outcomes
- AI Transformation Lead → prioritize change management, adoption metrics, org impact

**CV Match table:**

| JD Requirement | CV Evidence | Strength | Source |
|---|---|---|---|
| {requirement} | {exact line or proof point} | Strong / Very Strong / Moderate / Weak / Gap | cv.md / article-digest.md |

**Gaps section** -- for each gap:
1. Hard blocker or nice-to-have?
2. Can adjacent experience cover it?
3. Is there a portfolio project that addresses it?
4. Concrete mitigation (specific phrase for cover letter, project to mention, framing angle)

---

## Block C -- Level & Strategy

1. **Level detected in JD** vs **candidate's natural level for this archetype** (from cv.md)
2. **"Sell senior without lying" plan:** archetype-specific phrases, concrete achievements to highlight, how to frame career transitions as advantages
3. **"If they downlevel me" plan:** accept if comp is fair + negotiate 6-month review + ask for clear promotion criteria upfront
4. **GCC-specific note** (if applicable): Flag if the role title undersells the actual seniority (e.g. "Senior Analyst" doing Staff Engineer work). Advise on how to negotiate title alongside comp.

---

## Block D -- Comp & Market

**Step 1 -- CTC Research**

Use WebSearch for:
- AmbitionBox: `{company} {role} salary India`
- Glassdoor India: `{company} {role} salary Bangalore / Mumbai / remote`
- Levels.fyi (for MNCs/GCCs): `{company} {role} India`
- LinkedIn Salary (if accessible)
- Blind (for candid comp discussions)

Table with data and cited sources. If no data available, say so -- never invent.

**Step 2 -- Comp Structure Analysis**

| Component | Details | Flag |
|---|---|---|
| Fixed CTC | {amount or range in LPA} | -- |
| Variable % | {%} | Flag if >30% with no floor |
| ESOP / RSU | {details if mentioned} | Flag stage risk if pre-Series B |
| Bond / Service Agreement | {duration if mentioned} | Flag if >6 months |
| Joining Bonus | {amount if mentioned} | Note: one-time, non-recurring |
| In-Hand Estimate | {approx in-hand fixed} | Always compute |

**Step 3 -- Score**

| Assessment | Score |
|---|---|
| CTC band vs user target | {1–5} |
| Comp structure quality | {adjustment} |
| **Final Comp Score** | **{1–5}** |

---

## Block E -- Personalization Plan

Top changes to maximize match for this specific role:

| # | Section | Current State | Proposed Change | Why |
|---|---------|---------------|-----------------|-----|
| 1 | Professional Summary | {current framing} | {proposed reframe with keywords} | {reason} |
| 2–5 | {other sections} | ... | ... | ... |

Top 5 CV changes + Top 5 LinkedIn changes.

**Keyword injection list** (15–20 keywords from JD for ATS):
Extract and list here. These feed directly into the PDF generation step.

---

## Block F -- Interview Plan

6–10 STAR+R stories mapped to JD requirements:

| # | JD Requirement | Story Title | S (Situation) | T (Task) | A (Action) | R (Result) | Reflection |
|---|---|---|---|---|---|---|---|

**Reflection column:** What was learned or what would be done differently. This signals seniority -- junior candidates describe what happened, senior candidates extract lessons.

**Story Bank:** Check `interview-prep/story-bank.md` -- are any of these stories already there? If not, append new ones. Over time this builds a reusable bank of 5–10 master stories adaptable to any interview.

**Archetype framing:**
- AI/ML Engineer → emphasize experimentation rigor, production impact, model metrics
- LLMOps / GenAI → emphasize eval design, production hardening, cost/latency improvements
- Data Scientist → emphasize business impact, stakeholder communication, insight-to-action
- AI PM → emphasize discovery, trade-off decisions, cross-functional alignment
- AI Solutions Architect → emphasize architecture decisions, enterprise integration, POC-to-prod
- AI Consultant → emphasize client outcomes, delivery under constraints, stakeholder management
- AI Transformation Lead → emphasize adoption metrics, org change, executive communication

**Also include:**
- 1 recommended case study -- which portfolio project to present and how to frame it for this role
- 3 likely red-flag questions for this specific company/role + how to answer them honestly
- 1 India-specific question to prepare for: "What is your current CTC and expected CTC?" -- draft a response based on profile.yml comp targets

---

## Block G -- Posting Legitimacy + Full GLS

Run the complete GLS assessment using all 9 signals (see `_shared.md` for weights).

### Signals Assessment

**Signal 1 -- Reposting Pattern** (from scan-history.tsv):
- Check company + similar role title in last 90 days
- Note: how many times, over what period, same URL or different?

**Signal 2 -- Posting Age** (from Playwright snapshot):
- Date posted or "X days ago" -- extract from page
- Apply standard India threshold: >60 days is concerning (not 90 as in Western markets)

**Signal 3 -- Apply Button State** (from Playwright snapshot):
- Active / Closed / Missing / Redirects to generic page

**Signal 4 -- Source Quality:**
- Apply source quality table from _shared.md
- Note: Naukri "Actively Hiring" badge is NOT a positive signal

**Signal 5 -- JD Boilerplate Ratio:**
- Estimate % of JD that is role-specific vs generic filler
- Generic filler: "passionate professional", "fast-paced environment", "team player", etc.

**Signal 6 -- Requirements Realism:**
- Flag impossible combinations: "2 years experience with 5 years required technology"
- Flag contradictions: entry-level title + staff-level responsibilities

**Signal 7 -- Company Hiring Signals** (2–3 WebSearch queries):
- `"{company}" layoffs 2025 OR 2026`
- `"{company}" hiring freeze 2025 OR 2026`
- If found: is it the same department as this role?

**Signal 8 -- Consultancy / Unnamed Client:**
- Is the posting from a recruiter for an unnamed client?
- Flag as "Unverified Company" -- not Suspicious by default

**Signal 9 -- Missing Specifics:**
- Are all three of these absent: team size, tech stack, location?

### GLS Output

```
Ghost Likelihood Score: {X}/100 {emoji}

Signal breakdown:
  +{pts}  {Signal}: {finding}
  +{pts}  {Signal}: {finding}
  ...
  +0      {Signal}: {positive finding -- no points added} ✓

Assessment: {High Confidence / Proceed with Caution / Suspicious}
```

**Context Notes:** Any India-specific caveats:
- Walkin interview → not a ghost, volume hiring
- Unnamed MNC client → unverified, not suspicious
- GCC role open 75 days → normal for senior GCC hiring (longer pipelines)
- Startup with sparse JD → may be genuinely undefined role, not ghost

### Edge Cases
- **Immediate joiner required, posted 45+ days ago** → Strong ghost signal (+10 to GLS)
- **Government / PSU postings** → 90–120 days normal, adjust thresholds
- **No posting date available** → Default to Proceed with Caution, note limited data
- **Recruiter-sourced (no public posting)** → Active recruiter contact is itself a positive signal

---

## Post-evaluation

### 1. Save Report .md

Save to `reports/{###}-{company-slug}-{YYYY-MM-DD}.md`

- `{###}` = next sequential number (3 digits, zero-padded)
- `{company-slug}` = company name lowercase with hyphens
- `{YYYY-MM-DD}` = current date

**Report format:**

```markdown
# Evaluation: {Company} -- {Role}

**Date:** {YYYY-MM-DD}
**Archetype:** {detected}
**Score:** {X.X/5}
**Grade:** {A/B/C/D/F}
**GLS:** {X/100} {🟢/🟡/🟠/🔴}
**URL:** {url}
**Legitimacy:** {High Confidence | Proceed with Caution | Suspicious}
**Work Mode:** {Full Remote / Hybrid / WFO / Fake Remote 🚩}
**Company Stage:** {stage}
**PDF:** {path or pending}
**Verification:** {confirmed (Playwright) | unconfirmed (batch mode)}

---

## A) Role Summary
{full block content}

## B) CV Match
{full block content}

## C) Level & Strategy
{full block content}

## D) Comp & Market
{full block content}

## E) Personalization Plan
{full block content}

## F) Interview Plan
{full block content}

## G) Posting Legitimacy + GLS
{full block content}

## H) Draft Application Answers
{only if score >= 4.5 -- draft answers for the application form}

---

## Extracted Keywords
{15–20 keywords from the JD for ATS optimization}

## India Notes
{Any India-specific flags not covered above: notice period fit, bond terms,
 CTC in-hand estimate, GCC rotation opportunity, referral opportunity detected}
```

### 2. Register in Tracker

Write TSV to `batch/tracker-additions/{num}-{company-slug}.tsv`:

```
{num}\t{date}\t{company}\t{role}\t{status}\t{score}/5\t{gls}/100 {emoji}\t{pdf_emoji}\t[{num}](reports/{num}-{slug}-{date}.md)\t{note}
```

Status on first evaluation: `Evaluated`
PDF emoji: ✅ if auto-pipeline generated PDF, ❌ if pending

### 3. Suggest Next Action

After every evaluation, close with a clear recommendation:

**If score ≥ 4.0 and GLS ≤ 50:**
> "Strong candidate for application. Run `/career-ops pdf` to generate your tailored CV, then `/career-ops apply` to fill the form."

**If score ≥ 4.0 and GLS > 50:**
> "Good fit, but ghost job risk is elevated (GLS: {X}/100). Recommend verifying the role is active before investing time in a full application. Check LinkedIn for a contact at {company} first."

**If score 3.5–3.9:**
> "Borderline fit. Apply only if you have a specific reason (referral, company is a priority target, role is rare). Consider addressing gap: {top gap}."

**If score < 3.5 or SKIP:**
> "Not recommended. {Top reason}. Move on."
