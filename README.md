# career-ops-india

> AI-powered job search pipeline for India -- built on Claude Code. For experienced professionals and students alike.

[![Claude Code](https://img.shields.io/badge/Claude_Code-000?style=flat&logo=anthropic&logoColor=white)](https://claude.ai/code)
[![Node.js](https://img.shields.io/badge/Node.js-339933?style=flat&logo=node.js&logoColor=white)](https://nodejs.org)
[![Go](https://img.shields.io/badge/Go-00ADD8?style=flat&logo=go&logoColor=white)](https://golang.org)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)

---

## Credits

This project is a fork of **[career-ops](https://github.com/santifer/career-ops)** by [Santiago Fernández de Valderrama](https://santifer.io) -- an exceptional piece of work that Santiago built and used to evaluate 740+ job offers and land a Head of Applied AI role. The original architecture, pipeline design, PDF generation, batch processing, and HITL philosophy are entirely his.

This fork adapts career-ops for the **Indian job market**: India-specific archetypes, a Ghost Likelihood Score (GLS) for detecting ghost postings, an India-aware compensation framework (CTC/LPA/ESOP), and a portal scanner configured for Indian job boards and companies.

**If you find this useful, star the original too → [santifer/career-ops](https://github.com/santifer/career-ops)**

---

## What is career-ops-india?

career-ops-india turns Claude Code into an AI-powered job search command center, calibrated for the Indian job market. You bring your CV. The system does the analytical work. You make the decisions.

```
You paste a job URL or description
        │
        ▼
┌─────────────────────┐
│  GLS Pre-check      │  Ghost Likelihood Score -- is this a real opening?
└────────┬────────────┘
         │
┌────────▼────────────┐
│  Gate-Pass Check    │  CV Match ≥ 2.5 required to proceed
└────────┬────────────┘
         │
┌────────▼────────────┐
│  Archetype          │  Classifies: AI/ML / LLMOps / Data Scientist /
│  Detection          │  AI PM / Solutions Architect / Consultant / Transformation
└────────┬────────────┘
         │
┌────────▼────────────┐
│  A-F Evaluation     │  CV match, comp (CTC/LPA), cultural signals,
│  (reads cv.md)      │  work mode, company stage (incl. GCC)
└────────┬────────────┘
         │
    ┌────┼────┐
    ▼    ▼    ▼
 Report  PDF  Tracker
  .md   .pdf   .tsv
                 +GLS
```

**HITL design:** The system evaluates and recommends. You decide and act. Nothing is submitted without your review.

---

## What's Different from the Original

| Feature | Original career-ops | career-ops-india |
|---|---|---|
| Archetypes | 6 (Western AI market) | 7 (India market -- incl. AI Consultant, Data Scientist) |
| Ghost detection | Block G qualitative | **Ghost Likelihood Score (GLS) 0–100** with pre-check |
| Comp framework | USD/EUR market rates | **CTC/LPA, variable %, ESOP risk, bond penalties** |
| Geographic scoring | Remote / Hybrid / Onsite | + **Fake Remote detection** 🚩 |
| Company stage | Startup / Growth / Enterprise | + **GCC as distinct category** |
| Job boards | Western (Greenhouse, Ashby, Lever) | **Indian boards: Naukri, iimjobs, Cutshort, Foundit** |
| Company list | EU/US AI companies | **Indian companies: Razorpay, Sarvam, CRED, Zepto, GCCs** |
| Tracker columns | 9 | 10 (adds GLS column) |
| Intern / Fresher mode | Not present | **Dedicated mode for students and recent graduates** |
| Language | EN / ES / DE / FR / JA | EN (Hindi contributions welcome) |

---

## Ghost Likelihood Score (GLS)

The GLS is the headline feature of this India fork. Ghost job postings -- roles that are filled, fake, or not actively hiring -- are significantly more prevalent on Indian job boards, especially Naukri. A jobseeker can spend hours on an application for a role that was filled 3 months ago.

The GLS scores each posting **0–100** based on 9 signals:

| Score | Risk | What it means |
|---|---|---|
| 0–25 | 🟢 Low | Apply with confidence |
| 26–50 | 🟡 Moderate | Proceed, note the flags |
| 51–75 | 🟠 High | Investigate before investing time |
| 76–100 | 🔴 Very High | Strong ghost indicators -- verify first |

**The GLS is a separate signal from the job fit score.** A role can be a 4.5/5 fit AND have a GLS of 70. You see both and decide. The system never blocks you -- it informs you.

---

## India Archetypes

The system classifies every job into one of 7 archetypes calibrated for the Indian market:

| # | Archetype | Where they hire |
|---|---|---|
| 1 | AI/ML Engineer | Product startups, GCCs |
| 2 | LLMOps / GenAI Engineer | All three sectors |
| 3 | Data Scientist | GCCs, fintech, ecomm |
| 4 | AI Product Manager | Product startups, GCCs |
| 5 | AI Solutions Architect | GCCs, consulting firms |
| 6 | AI Consultant | Big 4, system integrators |
| 7 | AI Transformation Lead | Enterprise, large GCCs |

---

## Quick Start

```bash
# 1. Fork and clone
git clone https://github.com/{your-username}/career-ops-india.git
cd career-ops-india && npm install
npx playwright install chromium

# 2. Configure your profile
cp config/profile.example.yml config/profile.yml
# Edit profile.yml -- name, CTC targets (in LPA), location, target roles

# 3. Add your CV
# Create cv.md in the project root with your CV in markdown

# 4. Set up portals
cp templates/portals.example.yml portals.yml
# Edit portals.yml -- enable/disable companies, set sector focus

# 5. Open Claude Code
claude   # Opens Claude Code in this directory

# 6. Personalize with Claude
# "Update my archetypes to focus on LLMOps and AI PM roles"
# "Set my CTC target to 30-40 LPA"
# "Add these companies to my portals"
```

> **First evaluations won't be perfect.** The system doesn't know you yet. Feed it context -- your CV, proof points, what you're good at, what you want to avoid. The more you give it, the better it filters. Think of it as onboarding a recruiter.

See [USAGE.md](USAGE.md) for step-by-step instructions and workflow guides for both experienced professionals and students. See [docs/SETUP.md](docs/SETUP.md) for the full technical setup guide.

---

## Usage

```bash
/career-ops                → Show all commands
/career-ops {paste a JD}   → Full pipeline (GLS + evaluate + PDF + tracker)
/career-ops intern {URL or JD}  → Internship / fresher evaluation (students and recent grads)
/career-ops scan           → Scan Indian job boards and company pages
/career-ops pdf            → Generate ATS-optimized CV for a role
/career-ops batch          → Batch evaluate multiple offers in parallel
/career-ops tracker        → View application status dashboard
/career-ops apply          → Fill application forms with AI
/career-ops pipeline       → Process pending URLs from inbox
/career-ops contact        → LinkedIn outreach message
/career-ops deep           → Deep company research
/career-ops training       → Evaluate a course or certification
/career-ops patterns       → Analyze rejection patterns
/career-ops followup       → Follow-up cadence tracker
```

Or paste a job URL directly -- career-ops-india auto-detects it and runs the full pipeline.

---

## Pre-configured Indian Companies

The portal scanner comes with **40+ companies** across three segments:

**AI-Native India:** Sarvam AI, Krutrim, Yellow.ai, Haptik, Observe.AI, Mad Street Den, Vernacular.ai

**Product Startups:** Razorpay, CRED, Zepto, Meesho, PhonePe, Groww, Swiggy, Zomato, Freshworks, Postman, BrowserStack, Darwinbox, Hasura

**GCCs:** Google IDC, Microsoft IDC, Walmart Global Tech, JPMorgan India, Goldman Sachs Bangalore, Adobe India, Uber India, Atlassian, PayPal India, Intuit India, SAP Labs, Cisco India

**Job boards searched:** Naukri, LinkedIn India, iimjobs, Cutshort, Foundit, Wellfound, Greenhouse, Ashby, Lever

---

## For Students & Freshers

career-ops-india includes a dedicated mode for internships and entry-level roles -- a gap that the original career-ops does not address. College students in India face a completely different set of challenges than experienced professionals.

```
/career-ops intern {paste a JD or URL}
```

The intern mode has its own evaluation framework:

| Dimension | What it measures |
|---|---|
| Project & Academic Match | Your GitHub projects, coursework, hackathons vs JD requirements |
| Stipend | Market rate for intern/fresher role, city-adjusted, with in-hand estimate |
| PPO Probability | Likelihood of a return offer -- often the real goal of an internship |
| Brand Value | What this company name does for your next opportunity |
| Learning Curve | Will you do real work or fetch data for 3 months? |
| Red Flags | Unpaid, bond agreements, vague scope, commission-only "internships" |

**Platforms covered:** Internshala, LetsIntern, HelloIntern, Unstop, LinkedIn Early Careers, and company-specific programs (Google STEP, Microsoft Engage, Goldman Sachs Analyst, and more).

**Both tracks supported:**
- **On-campus:** Company visiting your college, placement cell involved
- **Off-campus:** Applying directly, no placement cell support

The GLS is calibrated differently for intern roles -- posting age threshold is tighter (45 days vs 60 days) and intern-specific ghost signals are added (unpaid roles, vague JDs, 500+ applicants with no response).

---

## Tech Stack

- **Agent:** Claude Code with custom skill modes
- **PDF:** Playwright/Puppeteer + HTML template (Space Grotesk + DM Sans)
- **Scanner:** Playwright + WebSearch
- **Dashboard:** Go + Bubble Tea (Terminal UI)
- **Data:** Markdown + YAML + TSV

---

## Project Structure

```
career-ops-india/
├── CLAUDE.md                          # Agent instructions (India fork)
├── cv.md                              # Your CV -- create this
├── article-digest.md                  # Your proof points -- optional
├── portals.yml                        # Your portal config -- create from example
├── .claude/
│   └── skills/career-ops/
│       └── modes/
│           ├── _shared.md             # India system context + GLS logic
│           ├── _profile.md            # Your customizations -- create from template
│           ├── _profile.template.md   # India archetype template
│           ├── oferta.md              # India evaluation mode
│           ├── batch-prompt.md        # India batch worker
│           └── ...                    # Other modes (unchanged from original)
├── config/
│   ├── profile.example.yml            # India example -- LPA, IST, sectors
│   └── profile.yml                    # Your profile -- create from example
├── templates/
│   ├── portals.example.yml            # Indian job boards + companies
│   └── cv-template.html               # ATS-optimized CV template
├── dashboard/                         # Go TUI pipeline viewer
├── data/                              # Your tracking data (gitignored)
├── reports/                           # Evaluation reports (gitignored)
└── output/                            # Generated PDFs (gitignored)
```

---

## About This Fork

Built by [Dhawal](https://www.linkedin.com/in/dhawalshrivastava/) -- adapted from the original career-ops for jobseekers navigating the Indian AI job market across product startups, GCCs, and AI-native companies.

Contributions welcome -- especially:
- Additional Indian companies in `portals.example.yml`
- Hindi language modes (`modes/hi/`)
- Improved GLS signal weights based on real data
- Comp band data for Indian roles

---

## License

MIT -- same as the original.

---

## Original Work

**[career-ops](https://github.com/santifer/career-ops)** by Santiago Fernández de Valderrama
> "Built and used to evaluate 740+ job offers, generate 100+ tailored CVs, and land a Head of Applied AI role."

The engine, architecture, and philosophy of this system are entirely Santiago's work. This fork only adapts the context layer for India. If career-ops-india helps your job search, the original deserves your star :)
