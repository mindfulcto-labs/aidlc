---
last_reviewed: 2026-06-14
tier: 3-hours
---

# Path 4, 3-hour tier: AI gateway architecture

Architecture posts paired with source-reading.

## 1. Portkey, Helicone, and TensorZero architecture posts

[`portkey.ai/blog`](https://portkey.ai/blog), [`helicone.ai/blog`](https://www.helicone.ai/blog), [`tensorzero.com/docs`](https://www.tensorzero.com/docs/)

Three different framings of the same category. Portkey leans on routing and reliability. Helicone leaned on speed (then was acquired by Mintlify in early 2026; check the maintenance status before adopting). TensorZero leans on the evals-and-observability cross-cut. Read one architecture post from each; the differences sketch the design space.

Why this slot: the category has matured to where the leading offerings rhyme on the basics. The differences in framing are themselves the teaching artefact.

## 2. Read the LiteLLM source

[`github.com/BerriAI/litellm`](https://github.com/BerriAI/litellm)

LiteLLM is the canonical Python implementation of multi-provider routing. Read the routing layer, the fallback layer, and the cost-tracking layer in source. The point is not to recommend it for production (the March 2026 supply-chain attack on `litellm@1.82.7/8` is worth searching for context); the point is that the source teaches the shape.

Why this slot: gateways are easier to design once you have read one mature implementation. LiteLLM is the most mature Python one.
