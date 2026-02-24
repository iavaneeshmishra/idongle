# AI Prompt Starters (SEM + SMM)

Use these as seed prompts for structured JSON generation.

## 1) SEM Campaign Draft Prompt

### Input
- Brand profile (voice, USP, prohibited terms)
- Product set (title, price, category, benefits)
- Target country/language
- Budget range
- Goal (traffic, conversions, ROAS)

### System intent
You are a performance marketing strategist specializing in Shopify ecommerce paid search.

### Expected JSON keys
- `campaign_name`
- `objective`
- `ad_groups[]`
  - `name`
  - `intent_theme`
  - `keywords[]`
  - `negative_keywords[]`
  - `rsa_headlines[]`
  - `rsa_descriptions[]`
- `budget_recommendation`
- `rationale`
- `compliance_notes`

---

## 2) SMM Content Calendar Prompt

### Input
- Brand voice
- Top products
- Seasonal events window
- Target audience personas
- Platforms (Instagram, Facebook, TikTok)

### Expected JSON keys
- `calendar_window_days`
- `posts[]`
  - `day`
  - `platform`
  - `content_pillar`
  - `hook`
  - `caption`
  - `hashtags[]`
  - `cta`
  - `utm`
- `creative_direction`
- `repurposing_ideas[]`

---

## 3) Weekly Optimization Summary Prompt

### Input
- Last 7/30 day channel metrics
- Prior recommendations and status
- Product-level conversion data

### Expected JSON keys
- `executive_summary`
- `wins[]`
- `losses[]`
- `root_causes[]`
- `recommended_actions[]`
  - `title`
  - `priority`
  - `estimated_impact`
  - `confidence`
  - `effort`
- `next_week_experiments[]`

