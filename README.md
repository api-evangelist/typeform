# Typeform (typeform)

Typeform is a conversational forms and surveys platform with branching logic, integrations and analytics. The developer platform exposes four primary surfaces — Create API, Responses API, Webhooks API and an Embed SDK — and is documented at typeform.com/developers.

**APIs.json:** [apis.yml](apis.yml)

## APIs
- **Create API** — `https://api.typeform.com` — manage forms, themes, images, workspaces. Bearer-token auth.
- **Responses API** — `https://api.typeform.com` — programmatic JSON access to submissions.
- **Webhooks API** — `https://api.typeform.com` — register URLs to receive every submission.
- **Embed SDK** — JS embed (inline / popup / fullscreen / sidetab / popover / slider).

## OpenAPI
Typeform documents the API on Stoplight but does not publish a downloadable OpenAPI/Swagger document at a stable public URL as of 2026-05-08. Pipeline did not retrieve a spec into `openapi/`.

## Tags
Forms, Surveys, Conversational, Lead Capture, SaaS, Webhooks, Embed

## Common Properties
- [Website](https://www.typeform.com/) · [Developer Hub](https://www.typeform.com/developers/)
- [Pricing](https://www.typeform.com/pricing/) · [Status](https://status.typeform.com/) · [GitHub](https://github.com/typeform)
- [Plans](plans/typeform-plans-pricing.yml) — reconciled
- [Rate Limits](rate-limits/typeform-rate-limits.yml) — reconciled
- [FinOps](finops/typeform-finops.yml) — reconciled, FOCUS-aligned

## Plans (reconciled)
- **Basic** — $39/mo, 100 responses/mo, 1 user.
- **Plus** — $79/mo, 1,000 responses/mo, 3 users.
- **Business** — $129/mo, 10,000 responses/mo, 5 users.
- **Talent** — $169/mo, 3,000 responses/mo, 3 users (HR).
- **Growth Flow** — $379/mo, 10,000+ responses, 5 seats.
- **Growth Custom / Enterprise** — custom.
- ~30% off on annual.

## Rate Limits (reconciled)
- 2 requests/second per token; 429 + Retry-After.
- Plan-tier monthly response ceilings act as a business-level quota.

## Timestamps
- **Created:** 2026-05-08
- **Modified:** 2026-05-08

## Maintainers
- **Kin Lane** — kin@apievangelist.com
