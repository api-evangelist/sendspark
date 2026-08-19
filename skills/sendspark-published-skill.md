---
name: Sendspark
description: Use when recording personalized videos, creating AI-powered dynamic video campaigns, automating video generation and sending, integrating with CRMs and email platforms, or tracking video engagement analytics. Agents should reach for this skill when users need to record videos, personalize at scale with AI voice cloning, set up automated workflows, or send videos through sales and marketing tools.
metadata:
    mintlify-proj: sendspark
    version: "1.0"
---

# Sendspark Skill

## Product summary

Sendspark is a video personalization platform that lets you record videos (camera, screen, or both), personalize them at scale with AI voice cloning and dynamic backgrounds, and send them through CRMs, email platforms, and sales automation tools. The core workflow is: record → personalize → send → track. Key tools include the Chrome Extension (easiest for recording), Desktop App (for recording over non-Chrome apps), Dynamic Videos (AI-powered personalization), Automated Workflows (trigger-based video generation), and Webhooks/API (for programmatic video creation). Primary docs: https://help.sendspark.com. API credentials are managed at `sendspark.com/settings/api-credentials`. Workspace settings control branding, integrations, and team permissions at `sendspark.com/settings/workspace`.

## When to use

- **Recording videos**: User wants to record a quick personalized message, demo, or follow-up using camera, screen, or both.
- **Scaling personalization**: User needs to send hundreds or thousands of personalized videos with AI voice cloning (replacing a placeholder word like "watermelon" with each recipient's name) and dynamic backgrounds (inserting each prospect's website behind the speaker).
- **Automating video workflows**: User wants videos to generate automatically when a trigger fires (form filled, meeting booked, lead added to sequence, etc.) and optionally auto-send via email or LinkedIn.
- **Integrating with sales/marketing tools**: User needs to send videos through HubSpot, Salesforce, Mailchimp, Outreach, Instantly, Lemlist, Apollo, or 60+ other platforms.
- **Tracking engagement**: User wants to see who watched videos, how much they watched, and whether they clicked CTAs.
- **Building with API/webhooks**: User wants to programmatically create dynamic videos or trigger actions based on video events (viewed, CTA clicked, etc.).

## Quick reference

### Recording modes (Chrome Extension)

| Mode | Use case | Notes |
|------|----------|-------|
| **Camera Only** | Face-to-camera message | Best for dynamic videos (backgrounds replace what's behind you) |
| **Screen Only** | Demo, walkthrough, screen share | No camera bubble |
| **Cam + Screen** | Intro + demo combo | Camera bubble over screen; default mode |

### Sharing methods

| Method | Best for | Notes |
|--------|----------|-------|
| **Linked GIF** | Email (1x1 or automation) | Copy animated or static thumbnail + link; paste in email draft |
| **Copy Link** | LinkedIn, Slack, messaging | Direct link; unfurls to show preview |
| **Embed in Email** | Marketing platforms (Mailchimp, HubSpot) | Requires HTML editing; video plays in-email if client supports it |
| **Download MP4** | Social media posts | Optimize newsfeed algorithm |
| **Website Embed** | Landing pages, blogs | Unlimited embeds; copy HTML code |

### Key file paths & settings

- **API Credentials**: `sendspark.com/settings/api-credentials` (generate keys here)
- **Workspace Settings**: `sendspark.com/settings/workspace` (branding, integrations, team)
- **Video Library**: `sendspark.com/my-library` (personal) or `sendspark.com/team-library` (shared)
- **Dynamic Videos**: `sendspark.com/dynamic-videos` (create campaigns)
- **Automated Workflows**: `sendspark.com/automated-workflows` (create automations)
- **Templates**: `sendspark.com/templates` (manage video page templates)

### Merge tags (personalization variables)

| Tag | Replaces with | Fallback |
|-----|----------------|----------|
| `#{{first_name}}` | Recipient's first name | "there" |
| `#{{company}}` | Recipient's company | "your company" |
| `#{{job_title}}` | Recipient's job title | "professional" |

### Dynamic video workflow

1. Record with **Face** mode (not Both) using Chrome Extension
2. Say **"watermelon"** once in intro (e.g., "Hey watermelon, I'm Dan...")
3. Pause briefly after "watermelon" for clean audio
4. Upload CSV with first name, email, company, job title
5. Turn on **AI voice cloning** to replace "watermelon" with each name
6. Customize landing page with merge tags
7. Click **Generate Videos** (processes in batches of up to 20)
8. Test with few contacts first, then scale

### API endpoints (core)

| Method | Endpoint | Purpose |
|--------|----------|---------|
| POST | `/v1/workspaces/{workspaceId}/dynamics` | Create dynamic campaign |
| POST | `/v1/workspaces/{workspaceId}/dynamics/{dynamicId}/prospects/bulk` | Add contacts & generate videos |
| POST | `/v1/workspaces/{workspaceId}/webhooks` | Create webhook |
| GET | `/v1/workspaces/{workspaceId}/dynamics` | List campaigns |

## Decision guidance

### When to use Chrome Extension vs Desktop App

| Scenario | Chrome Extension | Desktop App |
|----------|-----------------|------------|
| Recording over websites, Gmail, LinkedIn | ✓ | — |
| Recording over PowerPoint, PDFs, local apps | — | ✓ |
| Quick recording with pre-built integrations | ✓ | — |
| Better audio/video sync needed | — | ✓ |
| Recording multiple apps in one video | — | ✓ |

### When to use AI voice cloning vs static video

| Scenario | AI Voice Cloning | Static Video |
|----------|-----------------|--------------|
| Personalizing 100+ videos with names | ✓ | — |
| One-off personalized message | — | ✓ |
| Need lip-sync with dynamic backgrounds | ✓ | — |
| Simple text personalization only | — | ✓ |

### When to use dynamic backgrounds vs static

| Scenario | Dynamic Backgrounds | Static |
|----------|-------------------|--------|
| Prospect's website behind you | ✓ | — |
| LinkedIn profile background | ✓ | — |
| Professional/branded background | — | ✓ |
| Virtual background | — | ✓ |

### When to use Automated Workflows vs manual sending

| Scenario | Automated Workflow | Manual |
|----------|-------------------|--------|
| Trigger: form filled, meeting booked, lead added | ✓ | — |
| One-time send to list | — | ✓ |
| Recurring trigger (daily new leads) | ✓ | — |
| Need to review before sending | — | ✓ |

## Workflow

### Recording and sharing a single video

1. **Install recorder**: Chrome Extension (easiest) or Desktop App (for non-Chrome apps).
2. **Set preferences**: Choose recording mode (Camera Only, Screen Only, Cam + Screen).
3. **Record**: Click Sendspark icon → Record → use toolbar to pause/stop.
4. **Edit**: Trim, add template, or customize landing page (optional).
5. **Share**: Copy Linked GIF (email), Copy Link (LinkedIn/Slack), or Download MP4 (social).
6. **Track**: Click Analytics on video to see views, plays, CTA clicks, viewer details.

### Creating a dynamic video campaign

1. **Record with placeholder**: Use Chrome Extension in Face mode; say "watermelon" once in intro with a brief pause after.
2. **Start campaign**: Go to Dynamic Videos → Start Creating → select your video.
3. **Enable AI voice cloning**: Toggle on to replace "watermelon" with each contact's name.
4. **Customize landing page**: Add merge tags (first name, company, job title) to header, message, CTA.
5. **Upload contacts**: CSV with first name, email, company, job title (first name & email required).
6. **Generate**: Click Generate Videos; monitor progress (shows "3 of 20" while processing).
7. **Test first**: Review a few generated videos before scaling to full list.
8. **Add more contacts**: Click Add More Contacts to import additional CSVs.

### Setting up an automated workflow

1. **Go to Automated Workflows**: Click New Automation or Create from Template.
2. **Add trigger**: Select event (form filled, demo booked, lead status, webpage visited, etc.).
3. **Add action**: Choose action (generate dynamic video, send email, add to campaign, etc.).
4. **Connect Sendspark**: If using Sendspark as action, select "Create dynamic video" and map data fields.
5. **Add tools** (optional): Router logic, data cropping, time delays.
6. **Test**: Run with test data before activating.
7. **Activate**: Turn on automation; monitor for errors.

### Sending videos through a CRM or email platform

1. **Check integration**: Search docs for your platform (e.g., "HubSpot send dynamic videos").
2. **Connect platform**: Go to Integrations → Add Connection → authenticate.
3. **Share video**: Click Share Video on your video → find your platform → copy snippet or link.
4. **Paste in email/sequence**: Paste Linked GIF (email) or link (LinkedIn) into your message.
5. **Personalize** (optional): Add merge tags so each recipient sees their name/company.
6. **Send**: Use platform's send button; Sendspark tracks opens and clicks.

### Creating API-driven dynamic videos

1. **Generate API key**: Go to `sendspark.com/settings/api-credentials` → GENERATE KEYS.
2. **Create campaign**: POST to `/v1/workspaces/{workspaceId}/dynamics` with video ID and settings.
3. **Add prospects**: POST to `/v1/workspaces/{workspaceId}/dynamics/{dynamicId}/prospects/bulk` with contact list.
4. **Monitor generation**: Poll campaign status or set up webhook to listen for `video_generated_dv` event.
5. **Retrieve videos**: Use Share URL or Embed URL from response to send or embed.

## Common gotchas

- **Recording in "Both" mode for dynamic videos**: Always use **Face mode** for dynamic videos. "Both" mode will crop unexpectedly when backgrounds are applied. Switch mode from bottom icons in Chrome Extension.
- **"Watermelon" keyword issues**: Say it only **once** per video, in the intro. Pause briefly after it. If not paused, AI voice cloning may sound unnatural or fail.
- **Video too short for AI voice cloning**: Aim for **at least 10 seconds**; videos under 5 seconds often fail to clone cleanly.
- **Missing required fields in CSV**: First name and email are **required** for dynamic video campaigns. Company and job title are optional but recommended for merge tags.
- **Merge tag fallbacks not working**: If a contact's field is empty, Sendspark shows the fallback text. Set meaningful fallbacks (e.g., "there" instead of "[first_name]").
- **Webhook only for dynamic campaigns**: Webhooks fire only for dynamic video campaigns, not individual videos in your library.
- **API key plan requirement**: API keys require a paid plan; check for a badge next to "API Keys" in settings.
- **Permissions missing error**: If recording stops with "Permissions Missing" and timer stuck at 0:00, reset permissions: Extensions → Manage Extensions → Sendspark → Details → Site Settings → Reset Permissions.
- **Camera/microphone not detected**: Close other apps (Zoom, OBS) that may control peripherals. Connect devices directly (not through USB hub). Select correct device in extension Settings.
- **Batch processing limits**: Dynamic video generation processes up to 20 videos at a time. Larger lists show progress (e.g., "20 of 400").
- **Instant integrations require Chrome Extension**: Pre-built integrations (Gmail, LinkedIn, Outreach, HubSpot) only work with Chrome Extension installed.
- **Lip-sync best with dynamic backgrounds**: Lip-sync V-2 works best paired with dynamic backgrounds. Without backgrounds, try the "waving hand trick" to mask minor mismatches.

## Verification checklist

Before submitting work with Sendspark:

- [ ] **Recording**: Video is at least 10 seconds, audio is clear, background is stable, lighting is good.
- [ ] **Dynamic videos**: "Watermelon" keyword used once with pause after; Face mode selected; CSV has first name & email.
- [ ] **AI voice cloning**: Enabled and tested on 1-2 videos before scaling.
- [ ] **Merge tags**: Fallback text is meaningful (not blank or generic).
- [ ] **Landing page**: Header, message, and CTA are customized and preview looks correct.
- [ ] **Integrations**: Platform is connected and authenticated; snippet copied correctly.
- [ ] **Sharing**: Correct method used (Linked GIF for email, Link for LinkedIn, MP4 for social).
- [ ] **Automation**: Trigger and action are configured; test data processed successfully.
- [ ] **API**: Workspace ID and API key are valid; webhook URL is reachable.
- [ ] **Analytics**: Video is live and tracking (check Analytics button for views/plays).

## Resources

**Comprehensive navigation**: https://help.sendspark.com/llms.txt

**Critical docs**:
- [Getting Started: Record a Video](https://help.sendspark.com/getting-started-guide-record-a-video) — Install recorder, record, share, track.
- [How to Create a Dynamic Video Campaign](https://help.sendspark.com/how-to-create-a-dynamic-video-campaign) — AI voice cloning, merge tags, batch generation.
- [Sendspark Automated Workflows Beginner's Guide](https://help.sendspark.com/sendspark-automated-workflows-beginner-s-guide) — Triggers, actions, workflow patterns.

---

> For additional documentation and navigation, see: https://help.sendspark.com/llms.txt