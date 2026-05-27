# Outbound Studio Charter

**Version**: 1.0 (Lean)  
**Date**: May 27, 2026

## Core Rule (Non-Negotiable)
**No Theater.**  
The Builder can propose and execute.  
Only the **Auditor** can mark work complete — and it **must** verify a real live Vercel URL using `deploy-pipeline` + `vercel_verify.py` with full byte-count validation on every asset.

## Federated Agent Roles

| Agent          | Ownership                          | Primary Skills                              | Final Authority      |
|----------------|------------------------------------|---------------------------------------------|----------------------|
| Orchestrator   | Task routing + shared state ledger | `outbound-studio-orchestrator`              | Routes only          |
| Builder        | Design + Deploy execution          | `design-foundation`, `design-ui-variants`, `deploy-pipeline` | Proposes only        |
| Auditor        | Verification + Quality Gate        | `site-audit-suite`, `vercel_verify.py`, Firecrawl | **Final sign-off**   |

## Quality Gate Process
1. Builder completes design + deploy
2. Auditor is automatically triggered
3. Auditor runs full audit + live Vercel verification
4. Only if `ok: true` + all assets load correctly → Auditor approves and updates vertical library

## Vertical Asset Library (Compounding Efficiency)

```
/verticals/
  lawn-care/
    pitch-template.html
    aeo-rules.md
    verified-builds/
  barbershop/
  pressure-wash/
  restaurant/
```

Every successful, Auditor-approved build is automatically committed here with metadata (AEO Gap, close status, learnings).

## Invocation Methods
- Webhook (primary)
- Telegram
- Slack
- Website thread

## Memory & Portability
- Live state: JAW database + shared ledger
- Versioned context: `/context/judgements.md`, `/context/evolution-log.md`
- All skills remain standalone and reusable across any Hyperagent/JAW environment

## Success Metrics
- AEO Gap → Reply Rate → Close Rate correlation
- % of builds passing live Vercel verification on first attempt
- Reduction in time-to-first-verified-build per vertical

This charter ensures quality, clarity, and continuous improvement.