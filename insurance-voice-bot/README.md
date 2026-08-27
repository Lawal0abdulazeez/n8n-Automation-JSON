# Halim Insurance Voice Bot

**What it does (simple version)**  
This is a voice-powered customer support agent for Halim Insurance.  
A user records a short voice message → the bot turns the speech into text → looks up the answer in a knowledge base → speaks the answer back as audio.

It is designed to be connected to any front-end that can send audio and receive audio (for example a custom web app, WhatsApp voice notes, or a phone system).

---

## How It Works (Step by Step)

1. **Webhook**  
   Receives a POST request that contains the user’s voice recording (as base64 audio).

2. **Code node**  
   Converts the base64 string into a proper binary file that n8n can work with.

3. **Transcribe a recording (Google Gemini)**  
   Turns the spoken words into written text using Google’s Gemini model.

4. **AI Agent + Google Gemini Chat Model**  
   The main brain of the bot.  
   It receives the transcribed question and is instructed to act as “Halim Insurance Assistant”.

5. **Pinecone Vector Store + OpenAI Embeddings**  
   This is the bot’s memory (RAG – Retrieval Augmented Generation).  
   When the agent needs company-specific information (policies, claims process, product details, etc.), it searches the Pinecone index named `halim`.

6. **Generate audio (OpenAI)**  
   Takes the agent’s text answer and converts it into natural-sounding speech.

7. **Code node**  
   Prepares the audio as base64 so it can be sent back easily.

8. **Respond to Webhook**  
   Returns the audio (and any other data) to the original caller.

---

## What You Need to Set Up

| Credential / Service | Purpose | Notes |
|----------------------|---------|-------|
| **Google Gemini** (or Google AI) | Transcription + chat model | Used for speech-to-text and the main LLM |
| **OpenAI** | Text-to-speech + embeddings | Needed for voice generation and vector search |
| **Pinecone** | Knowledge base | Create an index called `halim` and upload your insurance documents |
| Webhook path | Already set in the workflow | You can change the path if you want |

---

## Important Notes About the Knowledge Base

The quality of the answers depends almost entirely on what you put into the Pinecone index `halim`.

Recommended content to upload:
- Product brochures
- Claims process guides
- FAQ documents
- Policy wordings
- Contact and branch information

You can keep the documents in a Google Drive folder and use another n8n workflow to automatically keep the vector store up to date.

---

## How to Customise

- **Change the personality or rules** → Edit the System Message inside the AI Agent node.
- **Use a different voice** → Look at the options in the “Generate audio” node.
- **Switch LLM models** → You can replace Google Gemini with OpenAI, Claude, or any other model n8n supports.
- **Add more tools** → The AI Agent can call extra tools (e.g. check claim status in a CRM) if you attach them.

---

## File in This Folder

- `workflow.json` — the complete n8n workflow (ready to import)

---

## Maintenance Tips

- Keep the Pinecone index updated whenever policies change.
- Monitor token usage (both Gemini and OpenAI) if the bot becomes popular.
- The webhook currently expects the audio in `body.audio_base64`. Adjust the Code node if your front-end sends the data differently.
- The workflow is currently set to **inactive**. Activate it only after testing the full voice loop.
