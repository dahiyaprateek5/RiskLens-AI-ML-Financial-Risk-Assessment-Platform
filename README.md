# RiskLens — AI/ML Financial Risk Assessment Platform

**Built by Prateek Dahiya** | Personal Project | 2025 – Present

RiskLens is something I built because I wanted to solve a real problem, not just complete a coursework exercise. It is a full-stack AI-powered financial analytics platform that evaluates any company (publicly traded or UK-registered private) and generates an instant financial risk score using machine learning.

The platform serves a genuine use case: helping SMEs, lenders, and investors quickly assess whether a company is financially healthy before making decisions. I designed, built, tested, and deployed the entire thing myself.

---

## What It Does

The platform takes a company ticker or UK Companies House number, pulls financial data from multiple sources, runs it through an ML ensemble model, and returns a 0-100 risk score with bankruptcy probability at 6, 12, and 24 month horizons.

**Core capabilities:**

- **AI Risk Scoring** — ML ensemble (RandomForest + XGBoost + LightGBM) trained on financial data, predicting distress probability and generating sub-scores for Liquidity, Profitability, Stability, and Debt
- **Final Verdict Engine** — Four-label verdict (Safe to Invest / Monitor Closely / Elevated Risk / High Risk) with plain-English reasoning, driver explanations, and confidence indicators
- **Global + UK Private Company Analysis** — Listed companies via yfinance, Alpha Vantage, and FMP. UK private companies via Companies House Document API, automatically fetching and parsing iXBRL annual accounts
- **Document-Based Risk Analysis** — Upload a PDF or Excel file, Gemini 2.5 Flash extracts the financials, ML pipeline scores the risk. Regex fallback ensures results even with partial data
- **15+ Financial Ratio Analysis** — Liquidity, profitability, leverage, growth, and cash flow metrics with colour-coded health indicators
- **Company Comparison** — Compare up to five companies side by side on financial ratios, revenue trends, and risk scores
- **Live Markets** — Top gainers, losers, and most active stocks with one-click analysis
- **Watchlist & Alerts** — Track companies and get notified on price changes, risk score shifts, and financial events
- **AI CFO Assistant** — Gemini 2.5 Flash-powered conversational advisor for financial guidance
- **SME Finance Tools** — Working capital calculator, loan affordability estimator, invoice financing calculator
- **Accounting Module** — Journal entries, P&L, balance sheet, and cash flow for SMEs
- **Supply Chain Risk** — Evaluate supplier risk exposure and detect dependencies

---

## How I Built It (Technology Stack)

### Backend
- **FastAPI** (async Python 3.11+) — chose this for performance and clean API design
- **Supabase** (PostgreSQL + Auth + Row Level Security) — handles data persistence and user authentication
- **scikit-learn** (ML ensemble: RandomForest + XGBoost + LightGBM) — trained and tuned the models myself
- **Celery + Redis** — background job processing and scheduled tasks
- **Gemini 2.5 Flash** — document extraction, AI CFO, and recommendation generation
- **Stripe** — subscription billing with webhook handling
- **slowapi** — per-endpoint rate limiting for security
- **pytest** — test suites with 80%+ code coverage

### Frontend
- **Next.js 14** (App Router, TypeScript) — server-side rendering and modern React patterns
- **Tailwind CSS** — responsive styling
- **TanStack React Query + Axios** — data fetching and caching
- **Recharts + custom SVG components** — data visualisation including a segmented speedometer gauge I designed from scratch

### Infrastructure & DevOps
- **Docker** — containerised the full stack (backend + frontend + Redis)
- **AWS (EC2, S3)** — cloud deployment
- **GitHub Actions** — CI/CD pipeline automating tests and deployment
- **Railway** (backend) + **Vercel** (frontend) — production hosting

### Data Sources
| Source | Purpose |
|--------|---------|
| yfinance | Primary: company financials, stock history |
| Alpha Vantage | Company search, backup financials |
| Financial Modeling Prep | Secondary backup |
| Polygon.io | Real-time market data |
| Companies House REST + Document API | UK company search, profiles, iXBRL accounts |
| Gemini 2.5 Flash | Document extraction, AI recommendations |

---

## What This Project Demonstrates

I am listing this because I think it shows more about my engineering ability than a CV bullet point can:

**System Design** — I designed the full architecture: async FastAPI backend, PostgreSQL with Row Level Security, Redis-backed task queue, Stripe billing integration, and a Next.js frontend. I made every architectural decision myself, from database schema to API rate limiting strategy.

**ML Engineering** — I did not just plug in a pre-trained model. I built the pipeline: data collection from multiple financial APIs, feature engineering (15+ financial ratios), model training and evaluation (RandomForest, XGBoost, LightGBM ensemble), and deployed the model behind a production API.

**Data Pipeline Engineering** — The UK company analysis flow is probably the most interesting part. It hits the Companies House API, downloads iXBRL annual accounts, parses them with regex matching 50+ UK GAAP/IFRS XBRL concepts, and feeds the extracted data into the same ML pipeline as listed companies. I wrote all of the parsing logic myself.

**API Design** — 30+ REST endpoints, JWT authentication, CORS hardening, rate limiting, Stripe webhook handling. The API is documented with Swagger/ReDoc.

**Testing & Quality** — pytest test suites covering core ML and API modules. CI/CD pipeline runs tests automatically before deployment.

**Production Deployment** — Docker Compose for local development, Railway + Vercel for production, with environment-specific configuration and a production checklist I follow for every deploy.

**Frontend Engineering** — 25+ pages/routes, responsive UI, custom SVG data visualisation components, real-time data fetching with React Query. I built the segmented speedometer risk gauge and circular score ring components from scratch.

---

## Architecture Overview

```
Client (Browser) — Next.js 14, Port 3000
        |
        | HTTP/REST (Axios + React Query)
        v
FastAPI Backend — Port 8001
  - AnalysisService, MLService, FinancialDataService
  - JWT Auth, Rate Limiting, CORS
        |                    |
        v                    v
   Supabase             External APIs
   PostgreSQL            yfinance, Alpha Vantage, FMP
   + Auth + RLS          Companies House, Gemini 2.5 Flash
        |
        v
   Celery Worker <---- Redis
```

---

## Scale of the Project

- **30+ API endpoints** across analysis, companies, documents, subscriptions, admin
- **25+ frontend pages** including dashboards, analysis reports, comparison tools, admin panels
- **15+ database tables** with Row Level Security policies
- **50+ regex patterns** for iXBRL financial data extraction
- **ML ensemble** with three model types trained on financial distress data
- **Three subscription tiers** with Stripe integration and usage metering

---

## A Note on the Code

This is a proprietary personal project. The source code is not publicly available on GitHub as I am actively developing it and exploring commercial potential.

However, I am happy to walk through the codebase, architecture decisions, and technical implementation in detail during a conversation or interview. If we connect personally, I can provide a private code walkthrough or demo. I would rather show someone the real thing than have them take my word for it.

If you would like to see RiskLens in action or discuss the technical decisions behind it, feel free to reach out:

**Prateek Dahiya**
dahiyaprateek5@gmail.com | [LinkedIn](http://www.linkedin.com/in/dahiyaprateek5) | [GitHub](https://github.com/dahiyaprateek5)
