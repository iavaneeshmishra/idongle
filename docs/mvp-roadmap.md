# MVP Roadmap: Shopify AI SEM + SMM App

## Phase 0 — Foundation (Week 1)

### Goals
- Stand up Shopify app shell and database.
- Define event logging + analytics baseline.

### Deliverables
- Shopify OAuth install flow complete.
- Merchant record + shop settings persisted.
- Product snapshot sync job (manual trigger).

### Exit criteria
- New merchant can install app and see synced catalog.

---

## Phase 1 — SEM Draft Generator (Week 2-3)

### Goals
- Generate high-quality Google Ads drafts from catalog data.

### Deliverables
- Prompt pipeline for keyword cluster suggestions.
- RSA copy generation endpoint with schema validation.
- Draft campaign review UI in admin app.

### Metrics
- Time-to-first-campaign draft < 5 minutes.
- Merchant accepts/edits at least one generated campaign.

---

## Phase 2 — SMM Assistant (Week 4)

### Goals
- Produce social-ready content plans and paid copy variants.

### Deliverables
- 14-day calendar generator (themes + captions + hashtags).
- Persona-based ad copy variants (prospecting/retargeting).
- UTM tag generation utility.

### Metrics
- Calendar generation < 60 seconds.
- At least 10 usable posts per merchant generated.

---

## Phase 3 — Cross-channel Analytics (Week 5-6)

### Goals
- Tie ad/social activity to Shopify outcomes.

### Deliverables
- Daily ingest of spend/click/conversion from channel APIs.
- Unified dashboard with channel comparison.
- AI weekly narrative summary.

### Metrics
- Dashboard data freshness < 24h.
- Weekly summary successfully generated for active shops.

---

## Phase 4 — Recommendations + Workflow (Week 7-8)

### Goals
- Turn analytics into prioritized actions.

### Deliverables
- Recommendation scoring model (impact x confidence x effort).
- Action center with approve/reject/status.
- Basic billing + usage limits.

### Metrics
- 3+ recommendations per shop/week.
- Recommendation acceptance rate tracked.

---

## Non-functional requirements

- Rate-limit aware API clients with retries/backoff.
- Queue isolation by job type (sync vs AI generation).
- PII minimization and secure token storage.
- Full audit trail for AI-generated outputs.

