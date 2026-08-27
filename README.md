# n8n Automation JSON

A clean, well-documented collection of ready-to-import **n8n** workflows.

This repository contains three practical automations built with [n8n](https://n8n.io) — an open-source workflow automation tool. Each workflow lives in its own folder so it is easy to find, understand, and maintain.

---

## What’s Inside

| Folder | Workflow | What it does (in plain English) |
|--------|----------|---------------------------------|
| [`email-job-alert/`](./email-job-alert/) | **Email Job Alert** | Checks for new remote jobs every day, uses AI to summarise them, and emails you a clean HTML digest. |
| [`insurance-voice-bot/`](./insurance-voice-bot/) | **Halim Insurance Voice Bot** | A voice-enabled AI assistant for Halim Insurance. Users send voice notes; the bot transcribes, answers using company knowledge, and replies with spoken audio. |
| [`minimart-os/`](./minimart-os/) | **MiniMart OS** | A full Telegram shop assistant for a small retail store. Staff can record sales, restock items, and check prices — all tracked in Google Sheets. |

---

## How to Import Any Workflow

1. Open your n8n instance (self-hosted or n8n Cloud).
2. Go to **Workflows** → click the **⋯** menu → **Import from File**.
3. Select the `workflow.json` file from the folder you want.
4. After import, open the workflow and connect the required credentials (see each folder’s README).
5. Activate the workflow when you are ready.

> **Tip:** Always test with a small amount of data first. Credentials are never stored inside the JSON files — you must add them yourself after import.

---

## Repository Structure

```
n8n-Automation-JSON/
├── README.md                          ← You are here
├── email-job-alert/
│   ├── README.md                      ← Detailed explanation
│   └── workflow.json
├── insurance-voice-bot/
│   ├── README.md
│   └── workflow.json
└── minimart-os/
    ├── README.md
    └── workflow.json
```

---

## General Prerequisites

- An n8n instance (v1.0+ recommended)
- Accounts / API keys for the services used by each workflow (listed in the individual READMEs)
- Basic understanding of how to create credentials inside n8n

---

## Why This Structure?

- **One folder = one workflow** → easy to find and version-control
- Clear, layman-friendly documentation so anyone can maintain the workflows later
- No credentials or secrets are committed
- Ready for future workflows — just add a new folder following the same pattern

---

## Contributing / Updating

When you improve a workflow:

1. Export the updated JSON from n8n.
2. Replace the `workflow.json` in the correct folder.
3. Update the corresponding `README.md` if the behaviour changed.
4. Commit with a clear message (e.g. `feat(email-job-alert): limit jobs to 15 and improve HTML`).

---

## License

These workflows are shared for personal and educational use. Feel free to adapt them to your own needs.
