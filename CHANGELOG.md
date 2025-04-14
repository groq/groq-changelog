# Groq Changelog

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