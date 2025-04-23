# Groq Changelog

## 2025-04-23 (Python SDK v0.23.0, TypeScript SDK v0.20.0)

### [CHANGED] Python SDK v0.23.0, TypeScript SDK v0.20.0

The Python SDK has been updated to v0.23.0 and the Typescript SDK has been updated to v0.20.0.

**Key Changes:**

 - `groq.files.content` returns a `Response` object now to allow parsing as text (for `jsonl` files) or blob for generic file types. Previously, the return type as a JSON object was incorrect, and this caused the SDK to encounter an error instead of returning the file's contents. Example usage in Typescript:

```ts
const response = await groq.files.content("file_XXXX");
const file_text = await response.text();
```

 - `BatchCreateParams` now accepts a `string` as input to `completion_window` to allow for durations between `24h` and `7d`. Using a longer completion window gives your batch job a greater chance of completing successfully without timing out. For larger batch requests, it's recommended to split them up into multiple batch jobs. [Learn more about best practices for batch processing](https://console.groq.com/docs/batch).
 - Updated chat completion `model` parameter to remove deprecated models and add newer production models.
   - Removed: `gemma-7b-it` and `mixtral-8x7b-32768`.
   - Added: `gemma2-9b-it`, `llama-3.3-70b-versatile`, `llama-3.1-8b-instant`, and `llama-guard-3-8b`.
   - For the most up-to-date information on Groq's models, see the [models page](https://console.groq.com/docs/models), or learn more about our [deprecations policy](https://console.groq.com/docs/deprecations).
 - Added optional chat completion `metadata` parameter for better compatibility with OpenAI chat completion API. [Learn more about switching from OpenAI to Groq](https://console.groq.com/docs/openai).

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