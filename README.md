# MAVERICK

**AI-powered pre-meeting sales intelligence agent**

Generate sourced sales briefs in under 60 seconds. Find company risks. Ask smarter questions. Close more deals.

---

## 🎯 What is MAVERICK?

MAVERICK helps sales reps prep for big client calls by automatically researching companies and finding key risks—in 1 minute instead of 3 hours.

**Input:**
- Company name
- Meeting with (e.g., "CFO")
- Meeting date

**Output:**
- 3 key business risks (with sources)
- 5 discovery questions (LEVER format)
- 4-item pre-call checklist

**Status:** MVP (Phase 5). Validated with 10 real companies. 100% source accuracy. Ready for pilot testing.

---

## ✨ Key Features

✅ **Automated Web Research** — Searches public data for company-specific signals  
✅ **Sourced Intelligence** — Every risk backed by real URLs (news, court filings, announcements)  
✅ **Domain-Specific Scoring** — Understands 4 risk domains: taxes (GST), customs/trade, logistics, cash flow  
✅ **Confidence Ratings** — Signals ranked by confidence level (High/Medium/Low)  
✅ **Discovery Questions** — Pre-formatted questions reps can ask in meetings  
✅ **Privacy-First** — Data stored locally on device. No server database.  
✅ **Fast** — Brief generated in 30–60 seconds  

---

## 🏗️ Architecture

```
User Input
   ↓
[n8n Workflow]
   ├─ Validate & Build Prompt (800 tokens)
   ├─ Tavily Web Search (3–8 queries)
   ├─ Claude Haiku 4.5 (Score + Extract)
   ├─ Parse & Validate JSON
   └─ Response to Frontend
   ↓
[HTML/JS Frontend]
   ├─ Brief Display (3 signals, 5 questions)
   ├─ Source Links (clickable, verified)
   ├─ Post-Call Feedback (Qualified/Exploring/Not a Fit)
   └─ Local Storage (no server)
```

### Tech Stack

| Component | Technology | Notes |
|-----------|-----------|-------|
| Workflow Engine | n8n (self-hosted) | Visual automation, 5 nodes |
| Web Search API | Tavily | Structured search, 3–8 queries per brief |
| LLM | Claude Haiku 4.5 | Fast, reliable, cost-effective (~$0.10/brief) |
| Frontend | HTML/JS | Single-page app, localStorage |
| Data Storage | localStorage | No backend database, privacy-first |
| Privacy | Public sources only | No GSTN/customs database access |

---

## 🚀 Getting Started

### Prerequisites
- n8n account (self-hosted or cloud)
- Anthropic API key (Claude Haiku 4.5)
- Tavily API key (web search)
- Modern browser (Chrome/Firefox/Safari)

### Installation

#### 1. Set up n8n Workflow
```bash
# Clone or recreate the 5-node workflow:
1. Webhook: HTTP POST (company + role + date)
2. Code: Build system prompt (800 tokens)
3. Agent: Claude + Tavily (max 3 iterations)
4. Code: Parse + validate JSON output
5. HTTP Response: Return brief to frontend

# Environment variables:
ANTHROPIC_API_KEY=your_key_here
TAVILY_API_KEY=your_key_here
```

#### 2. Deploy Frontend
```bash
# Simple: copy HTML/JS files to a static host
# GitHub Pages, Vercel, Netlify, or self-hosted

# Structure:
├── index.html
├── app.js
├── styles.css
└── assets/
    └── logo.png
```

#### 3. Connect Frontend to n8n
```javascript
// In app.js, set your n8n webhook URL:
const WEBHOOK_URL = "https://your-n8n-instance.com/webhook/maverick";

// Frontend sends:
{
  "company": "Suzlon Energy",
  "role": "CFO",
  "meeting_date": "2024-09-15"
}

// n8n responds with:
{
  "signals": [...],
  "questions": [...],
  "checklist": [...]
}
```

---

## 📊 Signal Inventory (15 Signal Types)

### Domain: Taxes (GST) — 40%
- Multi-State GST Compliance
- ITC Reconciliation Failures
- GSTR Filing Delays/Errors
- GST Refund Backlog

### Domain: Customs & Trade — 30%
- CBAM/EU Carbon Border Adjustment
- Import Duty Classification Disputes
- Export License Compliance / FTP Changes
- FTA Underutilization

### Domain: Logistics — 20%
- Multi-Modal Transport Planning
- Warehousing / E-way Bill Compliance
- Customs Clearance Delays

### Domain: Cash Flow — 10%
- GST Refund Delays
- Penalty Accumulation Risk

**Confidence Scoring:**
- **HIGH (90–95%)**: 2+ company-specific sources (news + court filing)
- **MEDIUM (70–80%)**: 1 company-specific source
- **LOW (50–60%)**: Industry pattern only, no company-specific proof

---

## 📝 Testing & Validation

### MVP Testing (Phase 5)
- **Sample size:** 10 real companies (Suzlon, TCS, Bharti Airtel, etc.)
- **Verification:** Manually checked all links + claims
- **Result:** 30/30 signals verified as real (100% accuracy)
- **Hallucination rate:** 0% (after validation filtering)

### Confidence Metrics
| Company | Signals | Confidence | Verified? |
|---------|---------|-----------|-----------|
| Suzlon Energy | 3 | 90–95% | ✅ |
| TCS | 3 | 85–95% | ✅ |
| Bharti Airtel | 3 | 80–90% | ✅ |
| ... | ... | ... | ... |

### Known Limitations
- ❌ No data for companies with zero public information
- ❌ No private database access (GSTN, customs records)
- ❌ Single geography (India only)
- ❌ No real-world sales impact data yet (Phase 6 test)

---

## 💰 Pricing (Phase 7+)

### INDIVIDUAL
- **₹4,000/month**
- One rep, unlimited briefs
- Full access to all signal types

### TEAM
- **₹3,500/seat/month (minimum 5 seats)**
- 10% volume discount
- Manager view (adoption, usage metrics)
- Team reporting

### ENTERPRISE
- **Custom pricing**
- 50+ reps, custom integrations
- SSO + dedicated support
- On-premises option

---

## 🔄 Call Outcome Feedback

After using MAVERICK, reps report call outcomes:

**QUALIFIED** ✅
- Prospect has the risk we identified
- Interested in solving it
- → Warm lead for follow-up

**EXPLORING** 🔍
- Prospect acknowledges problem
- Wants more information
- → Nurture opportunity

**NOT A FIT** ❌
- Problem doesn't exist or already solved
- Prospect not interested
- → Feedback to improve targeting

---

## 📈 Success Metrics

### Phase 5 (Current)
- ✅ Technical validation: 100% source accuracy
- ✅ System reliability: <60 sec latency
- ✅ Hallucination control: 0% fake URLs

### Phase 6 (Validation - Q4 2026)
- 📌 5 pilot customers (free trial)
- 📌 NPS >40 (would recommend)
- 📌 Activation >80% (use 3+ times in first week)
- 📌 Case studies from pilots

### Phase 7 (Growth - Q1 2027)
- 📌 20–30 paying customers
- 📌 ₹12–15 lakh ARR
- 📌 Churn <10% monthly
- 📌 Validated pricing elasticity

---

## 🛠️ Development

### Local Setup

```bash
# Clone repo
git clone https://github.com/your-org/maverick.git
cd maverick

# Install dependencies (if applicable)
npm install

# Set environment variables
cp .env.example .env
# Edit .env with your API keys

# Run n8n locally
docker run -it --rm -p 5678:5678 n8nio/n8n

# Run frontend dev server
npm start

# Open browser
http://localhost:3000
```

### Project Structure
```
maverick/
├── n8n/
│   ├── workflow.json          # 5-node n8n workflow
│   └── system-prompt.txt      # 800-token Claude prompt
├── frontend/
│   ├── index.html
│   ├── app.js                 # Core logic
│   ├── styles.css
│   └── assets/
├── docs/
│   ├── ARCHITECTURE.md        # Technical deep-dive
│   ├── SIGNALS.md             # Signal inventory
│   └── API.md                 # Frontend-to-n8n spec
├── .env.example
├── README.md
└── LICENSE
```

### Code Quality
- No linting/testing setup yet (Phase 6)
- Manual QA: 10 company tests
- Performance targets: <60s latency, <₹20 cost per brief

---

## 🤝 Team

| Role | Owner |
|------|-------|
| Product & GTM | Rahul (PM) |
| Backend Architecture | Rahul |
| Frontend UX | Gaurav / Bhavani |
| Research & Signals | Sanjeet / Sarita |
| Project Coordination | Abhijit |

---

## 📚 Documentation

- **[ARCHITECTURE.md](./docs/ARCHITECTURE.md)** — System design, workflow details
- **[SIGNALS.md](./docs/SIGNALS.md)** — Signal types and scoring logic
- **[API.md](./docs/API.md)** — Frontend-to-n8n request/response format
- **[TESTING.md](./docs/TESTING.md)** — How we validated with 10 companies

---

## 🔐 Privacy & Security

✅ **No personal data stored**
- Company names and call prep data stay on user's device
- No server-side database
- No tracking or analytics

✅ **Public sources only**
- All data from news, court filings, announcements
- No GSTN, customs, or private database access
- No scraping of proprietary platforms

✅ **Source validation**
- Every URL verified as real
- Every claim checked against source
- Hallucinated URLs filtered out

---

## 📋 Roadmap

### Phase 6 (Validation)
- Pilot with 5 real sales teams
- Collect feedback and case studies
- Validate pricing and positioning

### Phase 7 (Growth)
- Launch paid tiers
- Scale via Product Hunt, content, direct sales
- Target 20–30 customers

### Phase 8+ (Expansion)
- CRM integrations (Salesforce, Zoho)
- Manager analytics dashboard
- Multi-geography (Southeast Asia, Middle East)
- Mobile app

---

## 📞 Support & Feedback

- **Email:** team@maverick.ai (Phase 6+)
- **Issues:** GitHub Issues (for beta testers)
- **Feedback form:** https://maverick.ai/feedback (Phase 7+)

---

## 📄 License

[To be decided - likely MIT or Apache 2.0]

---

## 🙏 Acknowledgments

Built during BITSoM × Masai "Product Management with Generative & Agentic AI" program.

Special thanks to:
- Anthropic (Claude API)
- Tavily (web search)
- n8n (workflow automation)
- Course mentors and feedback

---

## 💬 Questions?

**For technical questions:**
- Check [ARCHITECTURE.md](./docs/ARCHITECTURE.md)
- Email: tech@maverick.ai

**For product questions:**
- Visit: https://maverick.ai
- Email: hello@maverick.ai

---

**Last updated:** September 2026  
**Current phase:** MVP (Phase 5)  
**Status:** Ready for pilot testing
