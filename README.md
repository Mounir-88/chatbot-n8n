# Multilingual Telegram Chatbot with n8n + Google Gemini

This project implements a **multilingual Telegram chatbot** using [n8n](https://n8n.io/) and **Google Gemini API**.  
The bot:
- Detects the user’s language.  
- Responds intelligently in the same language using **Gemini AI**.  
- Logs all conversations to Google Sheets (timestamp, user, message, response, language).  

---

## Setup Instructions (Local, with npm)

### 1. Install n8n globally
```bash
npm install -g n8n
```

Verify installation:
```bash
n8n --version
```

---

### 2. Clone this repository
```bash
git clone https://github.com/Mounir-88/chatbot-n8n.git
cd chatbot-n8n
```

---

### 3. Configure environment variables
Create a file called `.env` in the project root and add:

```env
TELEGRAM_BOT_TOKEN=your-telegram-bot-token
GOOGLE_SHEET_ID=your-google-sheet-id
PUBLIC_URL=https://your-tunnel.trycloudflare.com
GEMINI_API_KEY=your-gemini-api-key
```

- **TELEGRAM_BOT_TOKEN** → from [@BotFather](https://t.me/botfather).  
- **GOOGLE_SHEET_ID** → the ID part of your Google Sheet URL:  
  `https://docs.google.com/spreadsheets/d/<THIS_PART>/edit#gid=0`  
- **PUBLIC_URL** → a public HTTPS URL (from Cloudflare Tunnel, ngrok, etc).
- **GEMINI_API_KEY** → get one from [Google AI Studio](https://aistudio.google.com)
---

### 4. Start a public tunnel
Run Cloudflare Tunnel (or ngrok) to expose n8n:

```bash
cloudflared tunnel --url http://localhost:5678
```

Copy the generated URL (e.g. `https://xxxx.trycloudflare.com`) and update `PUBLIC_URL` in `.env`.

---

### 5. Run n8n
Start n8n with your webhook URL:

**Windows PowerShell**
```bash
$env:WEBHOOK_URL=$env:PUBLIC_URL
n8n
```

**Linux / macOS**
```bash
export WEBHOOK_URL=$PUBLIC_URL
n8n
```

n8n will now be available at:  
[http://localhost:5678](http://localhost:5678)

---

### 6. Import the workflow
1. Open the n8n editor (`http://localhost:5678`).  
2. Click **Import** → upload `workflows/telegram-chatbot.json`.  
3. Add **Telegram API** credentials (Bot token).  
4. Add **Google Sheets** credentials (OAuth2).  
5. Add **Gemini API** credentials (GEMINI_API_KEY).
6. Activate the workflow.

---

## Project Structure
```
chatbot-n8n/
├── workflows/             # Exported n8n workflows (.json)
│   └── telegram-chatbot.json
├── .env                   # Environment variables (ignored in GitHub)
├── README.md              # Documentation
```

---

## Features
- Multilingual support with automatic language detection.
- Gemini AI integration for **intelligent, context-aware responses**.
- Telegram integration (receive + send messages).
- Logs interactions to Google Sheets:
  - Timestamp
  - User ID / Username
  - User Message
  - Bot Response
  - Language Detected
- General error handling: fallback message ("Sorry, I wasn’t able to understand. Please try again.").

---

## Limitations
- Requires n8n to be running for the bot to respond.  
- Cloudflare/ngrok tunnel must stay active for Telegram webhooks.  
- Free Gemini quota may be limited; check [Google AI Studio](https://aistudio.google.com) for usage.  

---

## Future Improvements
- Deploy permanently (Render, Railway, Fly.io, or n8n.cloud).  
- Add WhatsApp support alongside Telegram.  
- Extend conversation logic (order processing, FAQs, etc).  
