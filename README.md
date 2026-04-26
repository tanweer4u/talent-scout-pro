# Talent Scout Pro — AI Talent Scouting & Engagement Agent

> Takes a job description. Discovers matching candidates. Engages them conversationally. Outputs a ranked shortlist scored on Match and Interest.

**Live Demo:** https://talent-scout-pro.netlify.app/

**Git Username:** tanweer4u

---

## What it does

Recruiters spend hours sifting through profiles and chasing candidate interest. Talent Scout Pro is an AI agent that automates the entire top-of-funnel:

1. Parses any job description to extract role requirements
2. Discovers matching candidates via Google Search on LinkedIn
3. Scores each candidate on Match Score (0-100) and Interest Score (0-100)
4. Simulates a personalised outreach conversation with each candidate
5. Outputs a ranked shortlist the recruiter can act on immediately

---

## Working Prototype

**Primary URL:** https://talent-scout-pro.netlify.app/

The Netlify page embeds the live Relevance AI agent. No login required. Paste any job description and the agent runs the full pipeline automatically in under 90 seconds.

**Direct Agent Link:** https://app.relevanceai.com/agents/f1db6c/920de9da-08a4-49f3-9bd6-3680f2bcfe69/7819e915-0a2d-4046-a2fe-e18952de568f/embed-chat

---

## Sample Input

```
Job Title: Senior Content Marketing Manager
Company: B2B SaaS startup, Bengaluru
Experience required: 6 to 9 years
Must have: SEO knowledge, managing a content team of 4+ writers,
B2B SaaS content experience
Skills: SEMrush, HubSpot, content strategy, keyword research
Location: Bengaluru, hybrid
Budget: 30 to 45 LPA
```

---

## Sample Output

```
RANK1: Arjun Kapoor (From Database) | MATCH:92 | INTEREST:86 | FINAL:89 | REC:Strong
RANK2: Kavitha Subramaniam (From Database) | MATCH:88 | INTEREST:86 | FINAL:87 | REC:Interview
RANK3: Vikram Nair (From Database) | MATCH:90 | INTEREST:72 | FINAL:81 | REC:Interview

Recruiter: "Hi Arjun — quick chat about a Senior Content Marketing
Manager role in Bengaluru?"
Arjun: "Sounds great — open to relocate; available in 2 months."

Screening Q: "Describe the largest content team you have directly
managed and the KPIs you used to measure pipeline impact."
```

---

## Architecture

```
[Job Description Input]
         |
   [JD Parser]
   Extracts: title, skills, experience, must-haves
         |
   [Candidate Discovery]
   Google Search tool: site:linkedin.com/in queries
   5 targeted searches per JD
   Knowledge base fallback: 10 curated Indian profiles
         |
   [Match Scorer]
   Skills alignment:    40%
   Experience fit:      30%
   Must-have criteria:  20%
   Growth potential:    10%
         |
   [Outreach Simulator]
   Personalised LinkedIn DM per candidate
   Candidate reply simulation
   Interest Score based on warmth + alignment
         |
   [Ranker]
   Final Score = Match x 0.6 + Interest x 0.4
   Ranked shortlist with notice periods + screening questions
         |
   [Output: Ranked Shortlist + Recruiter Action Plan]
```

**Platform:** Relevance AI (agent orchestration)
**LLM:** Claude via Relevance AI
**Live data:** Google Search tool (site:linkedin.com/in)
**Knowledge base:** 10 curated B2B SaaS candidates, Bengaluru
**Production data source:** Apify LinkedIn scraper (architecture ready)
**Front-end:** HTML on Netlify

---

## Scoring Logic

| Dimension | Weight | What drives it |
|-----------|--------|----------------|
| Match Score | 60% | Skills coverage, experience fit, must-have criteria |
| Interest Score | 40% | Response warmth, career alignment, openness to move |
| Final Score | 100% | (Match x 0.6) + (Interest x 0.4) |

---

## India-Specific Features

- Searches prioritise Indian cities: Bengaluru, Mumbai, Delhi, Hyderabad, Pune
- Notice periods in Indian norms: 30, 60, 90 days
- Salary in LPA
- Outreach simulated as LinkedIn DM or WhatsApp
- Fallback profiles from Indian product companies: Freshworks, Razorpay, BrowserStack, Chargebee, Postman

---

## Local Setup

No installation required.

1. Download `talent-scout-agent.html`
2. Open in any browser
3. The live agent loads automatically
4. Paste any job description and press send

---

## Built by

Tanveer Masood
GitHub: https://github.com/tanweer4u
LinkedIn: https://linkedin.com/in/tanveer-masood
