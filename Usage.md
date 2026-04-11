# How to Use career-ops-india

Quick reference guide for getting started and using every mode.
Two sections -- jump to yours:

- [For Experienced Professionals](#for-experienced-professionals)
- [For Students and Freshers](#for-students-and-freshers)

---

## For Experienced Professionals

### Workflow

```
┌─────────────────────────────────────────────────────┐
│                    FIRST TIME?                      │
│                                                     │
│  1. Add your CV         →  cv.md                   │
│  2. Fill your profile   →  config/profile.yml       │
│  3. Set your portals    →  portals.yml              │
│  4. Open Claude Code    →  claude                   │
└──────────────────────┬──────────────────────────────┘
                       │
                       ▼
┌─────────────────────────────────────────────────────┐
│                 DAILY WORKFLOW                      │
│                                                     │
│  Option A: You found a job                          │
│  Paste URL or JD → auto-pipeline runs               │
│                                                     │
│  Option B: Discover new jobs                        │
│  /career-ops scan → reviews 40+ companies           │
│                                                     │
│  Option C: Process a batch                          │
│  Add URLs to pipeline.md → /career-ops pipeline     │
└──────────────────────┬──────────────────────────────┘
                       │
                       ▼
┌─────────────────────────────────────────────────────┐
│                WHAT YOU GET                         │
│                                                     │
│  Report (.md)   Score + GLS + gaps + STAR stories   │
│  PDF            ATS-optimized CV for this role      │
│  Tracker entry  Auto-logged in applications.md      │
└──────────────────────┬──────────────────────────────┘
                       │
                       ▼
┌─────────────────────────────────────────────────────┐
│                 YOU DECIDE                          │
│                                                     │
│  Score >= 4.0 + GLS <= 50  →  Apply                │
│  Score >= 4.0 + GLS > 50   →  Verify first         │
│  Score 3.5-3.9             →  Your call             │
│  Score < 3.5               →  Skip                 │
└─────────────────────────────────────────────────────┘
```

---

### Reading Your Report

Every report has 7 blocks and two scores:

**The job fit score (1-5):** How well this role matches your CV, target archetype, and comp expectations.

**The Ghost Likelihood Score (0-100):** How likely this posting is a ghost job. Independent of fit score -- you decide how much weight to give it.

```
Score 4.2 / 5   +   GLS 38/100 🟡   =   Good fit, moderate ghost risk
                                         Verify the role is active, then apply

Score 4.5 / 5   +   GLS 72/100 🟠   =   Great fit, high ghost risk
                                         Check company careers page directly first

Score 3.2 / 5   +   GLS 15/100 🟢   =   Poor fit, real posting
                                         Skip -- the role is real but not for you
```

---

### Key Commands

| What you want to do | Command |
|---|---|
| Evaluate a job | Paste URL or JD directly |
| Find new jobs | `/career-ops scan` |
| Generate tailored CV | `/career-ops pdf` |
| Fill application form | `/career-ops apply` |
| Research a company | `/career-ops deep` |
| Check your pipeline | `/career-ops tracker` |
| Process pending URLs | `/career-ops pipeline` |
| Prep for an interview | `/career-ops interview-prep` |
| Evaluate a course/cert | `/career-ops training` |
| Analyse rejection patterns | `/career-ops patterns` |

---

### Personalisation Tips

The system gets smarter the more context you give it. After your first few evaluations, tell Claude:

- "This score is too high -- I wouldn't apply here because {reason}" -- it will recalibrate
- "You missed that I have experience in {X}" -- it will update your profile
- "I only want roles at product startups, not GCCs" -- it will adjust scoring
- "Add {company} to my portal scan" -- it will update portals.yml

All updates go to `modes/_profile.md` and `config/profile.yml` -- never to the system files.

---

### Common Mistakes to Avoid

- **Skipping cv.md setup** -- the system cannot evaluate fit without your CV. First evaluation will be generic.
- **Not setting CTC targets** -- the comp dimension scores against your target in profile.yml. Without it, comp scoring is meaningless.
- **Ignoring GLS** -- a 4.5/5 role with GLS 80 has wasted many applicants' time on Naukri. Always check.
- **Applying below 4.0** -- the system discourages this for good reason. High-volume, low-fit applications hurt your response rate over time.
- **Not reviewing before submitting** -- the system fills forms and generates PDFs but never submits. You always have the final call.

---

## For Students and Freshers

### Workflow

```
┌─────────────────────────────────────────────────────┐
│                    FIRST TIME?                      │
│                                                     │
│  1. Add your CV         →  cv.md                   │
│     (projects, courses, hackathons, CGPA)           │
│  2. Fill your profile   →  config/profile.yml       │
│     (target roles, stipend expectations, city)      │
│  3. Open Claude Code    →  claude                   │
└──────────────────────┬──────────────────────────────┘
                       │
                       ▼
┌─────────────────────────────────────────────────────┐
│                 FIND AN INTERNSHIP                  │
│                                                     │
│  Option A: You found one                           │
│  /career-ops intern {URL or paste JD}               │
│                                                     │
│  Option B: Discover opportunities                   │
│  /career-ops scan → checks Internshala,             │
│  Unstop, LinkedIn Early Careers + company pages     │
└──────────────────────┬──────────────────────────────┘
                       │
                       ▼
┌─────────────────────────────────────────────────────┐
│                WHAT YOU GET                         │
│                                                     │
│  Project Match     How your projects map to the JD  │
│  Stipend score     Is this fair for the role/city?  │
│  PPO probability   Likelihood of a return offer     │
│  Brand value       What this name does for you next │
│  Learning curve    Will you do real work here?      │
│  Red flags         Unpaid? Bond? Vague scope?       │
│  GLS               Is this even a real posting?     │
└──────────────────────┬──────────────────────────────┘
                       │
                       ▼
┌─────────────────────────────────────────────────────┐
│                 YOU DECIDE                          │
│                                                     │
│  Score >= 4.0   →  Apply -- intern roles close fast │
│  Score 3.5-3.9  →  Apply if brand/learning is high  │
│  Score < 3.5    →  Skip or build the missing skill  │
│  Unpaid flag    →  Verify before investing time      │
└─────────────────────────────────────────────────────┘
```

---

### What to Put in cv.md When You Have No Work Experience

This is the most common question from students. Your proof points are different, not absent.

```
INSTEAD OF:                    USE:
"No work experience"     →     Projects with outcomes
"Did a college project"  →     "Built X that does Y, used by Z people"
"Studied machine learning" →   "Completed Andrew Ng's ML course +
                                built a sentiment classifier (87% accuracy)"
"Participated in hackathon" →  "Won 2nd place at HackIndia 2025,
                                built {project} in 36 hours"
"CGPA 8.4"               →     Lead with it -- above 8.0 always mention it
"Know Python"            →     "Python (NumPy, Pandas, PyTorch) --
                                used in 3 projects"
```

**Your cv.md sections as a student:**
1. Summary -- 2 lines, your target role and strongest proof point
2. Projects -- most important section, 3-4 projects with metrics
3. Education -- degree, college, CGPA (if > 8.0), relevant coursework
4. Skills -- languages, frameworks, tools -- only what you actually know
5. Achievements -- hackathons, competitions, open source, publications
6. Certifications -- only relevant ones, not every Coursera badge

---

### Reading Your Intern Report

The two most important scores for a student:

**PPO Probability (1-5):** For many students the internship IS the job interview. A 4-5 here means strong historical conversion. A 1-2 means treat it as a learning opportunity, not a job pipeline.

**Brand Value (1-5):** What does this company name do for your next opportunity? A Tier 1 brand (Google, Goldman, Razorpay) opens doors even if the work was average. A Tier 4 brand requires a strong story to compensate.

```
Project Match 4.0  +  PPO 4/5  +  Brand 5/5  =  Apply immediately
                                                  This is a career-defining opportunity

Project Match 3.5  +  PPO 2/5  +  Brand 3/5  =  Apply only if nothing better
                                                  Build the missing skill first

Project Match 2.0  +  any      +  any        =  SKIP
                                                  You will not get shortlisted
                                                  Build {specific skill} first
```

---

### On-Campus vs Off-Campus

The system detects your track and adjusts strategy accordingly:

**On-campus:** The company is coming to you. Your college brand matters. The placement cell is your ally. Focus on clearing the coding round and interview -- the system helps you prep for both.

**Off-campus:** You are going to them. Your projects must speak louder because there is no placement cell vouching for you. The system will push harder on cover letter personalisation and LinkedIn outreach.

---

### Red Flags to Never Ignore

```
🔴  Unpaid / no stipend         Your time has real value. Always verify.

🔴  Bond / service agreement    Illegal for most internships in India.
                                Do not sign without legal advice.

🔴  Commission only             This is freelance work, not an internship.

🔴  "Certificate only"          Not worth it unless the brand is exceptional.

🟠  500+ applicants, no         Likely ghost posting on Internshala.
    response in 30 days         Check directly on company website.

🟠  Vague JD, no tech stack     You may end up doing data entry.
    mentioned                   Ask specifically what you will work on.
```

---

### Key Commands for Students

| What you want to do | Command |
|---|---|
| Evaluate an internship | `/career-ops intern {URL or JD}` |
| Generate tailored CV | `/career-ops pdf` |
| Research a company | `/career-ops deep` |
| Prep for an interview | `/career-ops interview-prep` |
| Evaluate a course/cert | `/career-ops training` |
| Check your applications | `/career-ops tracker` |

---

### One Tip That Changes Everything

After your first evaluation, tell Claude what you want to improve:

> "I keep getting low Project Match scores for ML roles. What should I build next?"

The system will look at your cv.md, look at the roles you have been evaluated against, and suggest the specific project or course that closes the gap fastest. This turns career-ops-india into a learning roadmap, not just a job filter.
