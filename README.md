# Outbound Studio Hub

**Lean, Federated, High-Quality Client Acquisition System**  
Version 1.0 — May 2026

One clean visual platform with **strictly separated** Build and Audit agents.

### Core Principle
**No theater.**  
Builder executes.  
**Auditor owns final approval** — and must verify a real live Vercel deployment using `deploy-pipeline` + `vercel_verify.py` (full byte-count check on every asset).

### Key Components
- **Visual Dashboard**: Real-time activity, agent topology, live logs, and campaign metrics (powered by JAW).
- **Federated Agents**:
  - Orchestrator — routes tasks + maintains shared ledger
  - Builder — runs design + deploy
  - Auditor — runs audit + live verification (final sign-off)
- **Vertical Asset Library**: Every approved build is automatically saved to `/verticals/{type}/` so the system compounds efficiency over time.
- **Portable Skills**: All logic packaged as clean `SKILL.md` + scripts (Hyperagent + consensus format).

### Quick Start
1. Fork this repo
2. Connect to your JAW instance (or run standalone)
3. Register `outbound-studio-orchestrator` as a custom agent
4. Trigger via webhook, Telegram, or Slack

See `CHARTER.md` for full roles, quality gates, and guidelines.

**Connected Services**: GitHub + Vercel (ready for verified deploys)