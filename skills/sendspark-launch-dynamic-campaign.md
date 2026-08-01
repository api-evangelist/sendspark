---
name: Launch a Sendspark dynamic video campaign and track a prospect
description: Create an AI-personalized (Dynamic Video) campaign in a workspace, add a prospect, and poll their generated-video status.
api: openapi/sendspark-openapi-original.json
operations: [getWorkspaces, postDynamicsV2, postV1WorkspacesWorkspaceidDynamicsDynamicsidProspect, getProspectDynamicsVideos, getWorkspaceDynamics]
---

# Launch a dynamic video campaign

Create a Dynamic Video campaign that personalizes one recording per prospect, then enroll a prospect and watch their video render.

## Auth
Both headers, on every call:
- `x-api-key: <API key>`
- `x-api-secret: <API secret>`

Base URL: `https://api-gw.sendspark.com`

## Steps
1. **Pick the workspace.** `getWorkspaces` (`GET /v1/workspaces`) → `workspaceId`.
2. **Create the campaign.** `postDynamicsV2` (`POST /v2/workspaces/{workspaceId}/dynamics`) with the campaign configuration (share page, buttons, layout, video properties). Capture the returned `dynamicId`. (The v1 equivalent is `postDynamics`.)
3. **Add a prospect.** `postV1WorkspacesWorkspaceidDynamicsDynamicsidProspect` (`POST /v1/workspaces/{workspaceId}/dynamics/{dynamicsId}/prospect`) with the prospect fields (including `contactEmail`). For many prospects use `postDynamicsProspectsBulkModify` (`.../prospects/bulk`).
4. **Poll status.** `getProspectDynamicsVideos` (`GET /v1/workspaces/{workspaceId}/dynamics/{dynamicId}/prospects/{contactEmail}`) until the video is ready — or subscribe to `video_generated_dv` / `video_mp4_ready` webhooks instead of polling.
5. **Inspect the campaign.** `getWorkspaceDynamics` (`GET /v1/workspaces/{workspaceId}/dynamics/{dynamicId}`).

## Rules
- `503 Service Unavailable` is a documented response on campaign operations — back off and retry.
- No idempotency key; on a `POST` timeout, re-fetch the campaign/prospect before recreating.
- Error envelope and codes: `errors/sendspark-problem-types.yml`. Conventions: `conventions/sendspark-conventions.yml`.
