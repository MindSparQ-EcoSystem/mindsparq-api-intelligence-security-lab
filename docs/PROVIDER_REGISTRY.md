# Provider and Model Registry

## Purpose

Maintain reliable, source-attributed information about AI providers and models. This catalog is independent from secret detection and credential validation.

## Initial provider candidates

The following are candidates for research, not a claim that every provider currently offers a free API tier:

- Google AI / Gemini
- OpenRouter
- Groq
- Cerebras
- Mistral
- OpenAI
- Anthropic
- Together AI
- Fireworks AI
- Hugging Face Inference Providers

## Required fields

| Field | Description |
|---|---|
| provider_id | Stable internal identifier |
| provider_name | Display name |
| official_site | Official provider website |
| api_docs | Official API documentation |
| auth_method | Documented authentication mechanism |
| base_url | Official API base URL, if public |
| compatibility | OpenAI-compatible, native, other |
| model_id | Exact provider model identifier |
| free_tier | FREE / LIMITED_FREE / TRIAL / PAID / UNKNOWN |
| pricing_url | Official pricing page |
| rate_limit_docs | Official rate-limit documentation |
| checked_at | Last verification timestamp |
| notes | Region/account eligibility and caveats |

## Data quality rules

- Prefer official provider sources.
- Record the source URL for every volatile claim.
- Distinguish open weights from free hosted API access.
- Distinguish free trial credits from ongoing free tier.
- Do not infer free access from model availability in a router.
- Recheck volatile data on a schedule and mark stale records.
- Never store provider credentials in this registry.
