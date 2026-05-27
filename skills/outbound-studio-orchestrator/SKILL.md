---
name: outbound-studio-orchestrator
description: Master orchestrator for the full Outbound Studio pipeline — prospect high-probability SMBs (high Google rating + poor digital presence), run AEO/SEO audits, qualify via gap scoring, auto-generate personalized pitch HTMLs and modern demo sites, deploy via GitHub/Vercel, and close with tracked outreach. Activate for end-to-end campaigns or any sub-stage. Always loads design-foundation + elite-orchestrator first. Triggers include outbound campaign, find clients, audit prospects, build pitch site, deploy demo, run studio workflow.
---

# Outbound Studio Orchestrator

This skill turns the fragmented skills (site-audit-suite, design-foundation + variants, deploy-pipeline) + the Ventura-style pitch pattern into a deterministic, multi-agent, self-improving pipeline that delivers measurable client acquisition results. It eliminates manual handoffs, forgotten prerequisites, and context loss.

**Core Principle (2026 best practice)**: Supervisor + narrow specialists with structured JSON handoffs, shared state ledger, guardrails, and post-campaign evolution. Firecrawl is the preferred web data layer for all scraping/auditing.

## Mandatory Pre-Loads (Never Skip)
1. Load `design-foundation` (universal baseline).
2. Load `elite-orchestrator` (for all complex reasoning, verification, decomposition).
3. Load `site-audit-suite` when auditing.
4. Load `deploy-pipeline` when shipping.

## Full Pipeline (Default Flow — Execute in Order)
**State Ledger**: Maintain `/tmp/outbound_studio_ledger.json` with keys: prospects (list), current_prospect, audit_results, pitch_data, deployed_url, email_payload, campaign_metrics. Update after every major step. Persist across turns.

1. **Prospecting (Research Specialist)**
   - Use Firecrawl search or web_search for SMBs in target niche (e.g., "lawn care West Houston" "4.8+ stars" "50+ reviews").
   - Filter for high-probability: Google rating ≥4.5 + ≥30 reviews + no/poor website (quick llms.txt/schema/robots check via audit or Firecrawl).
   - Enrich with business name, website, phone, services from Google Business Profile or site.
   - Output: Structured list of 5–20 prospects with "AEO Opportunity Score" estimate.

2. **Audit & Qualify (Auditor + Qualifier)**
   - For each prospect: Call site-audit-suite (enhanced with Firecrawl for rawHtml + structured extraction of schema, llms.txt, robots, on-page).
   - Compute/confirm AEO Gap (100 - AEO Score). High gap + high rating = hot lead.
   - Qualify: If AEO Gap ≥45 and rating ≥4.5 → proceed. Log why disqualified.
   - Structured output per prospect: full audit JSON + qualification decision + sales hooks (missing llms.txt, no schema, no AI crawler allowlist, etc.).

3. **Pitch & Demo Generation (Pitch Specialist + Designer)**
   - Build `pitch_manifest.json` from audit + business data (use Ventura template as base).
   - Generate customized pitch HTML (stats, gaps, break-even math, urgency "X days live", AEO wins, pricing $1,997 + optional $497/mo retainer).
   - For demo site: Select LANDING PAGE variant (or appropriate), enforce design-foundation dials (DESIGN_VARIANCE 8 for asymmetric, VISUAL_DENSITY 3–4), generate modern responsive site with real photos (or placeholders), LandscapeService schema, llms.txt, robots.txt AI allowlist.
   - Run design_variant_check.py and design_preflight.py automatically — fix violations before proceeding.
   - Output: pitch.html + demo_site/ folder ready for deploy.

4. **Deploy & Verify (Deploy Specialist)**
   - Use deploy-pipeline (or individual scripts): detect_assets → github_commit (atomic, byte-verify) → vercel_deploy (git-trigger or inline) → vercel_verify (full byte check on all assets + live URL).
   - Resolve repo/project via explicit + thread context + recent activity (resolve_target.py).
   - Auto-upload images to Cloudinary/ImageKit if referenced and credentials present.
   - Output: live_url, commit_sha, verification JSON (ok: true required).

5. **Outreach & Close (Closer)**
   - Build JAW_x operational email payload via send_email.py (personalized with audit gaps, AEO Gap number as hook, demo link, pricing, 7-day urgency).
   - Fire GMAIL_SEND_EMAIL (or equivalent).
   - Log opens/replies in ledger. Auto-schedule follow-ups (3/7/14 days) with new value (updated audit, competitor comparison).
   - Track campaign_metrics: sent, opened, replied, qualified, closed.

## Structured Handoffs (Mandatory)
Every step outputs strict JSON to the ledger. Never pass free text. Example prospect record:
```json
{
  "name": "Ventura Landscape",
  "website": "https://...",
  "rating": 4.9,
  "reviews": 138,
  "aeo_gap": 77,
  "audit_json_path": "/tmp/audit_ventura.json",
  "sales_hooks": ["No llms.txt", "No LandscapeService schema", "No AI crawler allowlist"],
  "status": "qualified"
}
```

## Guardrails & Error Recovery (Elite-Orchestrator Patterns)
- Every verification gate (audit complete, design preflight pass, deploy byte-verify ok, live URL loads) must pass or halt with specific recovery action.
- On Firecrawl 403/timeout: Note "partial data — homepage blocked" and use robots/llms.txt only (still valid sales hook).
- On deploy failure: Retry force-deploy or inline-files; surface exact error.
- Human-in-loop: For final close email approval or pricing negotiation.
- Token budget: Compact ledger after each stage.

## Self-Evolution (Post-Campaign — Always Run)
After every 5–10 prospects or lost deal:
- Analyze ledger: Which hooks converted? Which audits were inaccurate? Pitch win rate?
- Propose updates: New prompt for Pitch Specialist, new filter for Prospecting, new reference in site-audit-suite.
- Create or update sub-skills (e.g., "lawn-care-pitch-template").
- Log learnings to references/evolution_log.md.

## When to Use Sub-Stages Only
- "Audit this site" → steps 2 only.
- "Build pitch for Ventura" → steps 3 + 4.
- "Deploy this HTML" → deploy-pipeline directly.
- Always prefix with "outbound-studio-orchestrator" for full context.

## Integration Notes
- Firecrawl: Preferred for all HTML/raw data (use /scrape with formats=["rawHtml","markdown","screenshot@fullPage"] + structured extraction for schema/llms.txt).
- Hyper Agents env: Scripts in skill directories are executable. Credentials from env or thread context.
- GitHub repo (jGPT-Automated/outbound-studio): Store generated pitches/demos here for version history and easy client sharing.

This orchestrator removes 80% of the current friction by making the pipeline explicit, auditable, and self-improving. Run it on any campaign and it will produce consistent, high-conversion results like the Ventura example — at scale.