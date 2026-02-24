# Deployment Arenas for the Open-Source SEM/SMM Shopify Copilot

Use a staged rollout model so update-ingestion and recommendation quality can be validated safely.

## 1) Local Developer Arena

**Purpose**
- Fast iteration on connectors, prompts, and UI.

**Stack**
- Docker Compose for Postgres + Redis.
- App on localhost.
- Shopify dev store and test ad/social accounts.

**Use for**
- Day-to-day feature work.
- Prompt contract changes.
- Parser fixes for search/social updates.

## 2) Preview Arena (Per PR)

**Purpose**
- Ephemeral environment to review each pull request.

**Stack**
- Branch-based deploy (Vercel/Render/Fly.io/Kubernetes namespace).
- Seeded test dataset.

**Use for**
- Product/design review.
- QA verification of UI and API changes.
- Regression checks before merge.

## 3) Shared Staging Arena

**Purpose**
- Production-like integration testing.

**Stack**
- Managed Postgres + Redis.
- Real background workers and cron jobs.
- Sandbox channel credentials.

**Use for**
- End-to-end onboarding checks.
- Search/social update ingestion verification.
- Recommendation quality evaluation.

## 4) Canary Production Arena

**Purpose**
- Low-risk rollout to a small merchant cohort.

**Stack**
- Same infra as production.
- Feature flags + cohort targeting.

**Use for**
- Validate performance and recommendation impact.
- Catch policy/connector issues early.

## 5) General Production Arena

**Purpose**
- Full merchant availability.

**Stack**
- Multi-region app deployment.
- HA database setup + backups.
- Centralized logging/alerting.

**Use for**
- Stable releases.
- Routine patch/minor updates.

## 6) Hotfix Arena (Core Update Response)

**Purpose**
- Rapid response to major search/social algorithm or policy shifts.

**Stack**
- Dedicated release branch pipeline.
- Accelerated tests focused on ingestion + recommendations.

**Use for**
- Emergency parser updates.
- Immediate rule/prompt mitigation rollouts.

## Suggested Platform Options by Arena

- **Quick start OSS**: Render + Neon + Upstash.
- **Balanced**: Fly.io + Supabase + Upstash.
- **Enterprise/K8s**: EKS/GKE/AKS + RDS/Cloud SQL + ElastiCache/MemoryStore.

## Minimum Promotion Gates

- Migrations pass and rollback tested.
- Queue jobs healthy for 24h in staging.
- Search/social update ingestors produce valid normalized records.
- Recommendation endpoints meet schema + latency budgets.
- Alerting dashboards green before promotion.
