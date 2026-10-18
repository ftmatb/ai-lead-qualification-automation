# AI Lead Qualification & Follow-up Automation

A locally tested AI-assisted workflow that captures customer inquiries, classifies sales leads, stores their details, and prepares personalized email drafts for human review.

> **Status:** Functional local prototype. Not production-ready or publicly hosted.

## What it does

1. **Lead Form** receives a customer's name, email address, phone number, and inquiry.
2. **Ollama / Qwen 2.5 3B** analyzes the inquiry and returns a lead classification (`Hot`, `Warm`, or `Cold`), reasoning, an email subject, and an email body.
3. **Google Sheets** records the inquiry and classification in a `Leads` worksheet.
4. **Gmail** creates a reply **draft** for human review. The workflow does **not** automatically send the email.

```text
Lead Form --> Ollama (Qwen 2.5 3B) --> Google Sheets --> Gmail Draft
```

## Technology

- n8n Community Edition (local workflow automation)
- Docker Desktop (local n8n runtime)
- Ollama with `qwen2.5:3b` (local language model)
- Google Sheets and Gmail APIs
- Google Cloud OAuth credentials

## Demonstrated results

A test inquiry for a solar installation service was processed end to end. The workflow execution was marked successful in n8n, the classification appeared in Google Sheets, and a Gmail draft was created. These are **functional tests with sample data**, not security, uptime, or load tests.

## Local environment

The n8n instance was developed on an Apple Silicon Mac. The form URL in this environment is:

`http://localhost:5678/form/lead-intake`

`localhost` means the form is **not accessible to external customers**. A production-style path does not make the service publicly hosted.

## Configuration overview

The workflow requires:

1. A running n8n instance and a locally accessible Ollama service with `qwen2.5:3b` available.
2. An n8n form trigger with Name, Email, Phone, and Message fields.
3. An Ollama model node configured to return structured output containing `classification`, `reasoning`, `email_subject`, and `email_body`.
4. A Google Sheet with a `Leads` tab and the columns: `Timestamp`, `Name`, `Email`, `Phone`, `Message`, `Classification`, `Reasoning`.
5. Authorized Google Sheets and Gmail credentials in n8n, with the Gmail step set to create a draft.

**Reproducibility note:** Exact Docker networking, Ollama prompts, OAuth setup, and node mappings depend on the exported n8n workflow and local configuration. They have not been packaged as a complete, independently verified installation guide yet.

## Project files

The n8n workflow has been exported separately as JSON. Before publishing that export, review it for email addresses, instance details, IDs, or other sensitive configuration. **Never commit credentials, OAuth client secrets, access tokens, or real customer information.**

## Limitations and next steps

- No public hosting or guaranteed uptime
- No verified production security hardening
- No tested backup restoration or incident response process
- No automated monitoring or comprehensive failure handling
- No GDPR/commercial deployment review completed
- No independent installation or load test completed

Next steps: safely package the workflow export, add sanitized screenshots, verify a repeatable setup procedure, and test failures before considering any commercial deployment.

## Intended use

A learning and portfolio project demonstrating business-process automation, local AI integration, lead triage, Google API integrations, and draft-based human-in-the-loop communication.
