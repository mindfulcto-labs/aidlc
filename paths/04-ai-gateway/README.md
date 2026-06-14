---
last_reviewed: 2026-06-14
confidence: exploratory
---

# Path 4: AI gateway architecture

The reading order for a platform or staff-plus engineer who has been asked to put a gateway in front of the firm's AI traffic. Covers routing, rate limiting, key management, observability, PII redaction, prompt-injection defence, and the audit-emission shape that lines up with a regulator's expectations.

## Audience

Platform engineers, staff engineers, Heads of Platform. Anyone whose remit includes "all calls to a large language model from inside the firm should go through this one thing".

## 30 minutes

- *(in progress)* Cloudflare's AI Gateway documentation, intro section only. Sets the vendor-shaped framing of the category in a few paragraphs.
- *(in progress)* Kong's AI Gateway announcement. Different vendor, different framing; reading both back-to-back gives the operator a quick sense of what is genuinely category-level versus what is product-specific.

## 3 hours

- *(in progress)* Portkey's and Helicone's architecture posts, plus one vendor-neutral analysis. The category has consolidated enough that the leading vendors' architectures rhyme; reading both helps the operator pick the right wedge.
- *(in progress)* Read the LiteLLM source. It is the canonical Python implementation of multi-provider routing. The path does not endorse it as a production choice (March 2026 supply-chain attack), but the source still teaches the right shape.

## 30 hours

- *(in progress)* Build a small gateway that does multi-provider routing, PII redaction, prompt-injection scanning, audit-trail emission, and per-team cost attribution. No book covers this end-to-end; the project is the curriculum. Use [`apiloom`](https://github.com/mindfulcto-labs/apiloom) as the underlying API gateway and bolt the AI-specific bits on top.
- *(in progress)* The Rust-flavoured version of the same exercise lives in `sentinel-rs` (when published). The trade-off between Python and Rust at the gateway layer is itself part of the curriculum.

## Notes

The gateway category is moving quickly. The path will refresh more often than the others because the right answer in 2026 will not be the right answer in 2028.

The exploratory confidence tag reflects how much of the path is still being authored. The 30-hour project tier is the most stable element; the 30-minute and 3-hour tiers will revise as the entries stabilise.
