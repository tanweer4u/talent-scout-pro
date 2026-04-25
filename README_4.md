# TalentPulse — AI Talent Scouting & Engagement Agent

> Paste a job description. The agent parses, discovers, engages, and ranks candidates in one run.

**Live Demo:** https://talent-scout-pro.netlify.app/

---

## The problem it solves

Recruiters spend hours sifting through profiles and chasing candidate interest. TalentPulse is an AI agent that automates the entire top-of-funnel recruitment process. A recruiter pastes any job description and gets a ranked shortlist with Match Scores, Interest Scores, and simulated outreach conversations in under 60 seconds.

---

## Working prototype

**Primary URL:** https://talent-scout-pro.netlify.app/

The Netlify page embeds the live Relevance AI agent. No API key or login required. Paste any job description and the agent runs the full 4-step pipeline automatically.

**Built with:**
- Relevance AI (agent orchestration and LLM processing)
- Structured candidate knowledge base (10 Bengaluru B2B SaaS profiles)
- HTML + CSS front-end deployed on Netlify

---

## 4-step pipeline

### Step 1: JD parsing
Extracts job title, required skills, experience range, must-have criteria, nice-to-have criteria, and company context from any free-form job description text.

### Step 2: Candidate discovery
Searches the structured candidate knowledge base first. Candidates found in the database are labelled "From Database". If fewer than 5 matches are found, the agent supplements with AI-simulated profiles labelled "Simulated". In production, this step connects to LinkedIn via Apify for live candidate scraping.

### Step 3: Match scoring (0–100)
Scores each candidate against the parsed JD using a weighted formula:
- Skills alignment: 40%
- Experience fit: 30%
- Must-have criteria coverage: 20%
- Growth potential: 10%

### Step 4: Interest simulation (0–100)
Simulates a personalised 2-line outreach conversation with each candidate. Scores interest based on response warmth, career trajectory alignment, and openness to move.

---

## Scoring logic

```
Final Score = (Match Score × 0.60) + (Interest Score × 0.40)
```

Candidates are ranked highest to lowest by Final Score. The recruiter sees:
- Rank
- Name and current role
- Match Score
- Interest Score
- Final Score
- One-line recommendation
- Simulated outreach exchange

---

## Architecture

```
[Job Description Input]
         ↓
   ┌─────────────────┐
   │   JD Parser     │  Extracts: title, skills, experience, must-haves
   └─────────────────┘
         ↓
   ┌──────────────────────────────────────────┐
   │         Candidate Discovery              │
   │                                          │
   │  [Knowledge Base]    [Apify — LinkedIn]  │
   │  10 curated profiles  Live scrape        │
   │  Demo data source     Production source  │
   └──────────────────────────────────────────┘
         ↓
   ┌─────────────────┐
   │  Match Scorer   │  Score 0–100 per candidate
   └─────────────────┘
         ↓
   ┌─────────────────┐
   │ Outreach        │  Simulated conversation + Interest Score
   │ Simulator       │
   └─────────────────┘
         ↓
   ┌─────────────────┐
   │  Ranker         │  Final Score = Match × 0.6 + Interest × 0.4
   └─────────────────┘
         ↓
   [Ranked Shortlist Output]
```

**Agent platform:** Relevance AI
**LLM:** Claude (via Relevance AI)
**Knowledge base:** Structured candidate database (10 Bengaluru B2B SaaS profiles)
**Production data source:** Apify LinkedIn scraper (architecture ready, demo uses knowledge base)
**Front-end:** Single HTML file on Netlify

---

## Sample input

```
Job Title: Senior Content Marketing Manager
Company: B2B SaaS startup, Bengaluru
Experience required: 6 to 9 years
Must have: strong SEO knowledge, experience managing a content team
of 4 or more writers, B2B SaaS content experience
Skills: SEMrush, HubSpot, content strategy, keyword research,
thought leadership
Location: Bengaluru, hybrid
Budget: 30 to 45 LPA
```

---

## Sample output

| Rank | Name | Match | Interest | Final | Rec |
|------|------|-------|----------|-------|-----|
| 1 | Priya Menon (From Database) | 95 | 80 | 91 | Contact — High priority |
| 2 | Arjun Kapoor (From Database) | 90 | 85 | 89 | Contact — High |
| 3 | Divya Pillai (From Database) | 87 | 88 | 87 | Contact — High |
| 4 | Sneha Iyer (From Database) | 85 | 90 | 87 | Contact — High |
| 5 | Vikram Nair (From Database) | 88 | 70 | 83 | Consider — Medium |

Each candidate includes a simulated outreach exchange, availability status, and a one-line recruiter recommendation.

---

## Local setup

No installation required. The tool runs entirely in the browser.

1. Download `talent-scout-agent.html`
2. Open it in any browser (Chrome, Edge, Firefox)
3. The embedded agent loads automatically
4. Paste any job description and click send

---

## Candidate knowledge base

The agent includes a structured database of 10 content marketing professionals based in Bengaluru with experience at B2B SaaS companies including Freshworks, Zoho, Chargebee, Razorpay, Postman, Leadsquared, Clevertap, WebEngage, Perfios, and Setu.

Each profile includes: current title, company, location, years of experience, skills, education, team management history, current salary, availability, and career goals.

In production, this database would be replaced or supplemented by live LinkedIn data via the Apify scraping integration.

---

## Submission checklist

- [x] Working prototype: https://talent-scout-pro.netlify.app/
- [x] Source code in public repo with README
- [x] Architecture diagram and scoring logic (this README)
- [x] Sample inputs and outputs (this README)
- [ ] 3 to 5 minute demo video (Loom — add link here)

---

## Built by

Tanveer Masood — Senior Content and AI Workflow Professional
GitHub: https://github.com/tanweer4u
LinkedIn: https://linkedin.com/in/tanveer-masood
