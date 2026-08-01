---
name: Subscribe to Sendspark video events via webhooks
description: Register, inspect, update, and remove a workspace webhook that receives Sendspark video lifecycle and engagement events.
api: openapi/sendspark-openapi-original.json
operations: [getWorkspaces, postCreateWebhook, getWebhookListByWorkspaceId, getWebhookById, patchModifyWebhook, deleteWebhookById]
---

# Manage Sendspark webhooks

Use the Sendspark API to receive HTTP callbacks when videos are generated, rendered, watched, or clicked.

## Auth
Send both headers on every request (workspace-scoped):
- `x-api-key: <API key>`
- `x-api-secret: <API secret>`

Base URL: `https://api-gw.sendspark.com`

## Steps
1. **Resolve the workspace.** `getWorkspaces` (`GET /v1/workspaces`) to pick the `workspaceId`.
2. **Create the subscription.** `postCreateWebhook` (`POST /v1/workspaces/{workspaceId}/webhooks`) with a body containing `name`, `url` (your HTTPS endpoint), `module`, and an `events` array chosen from: `video_watched`, `video_played`, `video_cta_clicked`, `video_viewed`, `video_liked`, `video_request_received`, `video_generated_dv`, `video_mp4_ready`, `video_generated_error`. `name`, `url`, and `module` are required.
3. **Verify.** `getWebhookListByWorkspaceId` (`GET /v1/workspaces/{workspaceId}/webhooks`) or `getWebhookById` (`GET /v1/workspaces/{workspaceId}/webhooks/{webhookId}`).
4. **Adjust events/URL.** `patchModifyWebhook` (`PATCH /v1/workspaces/{workspaceId}/webhooks/{webhookId}`).
5. **Remove.** `deleteWebhookById` (`DELETE /v1/workspaces/{workspaceId}/webhooks/{webhookId}`).

## Rules
- Errors are a flat JSON envelope `{statusCode, code, error, message}` (not RFC 9457); handle `400`, `404`. See `errors/sendspark-problem-types.yml`.
- No idempotency key is supported — do not blindly retry `POST` on timeout; re-list to check whether the webhook was created.
- Event payload contract: `asyncapi/sendspark-webhooks-asyncapi.yml`.
