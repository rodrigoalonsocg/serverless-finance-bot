# 🤖 Serverless AI Finance Tracker

An automated, serverless personal finance bot built with **n8n**, integrated with **Telegram**, **OpenAI (GPT-4o-mini)**, and **Google Sheets**. 

Instead of relying on rigid, third-party expense tracking apps where I don't own my data, I engineered this custom pipeline to process natural language inputs, extract structured financial data, and securely log it into my own database.

## 🏗️ Architecture & Tech Stack

This project utilizes a microservices approach connected via webhooks and REST APIs:

* **Frontend / UI:** Telegram Bot API
* **Backend / Orchestrator:** n8n (Node-based workflow automation)
* **NLP / Processing:** OpenAI API (`gpt-4o-mini` model)
* **Database:** Google Sheets API (OAuth 2.0)

## ✨ Features

* **Natural Language Processing:** Users can type expenses naturally (e.g., *"Dinner with friends 85.50 PEN"*).
* **Automated Categorization:** The AI model parses the input and returns a clean, structured JSON object mapping the concept, exact amount, predefined category, and transaction type (income/expense).
* **Real-time Logging:** Instantly appends a new row in a connected Google Sheet with a timestamp.
* **Instant Feedback:** The bot replies via Telegram confirming the successful transaction log.
* **Data Ownership:** Complete control over the database for future data analysis or predictive modeling.

## 🚀 How it Works (The Workflow)

1. **Webhook Trigger:** The Telegram bot listens for incoming text messages from authorized User IDs.
2. **Data Extraction:** The text is sent to OpenAI with a strict system prompt to return only a formatted JSON object.
3. **Data Parsing:** n8n parses the JSON (`JSON.parse`) to map the variables (`amount`, `category`, `concept`).
4. **Database Insertion:** The Google Sheets node appends the parsed data into the designated columns.
5. **Confirmation:** A final Telegram node sends a Markdown-formatted receipt back to the user.

## 🛠️ Installation & Setup

If you want to replicate this environment:

1. Clone this repository.
2. Import the `workflow.json` file into your local or cloud-hosted n8n instance.
3. Configure your credentials within n8n:
   * **Telegram API Token** (via `@BotFather`).
   * **OpenAI API Key**.
   * **Google Sheets OAuth2 Credentials** (Client ID & Secret from Google Cloud Console).
4. Update the Google Sheets node with your specific Document ID and ensure your sheet has the correct headers (e.g., `Fecha`, `Concepto`, `Monto`, `Categoria`, `Tipo`).
5. Activate the workflow.

---
*Built by [Rodrigo Córdova](https://github.com/rdorigoalonsocg) - Data & Automation Enthusiast.*
