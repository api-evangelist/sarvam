---
name: Chat completion with Sarvam LLMs
description: Generate multilingual responses with Sarvam-30B / Sarvam-105B via an OpenAI-compatible chat endpoint.
api: openapi/sarvam-openapi-original.json
operations: [completions]
---

# Chat completion with Sarvam LLMs

## Auth
`api-subscription-key` header (or `Authorization: Bearer <key>`).

## Steps
1. `POST /v1/chat/completions` (`completions`) with `model` (`sarvam-30b` 64K context or `sarvam-105b` 128K), and an OpenAI-style `messages` array.
2. Tune with `temperature`, `top_p`, `max_tokens`, `reasoning_effort`, `frequency_penalty`, `presence_penalty`, `seed`, and `stop`.
3. Set `wiki_grounding: true` for RAG-style factual grounding from Wikipedia.

## Rules
- `sarvam-m` is deprecated and rejected — use `sarvam-30b` or `sarvam-105b`.
- Set `reasoning_effort` and `max_tokens` explicitly; defaults have changed over time.
- Auth failures = HTTP 403; 429 = rate limit / quota — back off.
- Pricing is per 1M tokens (input / cached input / output).
