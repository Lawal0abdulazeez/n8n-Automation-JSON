# n8n Automation JSON

A clean, well-documented collection of ready-to-import **n8n** workflows.

This repository contains three practical automations built with [n8n](https://n8n.io) — an open-source workflow automation tool. Each workflow has its own documentation folder so it is easy to find, understand, and maintain.

---

## What’s Inside

| Documentation Folder | Workflow File | What it does (in plain English) |
|----------------------|---------------|---------------------------------|
| [`email-job-alert/`](./email-job-alert/) | [`Email Job Alert 2.json`](./Email%20Job%20Alert%202.json) | Checks for new remote jobs every day, uses AI to summarise them, and emails you a clean HTML digest. |
| [`insurance-voice-bot/`](./insurance-voice-bot/) | [`Halim_Insurance_Voice_Bot222 copy.json`](./Halim_Insurance_Voice_Bot222%20copy.json) | A voice-enabled AI assistant for Halim Insurance. Users send voice notes; the bot transcribes, answers using company knowledge, and replies with spoken audio. |
| [`minimart-os/`](./minimart-os/) | [`MiniMart OS - Full System.json`](./MiniMart%20OS%20-%20Full%20System.json) | A full Telegram shop assistant for a small retail store. Staff can record sales, restock items, and check prices — all tracked in Google Sheets. |

---

## How to Import Any Workflow

1. Open your n8n instance (self-hosted or n8n Cloud).
2. Go to **Workflows** → click the **⋯** menu → **Import from File**.
3. Select the `.json` file of the workflow you want (see table above).
4. After import, open the workflow and connect the required credentials (see each folder’s README for details).
5. Activate the workflow when you are ready.

> **Tip:** Always test with a small amount of data first. Credentials are never stored inside the JSON files — you must add them yourself after import.

---

## Repository Structure

```
n8n-Automation-JSON/
├── README.md                                      ← You are here
├── Email Job Alert 2.json                         ← Workflow 1
├── Halim_Insurance_Voice_Bot222 copy.json         ← Workflow 2
├── MiniMart OS - Full System.json                 ← Workflow 3
├── email-job-alert/
│   └── README.md                                  ← Detailed explanation
├── insurance-voice-bot/
│   └── README.md
└── minimart-os/
    └── README.md
```

---

## General Prerequisites

- An n8n instance (v1.0+ recommended)
- Accounts / API keys for the services used by each workflow (listed in the individual READMEs)
- Basic understanding of how to create credentials inside n8n

---

## Why This Structure?

- Clear, layman-friendly documentation so anyone can maintain the workflows later
- One documentation folder per workflow
- No credentials or secrets are committed
- Ready for future workflows — just add a new folder + JSON following the same pattern

---

## Contributing / Updating

When you improve a workflow:

1. Export the updated JSON from n8n and replace the corresponding file in the root.
2. Update the corresponding `README.md` if the behaviour changed.
3. Commit with a clear message (e.g. `feat(email-job-alert): limit jobs to 15 and improve HTML`).

---

## License

These workflows are shared for personal and educational use. Feel free to adapt them to your own needs.
