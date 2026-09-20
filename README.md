# 🤖 AI Customer Feedback Intelligence Agent

An end-to-end AI automation workflow built with **n8n** that reads raw customer feedback, extracts structured business insights using an LLM, stores the results in a database, and automatically alerts the team when a high-urgency complaint comes in.

---

## 💡 The Problem

Businesses receive large volumes of customer feedback every day — through chats, emails, reviews, and support tickets. Manually reading and categorizing each message is:

- Slow and inconsistent
- Hard to scale as feedback volume grows
- Risky — urgent complaints can get buried and missed until it's too late

## 🛠️ The Solution

This project automates the entire feedback analysis pipeline. Instead of a human reading and tagging every message, an AI Agent does it instantly and consistently — then routes high-priority issues straight to the team's inbox.

---

## 🔄 How It Works

```
Customer Feedback (Chat Input)
            │
            ▼
        AI Agent (OpenAI)
            │
            ▼
   Structured Output Parser
   (Sentiment, Topic, Complaint,
   Intent, Urgency, Action, Summary)
            │
            ▼
   PostgreSQL Database (Supabase)
            │
            ▼
      IF Urgency = High?
            │
           YES
            │
            ▼
     Automated Email Alert
        (Gmail)
```

---

## ✅ Features

- **Sentiment Detection** — classifies feedback as Positive, Neutral, or Negative
- **Topic & Complaint Extraction** — identifies the core issue, even in multi-topic messages
- **Intent Classification** — Praise, Complaint, Question, Suggestion, Request, or Other
- **Urgency Scoring** — Low, Medium, or High
- **Suggested Action** — a practical, business-ready recommendation
- **Auto-Summary** — a concise summary of every feedback message
- **Structured JSON Output** — enforced via n8n's Structured Output Parser for consistent, reliable data
- **Persistent Storage** — every analysis is saved to a PostgreSQL (Supabase) database for tracking and reporting
- **Real-Time Alerts** — high-urgency complaints trigger an instant email notification, so nothing critical is missed

---

## 🧰 Tech Stack

| Component | Tool |
|---|---|
| Workflow Automation | [n8n](https://n8n.io) |
| Language Model | OpenAI (GPT) |
| Output Structuring | n8n Structured Output Parser |
| Database | PostgreSQL via [Supabase](https://supabase.com) |
| Notifications | Gmail API |

---

## 📥 Sample Input

```
The food was delicious and the staff was very friendly, but my delivery was
extremely late. I waited almost an hour and nobody answered my call.
```

## 📤 Sample Output

```json
{
  "sentiment": "Negative",
  "topic": "Delivery delay and unresponsive support",
  "complaint": "Delivery was almost an hour late and nobody answered the customer's calls.",
  "intent": "Complaint",
  "urgency": "High",
  "suggested_action": "Apologize to the customer, investigate the delivery delay and why calls were not answered, and offer a refund or discount.",
  "summary": "Customer praised the food and staff but experienced a significantly delayed delivery and unanswered support calls."
}
```

---

## 🗄️ Database Schema

```sql
CREATE TABLE customer_feedback (
  id SERIAL PRIMARY KEY,
  feedback_text TEXT,
  sentiment TEXT,
  topic TEXT,
  complaint TEXT,
  intent TEXT,
  urgency TEXT,
  suggested_action TEXT,
  summary TEXT,
  created_at TIMESTAMP DEFAULT NOW()
);
```

---

## 📸 Screenshots

**Complete Workflow**
![Workflow Diagram](screenshots/workflow-diagram.png)

**Execution Log — AI Agent Analyzing Feedback**
![Execution Log](screenshots/execution-log.png)

**Automated High-Urgency Email Alert**
![Email Alert](screenshots/email-notification.png)

---

## ⚙️ Setup (High-Level)

1. Import `workflow.json` into your n8n instance.
2. Connect your own **OpenAI**, **PostgreSQL (Supabase)**, and **Gmail** credentials — these are *not* included in the exported workflow for security reasons.
3. Run the SQL schema above in your Supabase SQL editor to create the `customer_feedback` table.
4. Update the email recipient in the Gmail node to your own address.
5. Activate the workflow and test via the built-in n8n chat trigger.

> ⚠️ No API keys, passwords, or tokens are stored in `workflow.json`. You must add your own credentials after importing.

---

## 🚀 Future Improvements

- Multi-channel intake (web form, WhatsApp, email inbox) via API trigger
- Live analytics dashboard (sentiment trends, top complaint categories)
- Slack/Telegram notifications as an alternative to email
- Automatic response drafting for common complaint types
- Multi-language feedback support

---

## 🧑‍💻 About This Project

This project was built as a hands-on exploration of practical AI automation — going beyond simple chatbot demos to build a system that makes real, structured, business-relevant decisions from unstructured text, end to end.

