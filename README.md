## Giolivo Garcia Santarelli

I'm a licensed financial advisor in Argentina who started writing software because
the tools available to advisors in this market weren't good enough. I now do both:
I advise two independent books of clients, and I build and operate the systems that
run underneath that work.

**Río Negro / CABA, Argentina (UTC−3)** · [maat.work](https://maat.work) ·
[LinkedIn](https://ar.linkedin.com/in/giolivo-garcia-451954322) · open to remote roles

---

### Two things worth knowing up front

**Most of my 50+ repositories are private.** Many hold client data for a regulated
financial-advisory practice, or production systems for businesses that are paying
customers — that isn't going public. I'm glad to give a read-only invite or walk
through any of them live: the schema, the test suite, the parts that went wrong.
Just ask.

**My first verifiable commit is 29 October 2025.** Everything below was written
after that date. I'd rather anchor this to a date you can check than to a number I
round in my favour. Every figure on this page comes from a repository I can open
for you.

---

## The work

### Fintech & quantitative finance

**MaatWork CRM** — a full-stack CRM for financial advisors, in production and in
active use by two advisory teams. 56-table PostgreSQL schema (Prisma) covering
clients, portfolios, positions, risk profiles and compliance data. **1,425 commits,
681 test files** (unit + Playwright e2e), deployed on Vercel with CI/CD.
`Next.js · React · TypeScript · Prisma · PostgreSQL · Playwright`

**[FF5 quantitative portfolio construction](https://github.com/Gigisanta/QuantUcema)** (UCEMA, public) — the Fama-French 5-factor model
end to end: factor download from the Ken French library, OLS beta estimation with
statsmodels, and constrained SciPy optimizers for maximum Sharpe and maximum
Information Ratio against SPY, with sector and position limits. **135 tests.**
`Python · pandas · statsmodels · SciPy`

**MaatQuant** — a unified quantitative research system for US and Argentine markets,
scanning 385+ tickers for systematic strategy evaluation.
`Python · pandas · market-data APIs`

**Cactus Wealth market brief** — an agent that produces the weekly client market
brief as HTML and PDF, end to end and unattended. 72 commits.
`Python · WeasyPrint · LLM APIs`

**Balanz portal automation** — an authenticated read-only client that reuses a live
browser session to pull advisor-portal data the platform exposes no API for, and
normalizes it into a local store. **Read-only by design: it never places an order.**
That boundary is architectural, not a convention.
`Python · Playwright · CDP · SQLite`

**[planning.maat.work](https://planning.maat.work)** — generates personalized
financial plans from income, expenses, goals and time horizon. Online.
`Next.js · React · TypeScript`

### AI infrastructure

**Local LLM inference optimization (MLX / Apple Silicon)** — took decode throughput
on a 27B model from **13.3 to 27.8 tok/s** on a single M2 Max. I profiled first,
found 93% of decode time sitting in one quantized matrix-vector kernel, and wrote a
replacement for it in Metal. Output was verified **hash-identical** at every step,
so the speedup couldn't be hiding a correctness regression. Every number is
documented against the commit that produced it.
`Metal · MLX · quantization · speculative decoding`

**LLM inference gateway** — an OpenAI-compatible gateway routing to four local model
tiers, serving **7,400 requests in a measured 24 hours**. It has a background
priority class that yields the GPU to interactive traffic instead of starving it,
and abort-on-disconnect so a closed client frees the GPU on the next token.
`Python · SSE · GPU scheduling`

**Hermes — personal automation platform** — orchestrates **115 active scheduled
jobs** across finance reporting, email triage, publishing and scraping, on a
reusable module architecture (27 composable skills, 22 agent modules) with shared
config validation, rate limiting, locking and kill-switch safety.
`Python · cron · LLM APIs`

**job-autopilot** — harvests postings from 33 job-board and ATS APIs, scores them
against a structured profile, generates a tailored CV and drives the application
form in a real browser over the Chrome DevTools Protocol. The part I'd actually
defend is the answering layer: **every answer must trace to a fact in a single
source-of-truth file**, and any question it can't ground fails closed and goes to a
human. **2,800+ tests.**
`Python · CDP · SQLite`

**[Hermes quota-max router](https://github.com/Gigisanta/hermes-quota-max-router)** (public, MIT) — an OpenAI-compatible LLM router that uses only
verified free-tier models, with automatic fallback, quota tracking and a circuit
breaker. 42 commits.
`Python`

**Agent-Reach** — a single CLI that gives an agent read and search access across
Twitter, Reddit, YouTube, GitHub and more, with no API fees. **249 commits.**
`Python`

**DeFi strategy simulator (PancakeSwap)** — forward-shadow evaluation of liquidity
provision strategies against live market data with zero capital deployed. It
computes and validates calldata but is **architecturally incapable of signing or
broadcasting a transaction.**
`Python · Web3.py · BSC`

### Products shipped for real businesses

Each of these is a working system with a paying or operating customer behind it.

| Project | What it is | Commits |
|---|---|---|
| **Oro Azul** | Management system for swimming pools and aquatic centres | 327 |
| **MaatWork Concesionarios** | Platform for car dealerships, CI/CD on GitHub Actions | 119 |
| **Simon-AI** | Conversational AI product | 184 |
| **VARIGAS** | Industrial gas operations platform | 155 |
| **MaatWork landing** | Commercial-automation SaaS site, Next.js 16 + Tailwind v4 | 135 |
| **MaatWork Design System** | Centralized visual language: tokens, symbol library, components | 97 |
| **MaatWork Mission Control** | API-first Kanban for teams and their AI agents | 43 |
| **Custodia Digital Forense** | Local-first forensic vault: hashing, traceability, timeline | 39 |
| **Control Comercial** | Analytics layer over a beverage distributor's ERP | 28 |
| **AduanaDocs** | SaaS for customs documentation operations | 13 |
| **MaatWork Nutrición** | Practice-management system for nutritionists | 7 |
| **Pilates MaatWork** | Studio management with self-service registration | 52 |

### Public repositories

Start here if you want to read code rather than take my word for it.

**[Software-Inmobiliarias](https://github.com/Gigisanta/Software-Inmobiliarias)** —
RealEstate OS, a multi-tenant SaaS for real-estate agencies: commercial pipeline,
explainable lead scoring, real-time operations centre. Built roughly fifty-fifty
with a collaborator.

**[MeetCapture](https://github.com/Gigisanta/MeetCapture)** — native macOS menu-bar
app for meeting capture and Spanish/English transcription. 100% local: no cloud
audio service, no meeting bot, no Python daemon. Core Audio process taps, two
swappable ASR engines (whisper.cpp and a streaming sherpa-onnx zipformer at ~25×
realtime), live in-call transcription and speaker diarization.
`Swift · SwiftUI · Core Audio · sherpa-onnx`

**[hermes-quota-max-router](https://github.com/Gigisanta/hermes-quota-max-router)**
— OpenAI-compatible LLM router over verified free-tier models, with fallback,
quota tracking and a circuit breaker. MIT.
`Python · Redis`

**[QuantUcema](https://github.com/Gigisanta/QuantUcema)** — the Fama-French
5-factor pipeline above: factor download, OLS beta estimation, constrained
optimizers for max-Sharpe and max-Information-Ratio. 135 tests. MIT.
`Python · pandas · statsmodels · SciPy`

**[cactus-landing](https://github.com/Gigisanta/cactus-landing)** — the Cactus
Wealth Management site.

Also open by design and available on request: **Sueño Claro**, a privacy-first
sleep-cycle PWA with no account, no microphone and no tracking.

---

### The other half of the CV

I hold Argentina's **Idóneo CNV** securities-agent licence and a **Quantitative
Finance** certificate from **UCEMA**. Since June 2024 I've advised a personal book
of 40 clients with **USD 300K+ under management** at Grupo Abax, and since March
2025 a separate digital-assets mandate at Decrypto. That's where the domain
knowledge in everything above comes from — I'm not modelling a business I read
about.

---

### How I work

I have no computer science degree and nobody walked me through any of this. What I
do have is a method: **measure first, learn only what the measurement says matters,
and prove you didn't break anything on the way.** That's how the GPU kernel work
happened, and it's why almost every claim on this page has a number and a commit
behind it.

I'm also straightforward about AI: most of the lines I ship are drafted by a model.
What isn't generated is the part that decides whether the code is any good — what
to measure, which constraint is non-negotiable, and whether the result holds up.

**Spanish** (native) · **English** (C2)
