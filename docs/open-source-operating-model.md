# Open Source Operating Model (Core-Update-First SEM/SMM)

This project is now positioned as an **open-source marketing copilot** for Shopify teams.

## Why open source here

Search and social ecosystems change constantly (core algorithm updates, policy changes, platform feature shifts). Open source makes the adaptation loop faster:

- Community can submit parser/adapter updates quickly.
- Maintainers can ship transparent rule changes.
- Merchants can self-host and inspect logic used in recommendations.

## Core-update-first architecture

Add a dedicated subsystem focused on search engine changes:

1. **Update Ingestors**
   - Pull from official/public sources (e.g., search central blogs, policy docs, changelogs).
   - Normalize entries into `engine_updates`.
2. **Impact Classifier**
   - Label updates by probable impact area: crawl/indexing, content quality, structured data, ads policy, shopping surfaces.
3. **Merchant Relevance Scoring**
   - Map updates to a shop profile (catalog, geo, vertical, traffic mix).
4. **Action Generator**
   - Produce actionable checklists + experiment ideas for impacted merchants.
5. **Verification Loop**
   - Compare pre/post metrics, then mark recommendations as validated, neutral, or regressive.

## Suggested additional tables

- `engine_updates` (source, title, published_at, normalized_payload)
- `update_impacts` (update_id, impact_type, severity, confidence)
- `shop_update_relevance` (shop_id, update_id, relevance_score, reasoning)
- `update_actions` (shop_id, update_id, action, status, outcome)

## Open source governance

- `main` branch protected with required review.
- `CODEOWNERS` for critical modules (attribution, campaign publishing, billing).
- Security disclosure process and dependency scanning enabled.
- Prompt/template versioning required for all AI recommendation changes.

## Community contribution lanes

- **Connector lane**: add/update channel integrations.
- **Rules lane**: improve heuristic recommendations.
- **Prompt lane**: improve generation quality within JSON contracts.
- **UI lane**: improve Polaris/UX workflows for approvals and reporting.

## Release strategy

- Weekly patch releases for bug fixes and connector updates.
- Bi-weekly minor releases for feature additions.
- Emergency hotfix path for major channel/search policy changes.
