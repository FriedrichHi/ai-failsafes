---
name: Surfaced — Spec Clarification Tool
description: Fred's business idea in active development. Spec quality + cross-functional alignment tool for teams using AI coding tools. Full decisions on product, ICP, pricing, metrics, features, onboarding, and pre-analysis setup.
type: project
last_updated: 2026-04-28
---
**Project name: Surfaced — Spec Clarification Tool** (renamed April 2026 from "Developer Retraining AI").
**Working product name: Surfaced** (chosen April 2026).
**GitHub repository:** https://github.com/FriedrichHi/surfaced (created April 2026 — private or not yet initialised at time of recording).
**Workspace folder:** `C:\Users\fried\Proton Drive\friedrich.hirler\My files\Fred\Work\1 - Own Projects\Surfaced App` (moved and renamed April 2026 from the old nested path under "Dev Trainer AI"). Selected over SpecManifest, SpecBrief, Preflight, Premise, Brief, Quorum after full brand/SEO/domain sweep. All alternatives were either taken, trademark-conflicted, or SEO-polluted. Surfaced is clear across all checked dimensions — no brand collision found. Domain variants (surfaced.ai, surfaced.io, getsurfaced.com) not yet formally checked but name space appears open.

> **Note for future sessions:** This file in the workspace folder is the canonical project memory. Update this file during sessions when decisions are made. The AppData copy is a backup only.

A spec quality and cross-functional alignment tool that surfaces hidden assumptions in software tickets before AI agents write code. Teaches through real work, not simulated exercises.

**Core mechanic:** AI agent flags every judgment call it had to make when interpreting a spec — showing exactly where intent was ambiguous and the downstream consequence.

**Why:** AI coding tools have moved the engineering bottleneck upstream to spec writing and agent supervision. Mid-level devs are hardest to retrain. Companies feel this as an operational problem (rework, review bottleneck, PM-dev misalignment).

**What it is NOT:** A training platform. A workflow quality tool that teaches as a byproduct.

## Product Decisions

**Insertion point:** PM tool layer — Linear first (tech-savvy early adopters), Jira v2.
**Architecture:** Standalone analysis API (survives platform changes) + Linear plugin as distribution surface. MCP server as v2.
**BYOK:** v1 is BYOK-only (user supplies API key, Fred's server makes the call). Eliminates AI cost risk. Reduces running costs to ~$100–150/month infrastructure.
**Data:** Fred's server intercepts input/output of its own analysis calls (not third-party tools). Free tier: mandatory retention (disclosed). Paid: opt-out included. Anonymised aggregates for product improvement. Legal review of anonymisation needed before launch.

## ICP

**Primary buyer:** Engineering Manager / CTO / VP Product at 20–200 person tech company already using AI coding tools, using Linear, feeling the spec quality pain.
**Primary users:** PMs/POs (user need clarity) + Developers (technical constraints) — same analysis, two role-aware views.
**Secondary:** Solopreneurs/individuals on free/pro tier. Drive distribution and data, not revenue decisions.

## Pricing (v1, BYOK only)

- **Free:** 50 analyses/month, single user, BYOK, core analysis only, data collection on
- **Individual Pro:** $5/month OR $79 one-time lifetime (launch only — first 90 days or 150 customers). Role-aware output, improvement suggestions (toggleable, token warning), personal quality trend, privacy opt-out.
- **Team:** $20/month base includes 4 seats, $5/seat additional. Manager dashboard, team quality trends, recurring gap analysis.
- **Enterprise:** Custom — v2. Jira, SSO, SLAs.

## Onboarding & Baseline Framing

Critical UX principle: week one will surface more assumptions than any subsequent week, because the team is seeing previously invisible debt. The risk is the manager who bought Surfaced has to show this to their team and it reads as an indictment. The framing must be established *before* any analysis runs, not after.

**Psychological reframe to establish:** "These findings don't mean you've been doing something wrong. They mean you can now see something that was always there." The MRI didn't cause the problem.

**Three moments that must get this right:**

1. **Pre-analysis interstitial** (between "connected to Linear" and "first analysis runs"): Set context explicitly before results appear. Brief, factual, non-patronising. E.g. "Every team we've worked with has hidden assumptions in their tickets — that's structural, not a reflection of your team. What you're about to see is your starting point."

2. **First dashboard view:** Lead with forward momentum, not a score. First number visible should be progress-oriented ("X assumptions resolved before first commit") not a grade (completeness %). Trend line appears immediately even when flat — a flat line at the start is a beginning, not a failure.

3. **Role-aware simultaneous reveal:** Manager and team should receive their respective views at the same time, not top-down. PM sees "3 assumptions your developer needs answered." Dev sees "3 questions your PM hasn't resolved." Both true. Neither an accusation. Prevents tool feeling like surveillance.

**Week two problem:** Volume of flagged assumptions often *increases* in week two as the team starts using the tool properly. Must proactively explain this in the product before it happens or managers churn thinking the tool is broken. Dashboard must tell the story: more assumptions surfaced + higher resolution rate = progress. Don't leave this for the user to infer.

**Onboarding UX detail (pending):** Users should be able to input their avg rework time and loaded hourly rate during setup so the primary dashboard metric reflects their actual numbers rather than industry defaults.

## Pre-Analysis Setup Window (First Run)

BYOK users may have API session limits, rate constraints, or cost sensitivity — they need control over scope before any tokens are spent. A setup window must appear before the first analysis run.

**Ticket selection options:**
- Active tickets only (in-progress/current sprint)
- Tickets filtered by status (user selects from their Linear statuses)
- Tickets created after a cutoff date (user sets date)
- Manual selection (cherry-pick specific tickets)

**Token/cost transparency (v1 approach):** Do not build a precise token counter — tokenisation varies by model and content, and false-precision estimates damage trust at the worst moment. Instead show ticket count + estimated character volume, with a per-model cost range. E.g. "47 tickets (~84,000 characters). Estimated cost: $0.05–0.15 with GPT-4o."

**Model cost configuration:** Show a dropdown of common models (GPT-4o, Claude Sonnet, Gemini Pro etc.) with pre-filled typical cost per 1K tokens. Make the cost field editable so users on custom/negotiated rates or self-hosted models can override. Do NOT hardcode a pricing table as a fixed constant — provider pricing changes frequently. Treat the defaults as user-editable hints, not authoritative figures. Consider a lightweight "last updated" note next to defaults so users know to verify against their provider.

**Volume guidance (important):** A higher input of tickets improves the quality of pattern detection and enables better improvement suggestions. Users opting for narrow scope should be informed: "Analysing more tickets gives Surfaced more signal to identify recurring patterns in your team's workflow. A broader initial run improves suggestion quality over time." Frame as an opt-in benefit, not a requirement. Suggestion quality feature (P2) is explicitly dependent on sufficient ticket volume — document this dependency in onboarding copy.

**How to apply:** Setup window is P0, ships with first Linear integration. Cost estimate display is P0 given BYOK architecture. Volume guidance copy is P1 (can be added post-launch but should be designed in from the start).

## Features (v1 Priority)

P0: Spec analysis engine, BYOK config, Linear integration, pre-analysis setup window (ticket scope selector + token cost estimate)
P1: Role-aware output (PM vs Dev views), discussion layer (resolvable questions), manager dashboard, data controls, volume guidance copy in onboarding
P2: Improvement suggestions (toggleable, paid only — requires sufficient ticket volume), personal quality trend

## Success Metrics

**Primary (manager dashboard headline):** Estimated staff time saved (hours + $ value) = assumptions resolved before first commit × avg rework time × loaded hourly rate. Display as a **range**, not a point estimate — both inputs (avg rework time, loaded hourly rate) are estimates. E.g. "Estimated $340–$610 in avoided rework this month." Range width reflects uncertainty in the model, not imprecision in the data. Narrow the range as the team accumulates actual rework data over time.

**Supporting:** Spec completeness score at commit time, recurring gap patterns (coaching metric), team quality trend month-over-month.

**Token cost display (dashboard):** Show API cost of running Surfaced analyses as a range for the same reason — tokenisation and model pricing vary. E.g. "Analysis cost this month: ~$1.20–$2.40." This is a supporting metric only, never a headline. Kept visible so BYOK users can track spend against their own key.

**Explicitly avoided:** Time to first code (will show negative — asking for clarification slows start), token savings as headline (too small vs subscription cost).

## Competitive Landscape

- **Linear** (HIGH THREAT): Declared "issue tracking is dead" March 2026, pivoting to agent management with native spec/agent features. Plugin strategy is risky — hence standalone API architecture.
- **GitHub Spec Kit** (MEDIUM): Free open-source spec review toolkit, no PM integration, no real-time feedback.
- **BMAD-METHOD** (LOW-MEDIUM): Open-source SDLC framework, requires full workflow adoption, not workflow adoption, not embedded.
- **Atlassian Intelligence** (MEDIUM): Generic AI, slow mover, Premium/Enterprise only.
- **ClickUp Brain** (LOW): General AI, supports MCP (potential integration channel).
- **Braintrust/Maxim/LangSmith** (LOW): Post-execution observability, different insertion point.
- **SpecPilot** (LOW): Open-source solo portfolio project. Generates specs from scratch (blank page problem), no PM tool integration, no discussion layer, no commercial intent. Not a competitor — different problem.

## Work Completed

- Problem statement ✓
- Competitor analysis ✓
- ICP definition ✓
- Feature plan ✓
- Pricing structure ✓
- Success metrics ✓
- PRD v1.0 document created ✓ (Surfaced - PRD v1.0.docx in workspace)
- Product name decided: Surfaced ✓
- Onboarding & baseline framing principles ✓
- Pre-analysis setup window specified ✓
- Workspace folder organised and renamed ✓
- Project memory moved to portable workspace file ✓

## Open Questions (in progress)

1. Product name — RESOLVED: Surfaced
2. Baseline framing — RESOLVED: see Onboarding section above
3. Linear integration mechanics — pending
4. GDPR anonymisation scope — pending

## Next Steps

- Resolve questions 3 and 4 (Linear integration mechanics, GDPR)
- Tech stack decisions (Node/TypeScript, DB, hosting)
- Write project CLAUDE.md for the repository
- Set up Linear developer workspace + test fixtures
- GTM strategy
- Business plan

**Why:** Need to confirm Q3 and Q4 before building. GTM especially important given Linear's March 2026 pivot means the window for Linear-first distribution is time-sensitive.
