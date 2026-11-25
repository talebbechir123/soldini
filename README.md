# Soldini — Landing Page

Marketing site for **Soldini**, a daily reconciliation and fraud-detection platform for independent mobile-money agents who run several service points across several operators.

This repository contains only the public landing page: a single, dependency-free `index.html` (inline CSS and JavaScript, French-language content). The product itself is developed in a separate private repository.

## What Soldini does

Independent agents entrust cash and operator float to tellers at several points of service. Most operator statements carry no running balance, so the owner depends on what tellers report. Soldini closes that gap:

- **Reconcile** — every evening, the teller's blind cash count is compared with the balance expected from operator statements, per point and per operator.
- **Detect** — eight explainable fraud rules derived from real misappropriation cases (one-way beneficiaries, deposits right after a float top-up, transactions on staff numbers, money transiting through the network, duplicates, etc.). Each alert links to the transactions that triggered it.
- **Locate** — a map where each point is coloured by its daily status: balanced, discrepancy, alert or missing data.

## Product architecture (as presented on the page)

| Area | Choices |
|---|---|
| Backend | Python 3.12, FastAPI, SQLAlchemy 2 |
| Data | PostgreSQL 16 + PostGIS, row-level security for tenant isolation |
| Frontend | Next.js, TypeScript, MapLibre GL |
| Infrastructure | Docker, Caddy, Google Cloud |
| Accounting model | Append-only double-entry ledger; integer amounts, never floating point |
| Quality | 900+ automated tests, including end-to-end tests |

Performance work on the detection pipeline (profiling, reduced per-alert evidence storage, bulk writes, native base image) brought the analysis of 365,000 transactions from 260–439 s down to 13 s, and the full test suite from 36 min to 3.6 min.

Architecture, specifications and code by Ahmed Taleb Bechir, using spec-driven development with Spec Kit and Claude Code agents.

## Run the page locally

No build step:

```bash
open index.html            # macOS
xdg-open index.html        # Linux
# or serve it:
python3 -m http.server 8000
```

## Contact

**Ahmed Taleb Bechir** — talebbechir123@gmail.com
[atbechir.com](https://atbechir.com) · [LinkedIn](https://www.linkedin.com/in/ahmed-taleb-bechir-97a7301a4) · [Substack](https://atalebbechir.substack.com)
