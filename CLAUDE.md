# Career-Ops India -- AI Job Search Pipeline

## Origin

This system is a fork of [career-ops](https://github.com/santifer/career-ops) by [santifer](https://santifer.io), adapted for the Indian job market. The original was built and used to evaluate 740+ job offers and land a Head of Applied AI role.

This fork adapts the archetypes, scoring logic, compensation framework, ghost detection, and portal configuration for jobseekers in India -- targeting product startups, GCCs (Global Capability Centers), and AI-native companies.

**It will work out of the box, but it's designed to be made yours.** If the archetypes don't match your career, the scoring doesn't fit your priorities, or you want to add companies -- just ask. You (AI Agent) can edit the user's files directly. That's the whole point.

---

## Data Contract (CRITICAL)

There are two layers. Read `DATA_CONTRACT.md` for the full list.

**User Layer (NEVER auto-updated, personalization goes HERE):**
- `cv.md`, `config/profile.yml`, `modes/_profile.md`, `article-digest.md`, `portals.yml`
- `data/*`, `reports/*`, `output/*`, `interview-prep/*`

**System Layer (auto-updatable, DON'T put user data here):**
- `modes/_shared.md`, `modes/oferta.md`, all other modes
- `CLAUDE.md`, `*.mjs` scripts, `dashboard/*`, `templates/*`, `batch/*`

**THE RULE: When the user asks to customize anything (archetypes, narrative, negotiation scripts, proof points, location policy, comp targets), ALWAYS write to `modes/_profile.md` or `config/profile.yml`. NEVER edit `modes/_shared.md` for user-specific content.** This ensures system updates don't overwrite their customizations.

---

## Update Check

On the first message of each session, run the update checker silently:

```bash
node update-system.mjs check
```

Parse the JSON output:
- `{"status": "update-available", "local": "1.0.0", "remote": "1.1.0", "changelog": "..."}` → tell the user:
  > "career-ops-india update available (v{local} → v{remote}). Your data (CV, profile, tracker, reports) will NOT be touched. Want me to update?"
  If yes → run `node update-system.mjs apply`. If no → run `node update-system.mjs dismiss`.
- `{"status": "up-to-date"}` → say nothing
- `{"status": "dismissed"}` → say nothing
- `{"status": "offline"}` → say nothing

---

## What is career-ops-india

AI-powered job search pipeline built on Claude Code, calibrated for the Indian market: offer evaluation with India-aware scoring, Ghost Likelihood Score (GLS) for ghost posting detection, ATS-optimized CV generation, portal scanning across Indian job boards, and batch processing.

### Main Files

| File | Function |
|------|----------|
| `data/applications.md` | Application tracker |
| `data/pipeline.md` | Inbox of pending URLs |
| `data/scan-history.tsv` | Scanner dedup + repost detection |
| `portals.yml` | Indian job boards and company config |
| `templates/cv-template.html` | HTML template for CVs |
| `generate-pdf.mjs` | Playwright: HTML to PDF |
| `article-digest.md` | Compact proof points (optional) |
| `interview-prep/story-bank.md` | Accumulated STAR+R stories |
| `interview-prep/{company}-{role}.md` | Company-specific interview intel |
| `analyze-patterns.mjs` | Pattern analysis (JSON output) |
| `followup-cadence.mjs` | Follow-up cadence calculator |
| `data/follow-ups.md` | Follow-up history tracker |
| `reports/` | Evaluation reports (`{###}-{company-slug}-{YYYY-MM-DD}.md`) |

---

## First Run -- Onboarding (IMPORTANT)

**Before doing ANYTHING else, check if the system is set up.** Run these checks silently every session:

1. Does `cv.md` exist?
2. Does `config/profile.yml` exist (not just profile.example.yml)?
3. Does `modes/_profile.md` exist (not just _profile.template.md)?
4. Does `portals.yml` exist (not just templates/portals.example.yml)?

If `modes/_profile.md` is missing, copy from `modes/_profile.template.md` silently.

**If ANY of these is missing, enter onboarding mode.** Do NOT proceed with evaluations or scans until basics are in place.

### Step 1: CV (required)

If `cv.md` is missing, ask:
> "I don't have your CV yet. You can either:
> 1. Paste your CV here and I'll convert it to markdown
> 2. Paste your LinkedIn URL and I'll extract the key info
> 3. Tell me about your experience and I'll draft a CV for you
>
> Which do you prefer?"

Create `cv.md` from whatever they provide. Standard sections: Summary, Experience, Projects, Education, Skills, Certifications.

### Step 2: Profile (required)

If `config/profile.yml` is missing, copy from `config/profile.example.yml` and ask:
> "I need a few details to personalize the system:
> - Your full name and email
> - Your location (city) and whether you're open to relocation
> - What roles are you targeting? (e.g., 'Senior ML Engineer', 'AI Product Manager')
> - Your CTC target range (in LPA)
> - Are you targeting product startups, GCCs, consulting firms, or all three?
>
> I'll set everything up for you."

Fill `config/profile.yml` with their answers. Store archetypes and narrative in `modes/_profile.md`.

### Step 3: Portals (recommended)

If `portals.yml` is missing:
> "I'll set up the job scanner with Indian job boards and 50+ pre-configured companies across product startups, GCCs, and AI-native firms. Want me to customize the search keywords for your target roles?"

Copy `templates/portals.example.yml` → `portals.yml`. Update `title_filter.positive` to match their target roles.

### Step 4: Tracker

If `data/applications.md` doesn't exist, create it:
```markdown
# Applications Tracker

| # | Date | Company | Role | Score | GLS | Status | PDF | Report | Notes |
|---|------|---------|------|-------|-----|--------|-----|--------|-------|
```

Note: GLS = Ghost Likelihood Score (0-100). This column is India-specific.

### Step 5: Get to know the user (critical for quality)

After basics are set up, proactively ask:
> "The basics are ready. The system works much better when it knows you well. Can you tell me:
> - What makes you stand out? What can you do that most candidates can't?
> - What kind of work excites you? What drains you?
> - Any deal-breakers? (e.g., no bond/service agreements, no on-site-only, no startups under Series A)
> - Your best professional achievement -- the one you'd lead with in an interview
> - Are you open to GCC roles, or strictly product startups? Or both?
> - Current notice period?
> - Any published projects, articles, or case studies?
>
> The more context you give me, the better I filter. Think of it as onboarding a recruiter -- the first week I need to learn about you, then I become invaluable."

Store insights in `config/profile.yml` (under narrative) and `modes/_profile.md`. Never put user-specific content in `modes/_shared.md`.

**After every evaluation, learn.** If the user says "this score is too high" or "you missed my experience in X", update `modes/_profile.md` or `config/profile.yml`. The system gets smarter with every interaction.

### Step 6: Ready

Once all files exist, confirm:
> "You're all set! You can now:
> - Paste a job URL or JD to evaluate it
> - Run `/career-ops scan` to search Indian job boards and company pages
> - Run `/career-ops` to see all commands
>
> Everything is customizable -- just ask me to change anything.
>
> Tip: The Ghost Likelihood Score (GLS) is unique to this India fork. It scores each posting 0–100 for ghost job risk, based on reposting patterns, posting age, source quality, and JD signals. A GLS > 50 means investigate before investing time."

---

## Skill Modes

| If the user... | Mode |
|----------------|------|
| Pastes JD or URL | auto-pipeline (evaluate + GLS + report + PDF + tracker) |
| Asks to evaluate offer | `oferta` |
| Asks to compare offers | `ofertas` |
| Wants LinkedIn outreach | `contact` |
| Asks for company research | `deep` |
| Preps for interview | `interview-prep` |
| Wants to generate CV/PDF | `pdf` |
| Evaluates a course/cert | `training` |
| Evaluates portfolio project | `project` |
| Asks about application status | `tracker` |
| Fills out application form | `apply` |
| Searches for new offers | `scan` |
| Processes pending URLs | `pipeline` |
| Batch processes offers | `batch` |
| Asks about rejection patterns | `patterns` |
| Asks about follow-ups | `followup` |

---

## Personalization

This system is designed to be customized by YOU (AI Agent). When the user asks to change archetypes, adjust scoring, add companies, or modify negotiation scripts -- do it directly.

**Common customization requests:**
- "Change the archetypes to data engineering roles" → edit `modes/_profile.md`
- "Add these companies to my portals" → edit `portals.yml`
- "Update my profile" → edit `config/profile.yml`
- "Change the CV template" → edit `templates/cv-template.html`
- "Adjust scoring weights" → edit `modes/_profile.md` for user-specific weights
- "I only want product startup roles" → update `config/profile.yml` sector preference

---

## Ghost Likelihood Score (GLS) -- India-Specific Feature

The GLS is a 0–100 score that estimates the probability that a job posting is a ghost job (filled, fake, or not actively hiring). It is **completely independent of the job fit score (1–5)**. The user decides how much weight to give it.

### GLS Ranges

| Score | Risk Level | Indicator | Recommendation |
|---|---|---|---|
| 0–25 | Low | 🟢 | Apply with confidence |
| 26–50 | Moderate | 🟡 | Proceed, note the flags |
| 51–75 | High | 🟠 | Investigate before investing time |
| 76–100 | Very High | 🔴 | Strong ghost indicators -- verify first |

### GLS Signal Weights

| # | Signal | Max Points | How measured |
|---|---|---|---|
| 1 | Reposting count (scan-history.tsv) | 20 | 3+ reposts in 90 days = 20pts |
| 2 | Posting age | 15 | >60 days = 15pts, 30–60 = 8pts, <30 = 0pts |
| 3 | Apply button inactive/redirect | 15 | Binary: inactive = 15pts |
| 4 | Source quality | 15 | Naukri/Foundit = 15pts, LinkedIn = 5pts, Direct/ATS = 0pts |
| 5 | JD boilerplate ratio | 10 | >70% generic = 10pts, 50–70% = 5pts |
| 6 | Requirements realism | 10 | Contradictions/impossible experience = 10pts |
| 7 | Company layoff/freeze news | 8 | Same dept = 8pts, different dept = 3pts |
| 8 | Consultancy/unnamed client posting | 4 | Flat penalty |
| 9 | Missing specifics (team/stack/location) | 3 | All three missing = 3pts |

### Pre-check (Option C) -- Runs BEFORE full evaluation

Uses only signals 1, 2, 3 (max 50 pts, fast to compute):

```
Pre-check score ≥ 40 → Pause pipeline, warn user:
  "This posting shows ghost job indicators (GLS pre-check: {score}/50).
   Reasons: {list}. Want me to evaluate anyway?"

Pre-check score < 40 → Proceed to full evaluation silently.
```

**In batch mode:** Never pause. Add prominent warning to report header instead.

### Source Quality Reference (India-specific)

| Source | Ghost Risk | GLS Points |
|---|---|---|
| Company careers page (direct) | Low | 0 |
| Greenhouse / Ashby / Lever / Workable | Low | 0 |
| LinkedIn India | Low–Medium | 5 |
| iimjobs / Instahire | Medium | 8 |
| Naukri | Medium–High | 15 |
| Foundit / Monster India | High | 15 |
| Third-party recruiter (named) | Medium | 5 |
| Consultancy / unnamed client | Medium | 4 (flat) |

### India-Specific Ghost Signals

- **"Walkin Interview" postings** -- NOT ghost jobs. Volume hiring. Adjust assessment accordingly.
- **"Our client, a leading MNC..."** -- Flag as "Unverified Company", not Suspicious.
- **Naukri "Actively Hiring" badge** -- Paid feature, not a real-time hiring signal. Do not treat as positive.
- **Same JD across multiple boards, same day** -- Positive signal (real urgency).
- **Staggered reposts weeks apart** -- Negative signal (pipeline building).

---

## CV Source of Truth

- `cv.md` in project root is the canonical CV
- `article-digest.md` has detailed proof points (optional, takes precedence over cv.md for metrics)
- **NEVER hardcode metrics** -- read from these files at evaluation time

---

## Ethical Use -- CRITICAL

**This system is designed for quality, not quantity.**

- **NEVER submit an application without the user reviewing it first.** Fill forms, draft answers, generate PDFs -- but always STOP before clicking Submit/Apply. The user makes the final call.
- **Strongly discourage low-fit applications.** Score below 4.0/5 → explicitly recommend against applying. The user's time and the recruiter's time are both valuable.
- **Quality over speed.** A well-targeted application to 5 companies beats a generic blast to 50.
- **GLS is advisory, not blocking.** A high GLS is a signal, not a veto. The user decides.

---

## Offer Verification -- MANDATORY

**NEVER trust WebSearch/WebFetch alone to verify if an offer is active.** ALWAYS use Playwright:
1. `browser_navigate` to the URL
2. `browser_snapshot` to read content
3. Only footer/navbar without JD = closed. Title + description + Apply button = active.

**Exception for batch workers:** Playwright unavailable in headless pipe mode. Use WebFetch as fallback and mark report header with `**Verification:** unconfirmed (batch mode)`.

---

## Stack and Conventions

- Node.js (mjs modules), Playwright (PDF + scraping), YAML (config), HTML/CSS (template), Markdown (data)
- Output in `output/` (gitignored), Reports in `reports/`
- JDs in `jds/` (referenced as `local:jds/{file}` in pipeline.md)
- Report numbering: sequential 3-digit zero-padded
- **After each batch of evaluations, run `node merge-tracker.mjs`**
- **NEVER create new entries in applications.md if company+role already exists.** Update the existing entry.

### TSV Format for Tracker Additions

Write one TSV file per evaluation to `batch/tracker-additions/{num}-{company-slug}.tsv`. Single line, 10 tab-separated columns (GLS added vs original):

```
{num}\t{date}\t{company}\t{role}\t{status}\t{score}/5\t{gls}/100\t{pdf_emoji}\t[{num}](reports/{num}-{slug}-{date}.md)\t{note}
```

**Column order:**
1. `num` -- sequential number
2. `date` -- YYYY-MM-DD
3. `company` -- short company name
4. `role` -- job title
5. `status` -- canonical status
6. `score` -- format `X.X/5`
7. `gls` -- format `XX/100` with risk emoji (🟢🟡🟠🔴)
8. `pdf` -- ✅ or ❌
9. `report` -- markdown link
10. `notes` -- one-line summary

### Canonical States

| State | When to use |
|-------|-------------|
| `Evaluated` | Report completed, pending decision |
| `Applied` | Application sent |
| `Responded` | Company responded |
| `Interview` | In interview process |
| `Offer` | Offer received |
| `Rejected` | Rejected by company |
| `Discarded` | Discarded by candidate or offer closed |
| `SKIP` | Doesn't fit, don't apply |

### Pipeline Integrity

1. **NEVER edit applications.md to ADD new entries** -- Write TSV and run `merge-tracker.mjs`
2. **YES you can edit applications.md to UPDATE status/notes of existing entries**
3. All reports MUST include `**URL:**` and `**GLS:**` in the header
4. All statuses MUST be canonical
5. Health check: `node verify-pipeline.mjs`
6. Normalize statuses: `node normalize-statuses.mjs`
7. Dedup: `node dedup-tracker.mjs`

---

## Professional Writing & ATS Compatibility

Applies to ALL candidate-facing documents: PDF summaries, bullets, cover letters, form answers.

### Avoid cliché phrases
- "passionate about" / "results-oriented" / "proven track record"
- "leveraged" → use "used" or name the tool
- "spearheaded" → use "led" or "ran"
- "synergies" / "robust" / "seamless" / "cutting-edge"
- "in today's fast-paced world"

### India-specific writing notes
- Avoid "CTC negotiable" in cover letters -- discuss comp in the right context
- Don't mention notice period in CV -- address in cover letter or form only
- For GCC applications: mirror their vocabulary ("CoE", "hub", "centre of excellence") where authentic
- For startup applications: use outcome language ("shipped", "grew", "reduced") over process language

### Prefer specifics over abstractions
- "Reduced model inference latency from 3.2s to 410ms" beats "improved performance"
- "Built RAG pipeline over 50K internal documents, deployed to 200 users" beats "designed scalable AI architecture"
- Name tools, projects, and business impact in INR or % where possible
