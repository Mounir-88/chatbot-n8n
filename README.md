# Multilingual Chatbot with n8n

This project implements a multilingual Telegram chatbot using n8n.
It detects the user’s language, translates responses, and logs all interactions to Google Sheets.

## Setup

1. Clone the repo:
   ```bash
   git clone https://github.com/Mounir-88/chatbot-n8n.git
   cd chatbot-n8n

2. Install dependencies:
    ```bash
    npm install

3. Configure .env:

    TELEGRAM_BOT_TOKEN=your-token
>>  GOOGLE_SHEET_ID=your-sheet-id
>>  PUBLIC_URL=https://your-tunnel.trycloudflare.com

5. Run n8n locally:
    ```bash
    $env:WEBHOOK_URL="PUBLIC_URL"
>> n8n


