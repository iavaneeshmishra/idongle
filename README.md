# AI Growth Copilot for Shopify (SEM + SMM)

This repository now contains a **build blueprint** for a Shopify app that is intentionally focused on:

- **AI-powered Search Engine Marketing (SEM)**
- **AI-powered Social Media Marketing (SMM)**

The product idea: a merchant installs the app, connects ad/social channels, and gets AI-generated campaigns, optimization recommendations, and weekly growth actions.

---

## 1) Product concept

### Core promise
Help Shopify merchants increase profitable traffic and conversions using AI-generated and AI-optimized:

1. **Google Ads search campaigns** (keywords, ad groups, RSAs, budget split)
2. **Meta social campaigns** (creative angles, audiences, copy variants)
3. **Organic social calendar** (post ideas, captions, hashtags, UTM tags)
4. **Cross-channel insights** (which campaigns actually produce revenue)

### Target users
- Solo founders and small Shopify brands
- DTC operators with limited marketing resources
- Agencies managing multiple Shopify stores (Phase 2)

---

## 2) Recommended stack

- **Shopify app**: Remix + Shopify App Bridge + Polaris
- **Backend runtime**: Node.js/TypeScript
- **Database**: Postgres (via Prisma)
- **Queue/worker**: BullMQ + Redis (for async AI generation & sync jobs)
- **AI provider**: OpenAI Responses API (structured JSON outputs)
- **Channel APIs**:
  - Google Ads API
  - Meta Marketing API
  - Optional: TikTok Ads API (phase 2)
- **Tracking + analytics**:
  - Shopify Orders/Products/Customers via Admin API
  - UTM normalization + attribution tables

---

## 3) MVP feature scope

### A. Shopify onboarding
- OAuth install flow
- Merchant onboarding wizard:
  - Brand voice/profile
  - Product catalog sync
  - Target countries/languages
  - KPI selection (ROAS, CAC, revenue)

### B. SEM module (Google)
- AI keyword clustering by product/category intent
- AI campaign drafts:
  - Campaign names, ad groups, keyword themes
  - RSA headlines/descriptions
  - Negative keyword suggestions
- Budget recommendation engine
- Weekly optimization suggestions from performance data

### C. SMM module (Meta + organic)
- AI creative briefs from product data and brand voice
- Ad copy variant generation by persona/funnel stage
- Organic social calendar generator (7/14/30-day plans)
- Hashtag and hook recommendation

### D. Performance copilot
- Unified dashboard: spend, clicks, conversions, revenue, ROAS
- AI “what changed” summaries each week
- Suggested actions with expected impact estimates

---

## 4) Data model (first pass)

Use these tables/entities as the baseline:

- `shops` (shop domain, plan, timezone)
- `shop_settings` (voice, goals, geos, channels enabled)
- `products_snapshot` (title, price, tags, inventory, collections)
- `channel_connections` (google/meta auth metadata)
- `campaigns` (channel, status, objective, budget)
- `ad_groups` / `ad_sets`
- `ad_creatives` (copy variants, media references)
- `performance_daily` (spend, clicks, conversions, revenue)
- `attribution_events` (utm source/medium/campaign + order linkage)
- `ai_generations` (prompt version, output JSON, approval status)
- `recommendations` (priority, rationale, projected uplift)

See `docs/mvp-roadmap.md` for phased schema and execution milestones.

---

## 5) API surface (app backend)

Suggested internal routes:

- `POST /api/onboarding/complete`
- `POST /api/sync/shopify/products`
- `POST /api/channels/google/connect`
- `POST /api/channels/meta/connect`
- `POST /api/ai/sem/generate-campaign`
- `POST /api/ai/smm/generate-calendar`
- `POST /api/ai/recommendations/run`
- `GET /api/dashboard/summary`
- `GET /api/dashboard/channel-breakdown`

All AI generation endpoints should:
1. Validate inputs against JSON schema
2. Call LLM with strict output schema
3. Persist generation results for audit/versioning
4. Return both machine-readable payload and human explanation

---

## 6) Suggested build order (8-week MVP)

1. **Week 1-2**: Shopify auth, onboarding, product sync
2. **Week 3**: SEM campaign generator (draft-only mode)
3. **Week 4**: SMM calendar + ad copy generator
4. **Week 5**: Dashboard + basic attribution plumbing
5. **Week 6**: Recommendation engine (rule + AI hybrid)
6. **Week 7**: Approval workflows + human-in-the-loop
7. **Week 8**: QA, rate-limit handling, billing, launch prep

Detailed roadmap: `docs/mvp-roadmap.md`.

---

## 7) Implementation starter checklist

- [ ] Create Shopify app scaffold (`npm init @shopify/app@latest`)
- [ ] Add Prisma models for core entities
- [ ] Add queue workers for sync and AI tasks
- [ ] Build onboarding wizard in Polaris
- [ ] Add Google & Meta connection screens
- [ ] Implement first AI prompts (see `docs/ai-marketing-prompts.md`)
- [ ] Build dashboard cards (ROAS, CAC, revenue by channel)
- [ ] Add merchant approval before publishing campaign changes
- [ ] Add error logging + retry policies
- [ ] Add subscription billing plans

---

## 8) AI quality and safety guardrails

- Force JSON outputs with explicit schema
- Add profanity/compliance filters for ad copy
- Keep prompt versions stored and reviewable
- Add confidence score + “needs review” flag
- Never auto-publish ads in MVP without user approval
- Add cost controls: generation quotas + caching

---

## 9) Next actions you can do immediately

1. Scaffold the app with Shopify CLI.
2. Implement onboarding + product sync.
3. Add one narrow AI endpoint: `generate SEM campaign draft for one collection`.
4. Render output in a review UI with approve/edit/reject.
5. Instrument with outcome tracking and weekly recommendation cron.

If you want, the next step can be creating the initial **Prisma schema + Remix route skeleton** directly in this repo.

---

## 10) Visual preview (build so far)

A lightweight static preview of the merchant dashboard is included at:

- `preview/index.html`

Run locally:

```bash
cd preview
python3 -m http.server 4173
```

Then open: `http://localhost:4173`


## 11) Open source direction (new)

Given that search engine marketing performance is heavily affected by core algorithm and policy updates, this project is now explicitly designed as an **open-source product** so the community can adapt quickly.

What changes with this direction:

- Core-update monitoring becomes a first-class subsystem.
- Recommendation logic is transparent and community-reviewable.
- Merchants can self-host and audit AI recommendation behavior.
- Faster adapter updates when search/social platforms change.

See `docs/open-source-operating-model.md` for architecture and governance details.
