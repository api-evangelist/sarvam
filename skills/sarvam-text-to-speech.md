---
name: Synthesize speech from text
description: Generate natural Indian-language audio from text with Sarvam's Bulbul text-to-speech model.
api: openapi/sarvam-openapi-original.json
operations: [convert, convert-stream]
---

# Synthesize speech from text

## Auth
`api-subscription-key` header (or `Authorization: Bearer <key>`).

## Steps
1. `POST /text-to-speech` (`convert`) with `text`, a `target_language_code`, and a `speaker` voice (Bulbul v3, 30+ voices).
2. For low-latency / long text, use `POST /text-to-speech/stream` (`convert-stream`) to stream audio over a single HTTP POST, or the WebSocket channel `/text-to-speech/ws` for interactive playback.
3. Read the returned base64/audio payload and play or persist it.

## Rules
- Use the Pronunciation Dictionary API (`create`/`update`) to control how brand names and abbreviations are spoken.
- Auth failures = HTTP 403. 429 = rate limit; back off.
- Streaming is defined in asyncapi/sarvam-streaming-asyncapi.yaml.
