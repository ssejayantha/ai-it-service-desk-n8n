# Portfolio Project Description

## Suggested title

AI-Powered IT Service Desk Automation — n8n, OpenAI, JavaScript, Google Sheets & Gmail

## Short description (website / project card)

Designed and tested an AI-assisted IT support ticket triage workflow using self-hosted n8n. The automation accepts authenticated webhook submissions, validates ticket data, checks Google Sheets for repeated request IDs, uses OpenAI to generate structured categorisation and troubleshooting suggestions, saves ticket records, and sends normal or high-priority Gmail alerts. Added reusable workflow-error notifications and verified accepted (HTTP 200), invalid (HTTP 400), and duplicate (HTTP 409) request outcomes. Developed as a portfolio prototype with documented security and concurrency limitations.

## Suggested interview explanation (45–60 seconds)

“I built an AI-assisted IT Service Desk automation on n8n, hosted on DigitalOcean. A webhook receives a support request, then JavaScript validates its input and Google Sheets is checked for duplicates. New requests go to an OpenAI model that returns a category, priority, possible cause, and suggested action in a structured format. The workflow stores the result and sends notifications through Gmail, with an extra alert for high-priority tickets. I tested successful requests, invalid submissions, duplicate IDs, and the error-notification workflow. One thing I learned is that a working demo is different from production readiness: Google Sheets lookups don't prevent simultaneous duplicate requests, so stronger idempotency and privacy controls would be next.”

## Resume-ready entry

**AI IT Service Desk Automation — Independent Project**
- Developed and tested an n8n workflow integrating secure webhooks, JavaScript validation, OpenAI structured classification, Google Sheets recordkeeping, and Gmail notifications.
- Implemented sequential duplicate checks and HTTP 200/400/409 outcomes; verified failure-alert delivery using a separate Error Trigger workflow.
- Documented security considerations, AI human-review requirements, and production hardening opportunities.

## GitHub repository suggestion

`ai-it-service-desk-n8n`

Do not publish a real n8n webhook secret, unsanitized exported workflow, staff ticket information, or internal service URLs.
