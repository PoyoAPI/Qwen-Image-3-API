# Qwen Image 3 API: cURL quickstart

Submit an async image task with model `qwen-image-3`:

```bash
export POYO_API_KEY="your-api-key"
export POYO_BASE_URL="https://api.poyo.ai"

curl -X POST "$POYO_BASE_URL/api/generate/submit" \
  -H "Authorization: Bearer $POYO_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
  "model": "qwen-image-3",
  "input": {
    "prompt": "Editorial travel poster of Hangzhou at dawn, West Lake mist, restrained teal and vermilion palette, crisp Chinese-inspired geometric layout, no logo",
    "size": "3:2",
    "resolution": "2K",
    "output_format": "png",
    "prompt_extend": true,
    "enable_safety_checker": true
  }
}'
```

Save `data.task_id`, then check status:

```bash
curl "$POYO_BASE_URL/api/generate/status/<task_id>" \
  -H "Authorization: Bearer $POYO_API_KEY"
```

For production, add a public HTTPS `callback_url` to the top-level request and make the receiver idempotent.

See the [full README](../README.md) and [production notes](../docs/production-notes.md).

