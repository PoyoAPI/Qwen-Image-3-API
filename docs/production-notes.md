# Qwen Image 3 API production notes

## Confirmed contract

- Endpoint: `POST /api/generate/submit`
- Model IDs: `qwen-image-3`, `qwen-image-3-pro`
- Authentication: `Authorization: Bearer <POYO_API_KEY>`

## Input limits

| Field | Requirement | Constraint |
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

## Operational checklist

- Keep API keys in a server-side secret manager.
- Validate user input before calling the API.
- Persist `data.task_id` immediately after submission.
- Use five-second polling only for development; prefer `callback_url` in production.
- Make webhook processing idempotent and reconcile status before fulfilling an order.
- Copy output files to durable storage before provider URLs expire.
- Recheck the live model page before hard-coding prices.

## Failure handling

Treat non-2xx HTTP responses and non-success API `code` values as errors. Preserve the HTTP status, API code, request ID when present, and a redacted response body for debugging.

Schema: [PoYo API documentation](https://docs.poyo.ai/api-manual/image-series/qwen-image-3)

