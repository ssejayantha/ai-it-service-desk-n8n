# AI IT Service Desk — Security & Publication Checklist

**Purpose:** Review the n8n demo before enabling real users or publishing project assets.

## Immediate cleanup

- [ ] **Unpublish** the temporary `IT Error Handler - Test` workflow; do not unpublish the real Error Handler.
- [ ] Keep the real `IT Service Desk - Error Handler` **published** and selected in the final workflow's Settings.
- [ ] Confirm the rotated `X-IT-Ticket-Key` Header Auth credential is selected on the final Webhook node.
- [ ] Retire any previous auth values that may still be accepted by other credentials or workflows.
- [ ] Inspect recent n8n executions for headers containing the previously exposed secret and restrict/delete sensitive saved data according to your needs. Rotating a credential does not remove its old value from historical execution logs.

## n8n settings and access

- [ ] Set **Save failed production executions** to Save while debugging errors; review retention and access permissions.
- [ ] Consider reducing successful/manual execution data storage after testing; configure pruning and verify backups.
- [ ] Check whether execution-data redaction is supported in your n8n edition; use it if available.
- [ ] Verify the n8n account uses a strong password and MFA if available; limit admin access.
- [ ] Limit Google Sheets sharing and Gmail/Google OAuth permissions to the intended accounts.
- [ ] Keep TLS/HTTPS configured at your public reverse proxy.
- [ ] Confirm production webhook authentication before enabling it.
- [ ] Consider rate limiting and IP allowlisting where practical; do not disable justified restrictions to pass tests.

## Before uploading to GitHub

- [ ] Download workflow JSON from n8n; do not assume screenshots are importable.
- [ ] Search the JSON for token strings, `Authorization`, `X-IT-Ticket-Key`, webhook paths, email addresses, spreadsheet IDs, credential names and credential IDs, user data, and hard-coded URLs.
- [ ] Remove/anonymize secrets, identifying metadata, OAuth token values, custom headers, pinned sample data and credential references as needed.
- [ ] Check **all screenshots** for visible personal data or credentials.
- [ ] Include only fictional sample ticket requests and responses.
- [ ] Keep the production webhook URL private and never publish an actual secret.
- [ ] Confirm public documentation says **demonstration, not production-ready**.

## Important limitations

- [ ] Document that Google Sheets matching by requestId does not guarantee concurrent deduplication.
- [ ] Make human review mandatory for AI-generated troubleshooting advice.
- [ ] Before using genuine staff tickets, establish privacy, consent, access, and retention controls for data sent to OpenAI, Google Sheets, and Gmail.

**Current project status:** Main HTTP 200 / 400 / 409 cases tested and automatic error notification demonstrated. This checklist is deliberately unmarked; complete it after checking the live n8n environment.
