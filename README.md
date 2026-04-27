# career-ops-india

> 🌐 **Try the app:** [coi-app.pages.dev](https://coi-app.pages.dev) — score any job in 60 seconds, right in your browser. Zero setup.
>
>  


<img width="2848" height="1472" alt="Gemini_Generated_Image_ld8wb5ld8wb5ld8w" src="https://github.com/user-attachments/assets/8ccae6b8-b62d-4264-ad81-e16baf64f6da" />




> India-adapted CLI fork of [career-ops](https://github.com/santifer/career-ops) by Santiago Fernández de Valderrama.
> Evaluate job offers for the Indian market -- 7 archetypes, Ghost Likelihood Score, CTC/LPA framework, GCC stage, Intern Mode.

---

## Two Ways to Use

| | career-ops-india CLI | Career-Ops-India App |
|---|---|---|
| **Who it's for** | Technical users | Everyone |
| **Setup** | Terminal + Node.js | Browser only -- zero setup |
| **Best for** | Batch scanning, PDF generation, automation | On-the-go evaluation, mobile, pipeline tracking |
| **Install** | `npm install` | Open URL |
| **Link** | This repo | [itsmedhawal.github.io/career-ops-india-app](https://itsmedhawal.github.io/career-ops-india-app) |


**The intended flow:**
CLI discovers and batch-scans roles → App evaluates, scores, and tracks your pipeline on mobile.

---

## What is Different from career-ops

| Feature | career-ops | career-ops-india |
|---------|-----------|-----------------|
| Archetypes | 6 Western roles | 7 India archetypes |
| Comp framework | USD/EUR | CTC/LPA, in-hand estimate, bond penalties |
| Company stages | Startup/Enterprise | + GCC (Global Capability Center) |
| Ghost detection | Qualitative (Block G) | **Ghost Likelihood Score (GLS) 0–100** -- original contribution |
| Work mode | Standard | + Fake Remote detection 🚩 |
| Student support | None | **Intern Mode** -- PPO probability, stipend benchmarks |
| Portal scanner | 73+ global | + Naukri, iimjobs, Cutshort, Foundit, 40 Indian companies |
| Tracker | 9 columns | + GLS column (10 cols) |
| Language | EN | EN (Hindi contributions welcome) |

---

## Ghost Likelihood Score (GLS)

Original contribution -- does not exist in the upstream career-ops repo.

A 0–100 score computed across 9 India-calibrated signals:

| Signal | Points |
|--------|--------|
| Frequent reposting detected | 20 |
| Posting age > 60 days | 15 |
| Apply button inactive | 15 |
| Source: Naukri/Foundit = 15, LinkedIn = 5, ATS = 0 | 15 |
| JD boilerplate ratio > 70% | 10 |
| Impossible requirements combo | 10 |
| Company layoff/hiring freeze news | 8 |
| Unnamed client / unnamed MNC | 4 |
| Missing team + stack + location | 3 |

**Score ranges:** 🟢 0–25 Low · 🟡 26–50 Moderate · 🟠 51–75 High · 🔴 76–100 Very High

GLS is independent of job fit score. You decide how much weight to give it.

---

## India Archetypes

1. AI/ML Engineer
2. LLMOps / GenAI Engineer
3. Data Scientist
4. AI Product Manager
5. AI Solutions Architect
6. AI Consultant
7. AI Transformation Lead

---

## Intern Mode

Triggered via `/career-ops intern`. Original contribution -- does not exist in the upstream repo.

Covers:
- PPO (Pre-Placement Offer) probability assessment
- Brand value scoring
- Stipend benchmarks by city
- On-campus vs off-campus strategy
- Internshala ghost posting signals

---

## Prerequisites

- Node.js 18+
- An Anthropic API key
- Claude Desktop (recommended) or CLI access

---

## Quick Start

```bash
git clone https://github.com/itsmedhawal/career-ops-india
cd career-ops-india
cp config/profile.example.yml config/profile.yml
# Edit profile.yml with your details
```

See [USAGE.md](USAGE.md) for full workflow and [FORK_SETUP.md](FORK_SETUP.md) for setup instructions.

---

## Credits

**Dhawal Shrivastava** -- creator of this fork, Career-Ops-India App, Ghost Likelihood Score (GLS), and Intern Mode.

**Santiago Fernández de Valderrama** -- creator of [career-ops](https://github.com/santifer/career-ops), the engine this fork is based on. Architecture, pipeline, PDF generation, batch processing, and HITL philosophy are his work.

---
## Feedback
This repo hosts community feedback for both the CLI pipeline and [COI-App](https://coi-app.pages.dev). 
Use [Discussions](https://github.com/itsmedhawal/career-ops-india/discussions) to share bug reports, feature requests, or general feedback.

---
## Contribute

Open source under MIT. Contributions welcome:
- 🌐 Hindi language modes
- 🏢 More Indian company data
- 📊 Better GLS signal weights
- 💰 Updated compensation bands

---

*Made with Love and Innovation, driven by Intention, dedicated to the Community.*
*-- [Dhawal Shrivastava](https://www.linkedin.com/in/dhawalshrivastava)*---
