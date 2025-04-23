# Groq Changelog

## 2025-04-23 (Python SDK v0.23.0, TypeScript SDK v0.20.0)

### [CHANGED] Python SDK v0.23.0, TypeScript SDK v0.20.0

The Python SDK has been updated to v0.23.0 and the Typescript SDK has been updated to v0.20.0.

**Key Changes:**

 - `groq.files.content` returns a `Response` object now to allow parsing as text (for `jsonl` files) or blob for generic file types
 - `BatchCreateParams` now accepts a `string` as input to `completion_window` to allow for time frames between `24h` and `7d`.
 - Updated chat completion `model` parameter to remove deprecated models and add newer production models.
 - Added optional chat completion `metadata` parameter for better compatibility.

## 2025-04-21 (Python SDK v0.22.0, TypeScript SDK v0.19.0)

### [ADDED] Compound Beta and Compound Beta Mini Systems

Compound Beta and Compound Beta Mini are agentic tool systems with web search and code execution built in. These systems simplify your workflow when interacting with realtime data and eliminate the need to add your own tools to search the web. Read more about [agentic tooling on Groq](https://console.groq.com/docs/agentic-tooling), or start using them today by switching to `compound-beta` or `compound-beta-mini`.

**Performance:**
- Compound Beta (`compound-beta`): 350 tokens per second (TPS) with a latency of ~4,900 ms
- Compound Beta Mini (`compound-beta-mini`): 275 TPS with a latency of ~1,600 ms

**Example Usage:**
```curl
curl "https://api.groq.com/openai/v1/chat/completions" \
  -X POST \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer ${GROQ_API_KEY}" \
  -d '{
         "messages": [
           {
             "role": "user",
             "content": "what happened in ai this week?"
           }
         ],
         "model": "compound-beta",
       }'
```

## 2025-04-14 (Python SDK v0.22.0, TypeScript SDK v0.19.0)

### [ADDED] Meta Llama 4 Support
Meta's Llama 4 Scout (17Bx16MoE) and Maverick (17Bx128E) models for image understanding and text generation are now available through Groq API with support for a 128K token context window, image input up to 5 images, function calling/tool use, and JSON mode. Read more in our [tool use](https://console.groq.com/docs/tool-use) and [vision](https://console.groq.com/docs/vision) docs.

**Performance (as benchmarked by [AA](https://artificialanalysis.ai/)):**
- Llama 4 Scout (`meta-llama/llama-4-scout-17b-16e-instruct`): Currently 607 tokens per second (TPS)
- Llama 4 Maverick (`meta-llama/llama-4-maverick-17b-128e-instruct`): Currently 297 TPS

**Example Usage:**
```curl
curl "https://api.groq.com/openai/v1/chat/completions" \
  -X POST \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer ${GROQ_API_KEY}" \
  -d '{
         "messages": [
           {
             "role": "user",
             "content": "why is fast inference crucial for ai apps?"
           }
         ],
         "model": "meta-llama/llama-4-maverick-17b-128e-instruct",
       }'
```