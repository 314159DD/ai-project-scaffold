# Providers - External Dependencies

**Updated:** <!-- YYYY-MM-DD -->

External services, APIs, and third-party dependencies the project relies on.

## Provider Matrix

| Provider | Type | Status | Cost | Doc |
|----------|------|--------|------|-----|
| <!-- e.g. Alchemy --> | <!-- RPC / API / SaaS --> | <!-- Active | Planned | Deprecated --> | <!-- Free tier / $X/mo --> | [<!-- alchemy.md -->](<!-- alchemy.md -->) |
| <!-- e.g. Supabase --> | <!-- Database + Auth --> | <!-- Active --> | <!-- Free tier --> | [<!-- supabase.md -->](<!-- supabase.md -->) |

<!-- Create one doc per provider from _TEMPLATE.md. Only add providers that need documentation beyond a one-liner. -->

## Credentials

<!-- Where are API keys stored? How are they managed? -->

- **Local dev:** `.env` / `.env.local` (gitignored)
- **Production:** <!-- e.g. Railway env vars, AWS Secrets Manager -->

## Rate Limits & Quotas

<!-- Quick reference for limits that affect architecture decisions -->

| Provider | Limit | Consequence |
|----------|-------|-------------|
| <!-- e.g. 0x API --> | <!-- 5 req/s --> | <!-- Must batch or cache --> |
| <!-- e.g. Alchemy --> | <!-- 30M CU/month --> | <!-- Pool to subgraph for bulk reads --> |
