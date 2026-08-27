# Email Job Alert

**What it does (simple version)**  
Every day this workflow looks for new remote job postings, picks the most relevant ones, asks an AI to write a nice summary, and sends you a clean HTML email so you don’t have to scroll through dozens of listings yourself.

---

## How It Works (Step by Step)

1. **Schedule Trigger**  
   Runs automatically on a schedule you choose (for example every morning at 8 AM).

2. **HTTP Request**  
   Fetches the latest jobs from the public RemoteOK API (`https://remoteok.com/api`).

3. **Code nodes (filter & format)**  
   - Removes the metadata row that the API returns.  
   - Limits the number of jobs (currently 10) so the workflow stays fast and cheap.  
   - Prepares the data so the AI can read it easily.

4. **Filter**  
   Keeps only jobs that match the tags or keywords you care about (you can change these later).

5. **Basic LLM Chain + OpenAI Chat Model**  
   Sends the jobs to OpenAI and asks it to turn them into neat HTML blocks.  
   The prompt tells the AI exactly how each job should look.

6. **Code – Build HTML Email**  
   Wraps the AI’s output in a full, professional-looking HTML email with today’s date and a simple header.

7. **Gmail – Send Alert**  
   Sends the finished email to your inbox.

---

## What You Need to Set Up

| Credential / Setting | Where to get it | Notes |
|----------------------|-----------------|-------|
| **OpenAI API** | [platform.openai.com](https://platform.openai.com) | Used by the Chat Model node |
| **Gmail OAuth2** | Create inside n8n → Credentials → Gmail | Needs permission to send email |
| Schedule | Inside the Schedule Trigger node | Change the cron or interval as you like |

---

## How to Customise

- **Change how often it runs** → Edit the Schedule Trigger node.
- **Get more or fewer jobs** → Look inside the “Code – Format Jobs” node and change the `.slice(0, 10)`.
- **Filter by different keywords** → Edit the Filter1 node or the Code node that builds the `tags_string`.
- **Change the email style** → Edit the HTML template inside “Code – Build HTML Email”.
- **Change the AI’s writing style** → Edit the prompt in the Basic LLM Chain node.

---

## File in This Folder

- `workflow.json` — the complete n8n workflow (ready to import)

---

## Maintenance Tips

- If the RemoteOK API changes its response format, the two Code nodes may need small updates.
- Keep an eye on OpenAI costs if you raise the job limit a lot.
- The workflow is currently set to **inactive**. Activate it only after you have tested it successfully.
