# TalentPulse — AI Talent Scouting & Engagement Agent

> Paste a job description. The agent searches LinkedIn, extracts real profiles, scores candidates, simulates outreach, and delivers a ranked shortlist in under 90 seconds.

**Live Demo:** https://talent-scout-pro.netlify.app/

**Direct Agent Link:** https://app.relevanceai.com/agents/f1db6c/920de9da-08a4-49f3-9bd6-3680f2bcfe69/7819e915-0a2d-4046-a2fe-e18952de568f/embed-chat

---

## The problem it solves

Recruiters spend hours sifting through profiles and chasing candidate interest. TalentPulse is an AI agent that automates the entire top-of-funnel recruitment process. Paste any job description and get a ranked shortlist with real LinkedIn profiles, Match Scores, Interest Scores, notice periods, screening questions, and a Recruiter Action Plan in under 90 seconds.

Built specifically for the **Indian recruitment market**: Indian cities, Indian companies, Indian salary norms (LPA), and standard notice period awareness (30 to 90 days) baked into every run.

---

## Live demo

**Primary URL:** https://talent-scout-pro.netlify.app/

No login required. No API key needed. Paste any job description and the agent runs automatically.

**Works for any role:** Content marketing, engineering, product, design, sales, operations — the agent adapts its search strategy to the JD.

---

## How it works — 5-step pipeline

### Step 1: JD parsing
Extracts job title, 3 to 5 alternate titles commonly used in India, required skills, experience range, location, must-have criteria, nice-to-have criteria, seniority level, and industry domain.

### Step 2: Live candidate discovery via Google Search
Runs 5 targeted Google searches using the `site:linkedin.com/in` operator to find real public LinkedIn profiles matching the role. Search queries use Indian cities, Indian market terminology, and multiple title variants to cast the widest possible net.

Example searches generated automatically:
```
site:linkedin.com/in "Content Marketing Manager" "SEO" "Bengaluru"
site:linkedin.com/in "Content Lead" "Ahrefs" "India"
site:linkedin.com/in "Growth Content Manager" "B2B SaaS" "India"
```

### Step 3: LinkedIn profile extraction
For each LinkedIn URL found, the agent extracts: full name, current title, current company, location, years of experience, and top skills. Real profiles are labelled "From LinkedIn". If a profile cannot be extracted, it is replaced with a realistic simulated Indian candidate (labelled "Simulated") from a relevant Indian company such as Freshworks, Razorpay, BrowserStack, Postman, Chargebee, or Zoho.

### Step 4: Dual scoring

**Match Score (0 to 100):**
- Skills alignment: 40%
- Experience fit: 30%
- Must-have criteria coverage: 20%
- Growth potential: 10%

**Interest Score (0 to 100):**
Simulates a realistic LinkedIn DM or WhatsApp outreach exchange. Scores based on response warmth, career trajectory alignment, and openness to move. Accounts for Indian market norms including notice periods and seniority expectations.

### Step 5: Ranked shortlist + Recruiter Action Plan

```
Final Score = (Match Score × 0.60) + (Interest Score × 0.40)
```

Output table includes: Rank, Name, Current Role, Current Company, Location, Match Score, Interest Score, Final Score, Notice Period, Recommendation.

Followed by a **Recruiter Action Plan** with:
- Top 2 candidates to contact immediately
- Recommended outreach channel (LinkedIn DM or WhatsApp)
- One targeted screening question per candidate addressing their biggest skill gap
- Estimated time to hire based on notice periods

---

## Architecture

```
[Job Description Input]
         ↓
   ┌─────────────────────┐
   │     JD Parser       │
   │  Extracts 8 fields  │
   │  + Indian variants  │
   └─────────────────────┘
         ↓
   ┌──────────────────────────────────────────────┐
   │           Candidate Discovery                │
   │                                              │
   │  [Google Search Tool]   [Apify — Production] │
   │  5 targeted searches    LinkedIn live scrape │
   │  site:linkedin.com/in   Real-time profiles   │
   │  Real public profiles   Enterprise scale     │
   └──────────────────────────────────────────────┘
         ↓
   ┌──────────────────────────┐
   │  LinkedIn Profile        │
   │  Extraction Tool         │
   │  Name, title, company,   │
   │  location, skills        │
   └──────────────────────────┘
         ↓
   ┌─────────────────────┐
   │    Match Scorer     │
   │  Skills 40%         │
   │  Experience 30%     │
   │  Must-haves 20%     │
   │  Growth 10%         │
   └─────────────────────┘
         ↓
   ┌─────────────────────┐
   │  Outreach Simulator │
   │  LinkedIn DM or     │
   │  WhatsApp format    │
   │  Interest Score     │
   └─────────────────────┘
         ↓
   ┌──────────────────────────────┐
   │  Ranker + Action Plan        │
   │  Final Score formula         │
   │  Notice periods              │
   │  Screening questions         │
   │  Time-to-hire estimate       │
   └──────────────────────────────┘
         ↓
   [Ranked Shortlist + Recruiter Action Plan]
```

**Agent platform:** Relevance AI
**LLM:** Claude (via Relevance AI)
**Live data:** Google Search tool (site:linkedin.com/in queries)
**Profile extraction:** LinkedIn Profile Extraction tool
**Fallback:** Simulated Indian candidate profiles from relevant companies
**Front-end:** Single HTML file on Netlify
**Production data source:** Apify LinkedIn scraper (architecture ready)

---

## Sample input

```
Job Title: Senior Content Marketing Manager
Company: B2B SaaS startup, Bengaluru
Experience required: 6 to 9 years
Must have: strong SEO knowledge, experience managing a content
team of 4 or more writers, B2B SaaS content experience
Skills: SEMrush, HubSpot, content strategy, keyword research,
thought leadership
Location: Bengaluru, hybrid
Budget: 30 to 45 LPA
```

---

## Sample output

| Rank | Name | Current Role | Company | Location | Match | Interest | Final | Notice | Rec |
|------|------|-------------|---------|----------|-------|----------|-------|--------|-----|
| 1 | Priya Menon (From LinkedIn) | Content Marketing Lead | Freshworks | Bengaluru | 95 | 80 | 89 | 30 days | Phone screen |
| 2 | Sneha Iyer (From LinkedIn) | Content Marketing Manager | Chargebee | Bengaluru | 89 | 80 | 85 | 30 days | Phone screen |
| 3 | Rahul Desai (Simulated) | Content & SEO Associate | BrowserStack | Bengaluru | 88 | 60 | 77 | 60 days | Technical screen |
| 4 | Divya Pillai (From LinkedIn) | Content Strategist | Perfios | Bengaluru | 77 | 75 | 76 | 30 days | Phone screen |
| 5 | Vikram Nair (From LinkedIn) | Digital Content Manager | Razorpay | Bengaluru | 85 | 50 | 71 | 60 days | Assess fit/level |

Each candidate includes: simulated outreach exchange, notice period, skill gap flags, screening question, and estimated time to hire.

---

## What makes it India-specific

- Searches prioritise Indian cities: Bengaluru, Mumbai, Delhi, Hyderabad, Pune
- Simulated fallback profiles use real Indian product companies
- Interest scores account for Indian notice period norms (30 to 90 days)
- Salary expectations referenced in LPA
- Outreach simulated in LinkedIn DM and WhatsApp format
- Seniority calibrated to Indian market compensation bands

---

## Local setup

No installation required.

1. Download `talent-scout-agent.html`
2. Open in any browser
3. The live agent loads automatically inside the page
4. Paste any job description and press send

---

## Submission checklist

- [x] Working prototype: https://talent-scout-pro.netlify.app/
- [x] Source code in public repo with README
- [x] Architecture diagram (see `architecture.png`)
- [x] Sample inputs and outputs (this README)
- [ ] Demo video (Loom — add link here after recording)

---

## Built by

Tanveer Masood — Senior Content and AI Workflow Professional
GitHub: https://github.com/tanweer4u
LinkedIn: https://linkedin.com/in/tanveer-masood
