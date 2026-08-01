---
name: Transcribe Indian-language speech
description: Convert a short audio file to text (or English translation) using Sarvam's synchronous Speech-to-Text API.
api: openapi/sarvam-openapi-original.json
operations: [transcribe]
---

# Transcribe Indian-language speech

Use this for audio files up to the synchronous size limit (~1 MB / short clips). For long files use the batch job flow instead.

## Auth
Send your key in the `api-subscription-key` header (`Authorization: Bearer <key>` also works). The SDK reads `SARVAM_API_KEY`.

## Steps
1. `POST /speech-to-text` (`transcribe`) with the audio `file` (multipart), `model` (default `saaras:v3`), and `mode` (`transcribe`, `translate`, `verbatim`, `translit`, or `codemix`).
2. Optionally set BCP-47 `language_code`; omit to auto-detect.
3. Read the transcript from the JSON response.

## Rules
- Auth failures return HTTP **403** (not 401) with `error.code: invalid_api_key_error`.
- 413 means the file exceeds the sync limit — switch to the batch job flow.
- 429 = rate limit / quota; back off with exponential retry.
- No idempotency key; do not blindly retry non-idempotent 4xx.
