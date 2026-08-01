---
name: Translate and transliterate text
description: Translate, transliterate, or language-detect text across 22 Indian languages with Sarvam's text APIs.
api: openapi/sarvam-openapi-original.json
operations: [translate, transliterate, identify-language]
---

# Translate and transliterate text

## Auth
`api-subscription-key` header (or `Authorization: Bearer <key>`).

## Steps
1. Translate: `POST /translate` (`translate`) with `input`, `source_language_code` (use `auto` to detect), and `target_language_code` (BCP-47, e.g. `hi-IN`). Choose model `mayura:v1` or `sarvam-translate:v1`.
2. Transliterate: `POST /transliterate` (`transliterate`) to convert script without changing language.
3. Detect language: `POST /text-lid` (`identify-language`) returns the detected language with a confidence score.

## Rules
- Billed per character (rounded up).
- Auth failures = HTTP 403; 422 = validation error — check field names against the OpenAPI.
- 429 = rate limit / quota; back off with exponential retry.
