# MiniMart OS – Full System

**What it does (simple version)**  
A complete Telegram bot that acts as a digital assistant for a small shop or mini-mart.  

Shop staff can:
- Record a **sale**
- **Restock** items
- **Check the price** of any product

Everything is stored and tracked in a Google Sheet called **MiniMart Hub**. The bot remembers what each user is currently doing (the “context”) so conversations feel natural.

---

## How It Works (High-Level Flow)

```
Telegram message arrives
        ↓
Router decides: is it /start, a button click, or free text?
        ↓
┌─────────────────┬──────────────────┬─────────────────┐
│     /start      │  Button click    │   Free text     │
│ Reset session   │ (Sale / Restock  │ Look up what    │
│ Show main menu  │  / Check Price)  │ the user is     │
└─────────────────┴──────────────────┴─────────────────┘
        ↓
Google Sheets keeps a small “session” for every user
(Current_Context + temporary data)
        ↓
Depending on context → ask for product name → ask for quantity → log the transaction → reply with confirmation
```

---

## Main Features

| Feature | What the user does | What the system does |
|---------|--------------------|----------------------|
| **Start / Reset** | Sends `/start` | Clears previous context and shows the main menu with buttons |
| **Record Sale** | Taps “Sale” → types product name → chooses quantity | Looks up the item, reduces stock, logs the sale, sends confirmation |
| **Restock** | Taps “Restock” → types product name → chooses quantity | Looks up the item, increases stock, logs the restock |
| **Check Price** | Taps “Check Price” → types product name | Finds the item and replies with current price and stock level |
| **Cancel** | Taps Cancel or sends cancel | Clears the current operation |

---

## Google Sheet Structure (MiniMart Hub)

The workflow expects a Google Spreadsheet with at least these sheets:

| Sheet Name | Purpose | Key Columns |
|------------|---------|-------------|
| **Inventory_Master** | Current stock and prices | Product Name, Unit Price, Current Stock, … |
| **Bot_Sessions** | Tracks what each Telegram user is doing | User_ID, Current_Context, Temp_Data |
| (Transactions / Logs) | Optional history of sales & restocks | Timestamp, Type, Product, Quantity, User, … |

You will need to create these sheets (or adapt the node column mappings) before the bot works correctly.

---

## What You Need to Set Up

| Credential / Setting | Purpose | Notes |
|----------------------|---------|-------|
| **Telegram Bot Token** | Receive messages & send replies | Create a bot with @BotFather |
| **Google Sheets OAuth2** | Read/write inventory and sessions | Share the spreadsheet with the Google account you connect in n8n |
| Spreadsheet ID | Already present in the nodes | Change it if you use a different sheet |

---

## How to Customise

- **Add more menu options** → Edit the main menu Telegram node and the Router: Button Clicks node.
- **Change the currency or message style** → Edit the text inside the Telegram “Send …” nodes (many messages already use ₦).
- **Add new contexts** (e.g. “View low stock”) →  
  1. Add a new button  
  2. Create a “Set Context: …” Google Sheets node  
  3. Add a new branch in “Router: Context”
- **Log more details** → Expand the “Log Transaction” nodes to write extra columns.

---

## Workflow File

- [`MiniMart OS - Full System.json`](../MiniMart%20OS%20-%20Full%20System.json) — the complete n8n workflow (ready to import)

---

## Maintenance Tips

- The bot relies heavily on the **Bot_Sessions** sheet. Never delete columns that the workflow uses (User_ID, Current_Context, Temp_Data).
- If product names are typed with different spellings, consider adding a fuzzy-search step later.
- Because the flow is stateful, always test the full path (start → choose action → type product → choose quantity) after any change.
- The workflow is currently set to **inactive**. Activate it only after you have connected the correct Telegram bot and Google Sheet.
