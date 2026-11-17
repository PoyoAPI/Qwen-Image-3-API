# Qwen Image 3 API: runnable cURL and Node.js examples

[![PoYo model page](https://img.shields.io/badge/Try%20on%20PoYo-qwen--image--3--api-84cc16)](https://poyo.ai/models/qwen-image-3) [![API docs](https://img.shields.io/badge/API-docs-22d3ee)](https://docs.poyo.ai/api-manual/image-series/qwen-image-3) [![Check](https://github.com/PoyoAPI/Qwen-Image-3-API/actions/workflows/check.yml/badge.svg)](https://github.com/PoyoAPI/Qwen-Image-3-API/actions/workflows/check.yml)

Generate or edit 1K and 2K images with Qwen Image 3 or Qwen Image 3 Pro through PoYo's async API.

**Answer:** To use the Qwen Image 3 API, send a server-side request to `POST https://api.poyo.ai/api/generate/submit` with model `qwen-image-3`, `qwen-image-3-pro` and a PoYo API key. The examples in this repository are runnable with Node.js 22+ or cURL.

Last verified against the live PoYo schema and pricing on **November 16, 2026**.

## Quickstart

1. Create a key in the [PoYo dashboard](https://poyo.ai/dashboard/api-key).
2. Copy `.env.example` to `.env` and replace the placeholder.
3. Run `node node/index.mjs`.

```dotenv
POYO_API_KEY=YOUR_POYO_API_KEY_HERE
POYO_BASE_URL=https://api.poyo.ai
```

The complete cURL request is in [curl/generate.md](curl/generate.md). The Node.js example submits the task and polls until `finished` or `failed`.

## Model IDs

- `qwen-image-3`
- `qwen-image-3-pro`

Use the exact IDs above. Product names and API model IDs are not always identical.

## Request fields

| Field | Requirement | Meaning |
| --- | --- | --- |
| prompt | required | Generation or editing instruction, up to 5,000 characters. |
| image_urls | optional | One to three input images. |
| size | optional | 1:1, 3:2, 2:3, 4:3, 3:4, 16:9, 9:16, or 21:9. |
| resolution | optional | 1K or 2K; default 1K. |
| output_format | optional | png or jpeg. |
| prompt_extend | optional | Boolean prompt expansion. |
| negative_prompt | optional | Up to 5,000 characters. |
| seed | optional | Integer from 0 to 2147483647. |
| enable_safety_checker | optional | Boolean. |

## Pricing snapshot

| Usage | Price |
| --- | --- |
| qwen-image-3, 1K or 2K | $0.024 per image |
| qwen-image-3-pro, 1K | $0.032 per image |
| qwen-image-3-pro, 2K | $0.06 per image |
| Input image surcharge | $0.0025 per image |

Pricing can change. Confirm the current amount on the [model page](https://poyo.ai/models/qwen-image-3) before a production rollout.

## Best for

- text-to-image
- multi-image editing
- poster and product artwork

## Important behavior

- Use qwen-image-3-pro when the higher-tier model is required.
- Editing accepts one to three public input-image URLs.
- Output URLs should be downloaded and stored by your application.

## Async production flow

```text
submit -> persist data.task_id -> poll during development -> receive callback_url webhook in production
```

Treat `finished` and `failed` as terminal states. Accept a webhook only for task IDs your system created, process it idempotently, and reconcile the final state through the status endpoint.

## Repository map

- [`curl/generate.md`](curl/generate.md) — copy-paste request
- [`node/index.mjs`](node/index.mjs) — dependency-free Node.js example
- [`docs/production-notes.md`](docs/production-notes.md) — limits and rollout checklist

## Links

- [Try Qwen Image 3 API on PoYo](https://poyo.ai/models/qwen-image-3)
- [API reference](https://docs.poyo.ai/api-manual/image-series/qwen-image-3)
- [All PoYo examples](https://github.com/PoyoAPI/poyo-examples)
- [PoYo model catalog](https://poyo.ai/models)

## License

MIT

