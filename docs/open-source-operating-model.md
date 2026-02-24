# Open Source Operating Model (Core-Update-First SEM + SMM)

This project is now positioned as an **open-source marketing copilot** for Shopify teams.

## Why open source here

Search and social ecosystems change constantly (algorithm updates, policy changes, platform feature shifts). Open source makes the adaptation loop faster:

- Community can submit parser/adapter updates quickly.
- Maintainers can ship transparent rule changes.
- Merchants can self-host and inspect logic used in recommendations.

## Core-update-first architecture (search + social)

Add dedicated update intelligence subsystems for both SEM and SMM:

1. **Update Ingestors**
   - Pull from official/public sources (search blogs, social platform policy/changelog feeds, ads docs).
   - Normalize entries into channel-specific update tables.
2. **Impact Classifier**
   - Label probable impact area.
   - Search examples: crawl/indexing, content quality, structured data, ads policy.
   - Social examples: ranking distribution shifts, ads review policy, creative format changes, targeting limits.
3. **Merchant Relevance Scoring**
   - Map updates to each shop profile (catalog, geo, vertical, traffic mix, channel dependency).
4. **Action Generator**
   - Produce channel-specific checklists + experiments for impacted merchants.
5. **Verification Loop**
   - Compare pre/post metrics and mark recommendations as validated, neutral, or regressive.

## Suggested additional tables

### Shared
- `update_impacts` (update_id, channel, impact_type, severity, confidence)
- `shop_update_relevance` (shop_id, update_id, relevance_score, reasoning)
- `update_actions` (shop_id, update_id, action, status, outcome)

### Search-specific
- `search_engine_updates` (source, title, published_at, normalized_payload)

### Social-specific
- `social_platform_updates` (platform, source, title, published_at, normalized_payload)
- `social_update_constraints` (update_id, audience_constraints, creative_constraints, policy_risk_level)

## Open source governance

- `main` branch protected with required review.
- `CODEOWNERS` for critical modules (attribution, campaign publishing, billing, policy ingestion).
- Security disclosure process and dependency scanning enabled.
- Prompt/template versioning required for all AI recommendation changes.

## Community contribution lanes

- **Connector lane**: add/update channel integrations.
- **Rules lane**: improve heuristic recommendations.
- **Prompt lane**: improve generation quality within JSON contracts.
- **Policy lane**: maintain update parsers and impact classifiers for search + social changes.
- **UI lane**: improve Polaris/UX workflows for approvals and reporting.

## Release strategy

- Weekly patch releases for bug fixes and connector/update-parser updates.
- Bi-weekly minor releases for feature additions.
- Emergency hotfix path for major search/social policy changes.
