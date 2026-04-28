# Surfaced — Spec Clarification Tool

## What this is
Surfaced is a spec quality and cross-functional alignment tool that analyses software tickets before AI agents write code, flags hidden assumptions and judgment calls, and facilitates resolution between PMs and developers. It lives at the PM tool layer — Linear first, Jira v2.

**It is NOT a training platform.** It is a workflow quality tool that improves spec clarity as a byproduct of use. Never frame it as training or checking — it surfaces what was always there.

## Architecture
- **Analysis API** — standalone Node/TypeScript service. Processes ticket content, returns structured assumption flags and role-aware output. Standalone so it survives platform changes (Linear pivoting doesn't kill the core product).
- **Linear plugin** — distribution surface for v1. Hooks into Linear via webhook + issue comments at minimum; sidebar panel if/when Linear app review is completed.
- **Web dashboard** — manager view, team trends, setup wizard. Next.js.
- **Shared types/schemas** — used across packages.

Monorepo structure:
```
/api        — analysis engine (Express or Fastify, TypeScript)
/plugin     — Linear integration (webhook listener, comment writer)
/web        — dashboard + onboarding setup wizard (Next.js)
/shared     — shared TypeScript types and Zod schemas
```

## BYOK Model (critical constraint)
v1 is BYOK-only. The user supplies their API key; our server makes the AI call on their behalf. This means:
- Never store API keys beyond the request lifecycle
- Always show token/cost estimates before analysis runs
- Cost display uses character-count estimates + per-model ranges (not precise tokenisation)
- Model selection dropdown with editable cost-per-1K-tokens field — do NOT hardcode pricing tables as constants (provider pricing changes frequently)
- Support at minimum: GPT-4o, Claude Sonnet, Gemini Pro

## Key product decisions
- **Role-aware output:** same ticket analysis, two views. PM view surfaces assumptions about user needs and acceptance criteria. Dev view surfaces technical judgment calls and missing constraints. Both views generated in one API call, returned as separate structured objects.
- **Discussion layer:** flagged assumptions become resolvable questions. PM and dev can mark questions as resolved with a brief answer. Resolution state is stored and visible to the manager dashboard.
- **Pre-analysis setup window:** before first run, user selects ticket scope (active only / by status / by date cutoff / manual). Show estimated ticket count + character volume + per-model cost range before confirming.
- **Dashboard primary metric:** "Estimated staff time saved" displayed as a range (e.g. "$340–$610 avoided rework this month"). Input variables (avg rework time, loaded hourly rate) are set by the user during onboarding. Never show a false-precision single number.

## Onboarding psychology (affects copy and UX decisions)
Week one will look bad — the tool catches assumptions that were previously invisible. All copy and UI must frame this as "establishing your baseline" not "you write bad specs." Key principle: the MRI didn't cause the problem.
- First dashboard metric must be forward-looking (assumptions resolved) not a grade (completeness score)
- PM and dev get their role-aware views simultaneously, not top-down via manager
- Week two often surfaces MORE assumptions (team using tool properly) — dashboard must explain this proactively

## Data & privacy
- Free tier: data retention mandatory, disclosed at signup
- Paid tier: opt-out included
- Anonymised aggregates used for product improvement only
- GDPR legal review required before launch (open question — do not build permanent storage until this is resolved)
- Fred's server intercepts only its own analysis calls, not third-party tool traffic

## Linear integration
- Linear workspace: https://linear.app/surfacedapp/
- v1 minimum viable: webhook listener + issue comments (no app store submission required)
- v2 target: sidebar panel (requires Linear app review process — research timeline before committing)
- Use Linear SDK (@linear/sdk) not raw API calls

## Tech stack preferences
- Runtime: Node.js via Volta
- Language: TypeScript throughout
- API framework: Fastify preferred (performance, TypeScript-first) — confirm before scaffolding
- Frontend: Next.js (App Router)
- Database: PostgreSQL — use Prisma ORM
- Validation: Zod (shared schemas between API and web)
- Testing: Vitest
- Package manager: npm

## Current status
- PRD complete (see project_surfaced.md and Surfaced - PRD v1.0.docx)
- Repo initialised, no code yet
- Linear workspace created: linear.app/surfacedapp
- Open before building: Linear integration mechanics (webhook vs sidebar — research required), GDPR anonymisation methodology

## What NOT to build yet
- Permanent ticket data storage (GDPR unresolved)
- Linear sidebar panel (app review timeline unknown)
- Improvement suggestions feature (P2 — needs ticket volume data first)
- Jira integration (v2)
