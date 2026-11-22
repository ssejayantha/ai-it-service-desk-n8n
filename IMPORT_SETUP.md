# AI IT Service Desk — Import & Setup Guide

This JSON is a **sanitised portfolio template** made from the user's tested 17-node n8n workflow. It preserves the workflow nodes, code, AI prompt, structured output parser, connections and HTTP response logic. It is **not configured to run immediately after import**.

## Import into your own n8n instance

1. In n8n create a new workflow and choose **Import from File** (workflow menu).
2. Import `ai-it-service-desk-sanitized.json`.
3. On **Webhook - New Ticket**, create/select your own **Header Auth** credential with a strong private header secret. The header name used in testing was `X-IT-Ticket-Key`.
4. On **Check Duplicate Ticket** and **Append row in sheet**, choose your own Google Sheets OAuth credential, document and `Tickets` sheet. Create the 13 columns listed below.
5. On both **Gmail** nodes, select your own Gmail credential and set an intended recipient address; recipients are deliberately blank in this export.
6. On **OpenAI Chat Model**, select your own OpenAI credential. The template references a model name; availability and billing depend on your account.
7. Under the workflow **Settings**, choose your own separately configured and published **Error Handler** workflow. It is not bundled in this export.
8. Save, then test with **Execute workflow from the main canvas** and the displayed **Test URL**. The workflow is deliberately exported inactive.
9. Inspect all settings and security protections before enabling any Production Webhook.

Google Sheet header columns (in order):

`ticketId, requester, summary, priority, category, receivedAt, status, note, requestId, aiCategory, aiPriority, aiCause, aiSuggestedAction`

## Expected test cases

- Valid new ticket -> HTTP **200**, model analysis, one sheet row and Gmail notification.
- Invalid request (empty `summary`) -> HTTP **400**, no model/sheet/email.
- Duplicate `requestId` -> HTTP **409**, no model/sheet/email.
- Unexpected workflow execution failure -> separately configured Error Handler should alert; verify with a dedicated isolated test workflow.

## Security and limitations

- This public JSON intentionally contains **no real credential references, recipient addresses, spreadsheet IDs, original webhook path, instance identifiers, execution logs or original workflow ID**.
- The code and architecture are preserved, but imported nodes must be reconfigured before execution.
- **Google Sheets lookup isn't atomic**; simultaneous submissions can bypass duplicate prevention. Add transactional/unique-key idempotency for real production use.
- **Model outputs are advice**, not confirmed diagnoses, and require human review.
- Ensure a retention policy, data minimisation, rate limiting, access control and appropriate handling of real ticket content before deploying.
- The Error Handler is a **separate workflow** and must be exported/sanitised separately to reproduce automatic alerting.
- Never store production secrets or identifiable IT ticket data in a public repository.
