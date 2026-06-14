---
last_reviewed: 2026-06-14
tier: 30-minutes
---

# Path 4, 30-minute tier: AI gateway architecture

Two vendor pieces read back-to-back. The differences teach you what is genuinely category-level versus what is product-specific.

## 1. Cloudflare AI Gateway docs, intro section

[`developers.cloudflare.com/ai-gateway`](https://developers.cloudflare.com/ai-gateway/)

Cloudflare's framing of the AI Gateway category. Strong on observability and rate limiting; lighter on the runtime safety pieces. Cloudflare's reach gives them a clear view of what real traffic looks like at the boundary.

Why this slot: Cloudflare's perspective is edge-first, which is the lens most other vendors avoid. Reading them first widens the operator's mental model of where a gateway can sit.

## 2. Kong's AI Gateway announcement and feature pages

[`konghq.com/blog/product/kong-ai-gateway`](https://konghq.com/blog/product/kong-ai-gateway)

Kong's framing. More mature on API-management heritage; later to the AI-specific safety pieces. The contrast with Cloudflare's read sharpens both.

Why this slot: Kong is the closest analogue to the open-source API-management lineage. Their product is the natural reference for any team already operating Kong or its peers.
