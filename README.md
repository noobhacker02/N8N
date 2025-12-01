# 🌟 n8n Automation Hub
### AI-Powered Workflow Collection for Real-World Business Efficiency

A refined collection of **8 production-ready automation systems** built using **n8n**, **Google Gemini**, **Mistral**, **Retell Voice AI**, and standard business tools. These workflows turn manual operational tasks into autonomous agents—handling everything from personal logistics to complex voice-driven data entry.

> **Project Goal:** To create a "Second Brain" and automated workforce that eliminates repetitive admin work, improves data hygiene, and allows for infinite scaling of personal and business operations without adding headcount.

---

## ⚡ Quick Index

| # | Workflow Name | Description |
|---|---|---|
| **1** | **Unified Telegram "Life OS" Agent** | **(Flagship)** A hyper-personalized AI agent acting as "Talha." Manages Calendar, Gmail, Contacts, & Tasks via Telegram with vision capabilities. |
| **2** | **Smart Invoice-to-Sheet Pipeline** | Auto-extracts invoice data (OCR) from Drive and logs structured rows in Sheets. |
| **3** | **AI Invoice Intake & Approval** | Routes invoices for email approval and tracks status; centralizes procurement. |
| **4** | **Google Maps Lead Finder** | Scrapes and cleans business leads from Maps based on location/category. |
| **5** | **Gmail Outreach Engine** | Automates cold outreach and smart follow-ups based on recipient engagement. |
| **6** | **RAG Knowledge Assistant** | Chatbot that answers questions based on internal company files (Drive/Pinecone). |
| **7** | **AI Email Support Bot** | Auto-drafts or sends replies to customer support tickets with complexity fallback. |
| **8** | **Retell Voice Scheduler** | Voice agent that answers calls, checks Calendar availability, and books appointments. |

---

## 🧠 1. Unified Telegram "Life OS" Agent (The Flagship)

**The "Second Brain" of the operation.** This is not just a chatbot; it is an autonomous agent designed to embody the user's specific persona ("Talha") to manage personal and professional logistics via a single chat interface.

### 🛠 Tech Stack
* **Orchestration:** n8n (Self-Hosted/Cloud)
* **Core Brain:** Google Gemini 1.5 Flash (via LangChain Agent)
* **Vision Engine:** Mistral Large (via HTTP Request) for image analysis
* **Memory:** Window Buffer Memory (Short-term context retention)
* **Integrations:** Google Calendar, Gmail, Google Contacts, Google Sheets, Airtable, Slack
* **Protocol:** MCP (Model Context Protocol) for external tool connections

### 🔍 Deep Dive: Capabilities & Logic
This workflow is the most complex in the collection, featuring **65+ nodes** working in concert.

1.  **Identity & Security Layer**
    * **Persona Enforcement:** The system prompt forces the AI to "think, act, and speak like Talha," ensuring responses align with the user's specific tone and decision-making style.
    * **Strict Authorization:** A **Switch Node** immediately validates the incoming Telegram `chat_id`. If the ID does not match the owner, the workflow terminates with a "Not Authorized" rejection, preventing unauthorized access to personal data.

2.  **Multi-Modal Vision (The "Eyes")**
    * When an image is sent (e.g., a flyer, receipt, or handwritten note), the workflow branches to an **HTTP Request node** calling the **Mistral API**.
    * It generates a detailed text description of the image, which is then fed back into the Gemini Agent.
    * *Use Case:* Snap a photo of a wedding invitation -> Agent reads the date/time -> Agent adds it to Google Calendar automatically.

3.  **Advanced Tool Usage (The "Hands")**
    * **Calendar Management:** The agent uses 4 separate tools (`get`, `create`, `update`, `delete`) to manage schedule conflicts in real-time. It can "find a free slot next Tuesday" or "move my 3 PM meeting to 4 PM."
    * **Gmail Command Center:** It can read unread emails, draft replies (saved to Drafts for review), send urgent emails immediately, and organize inboxes by adding labels.
    * **CRM Control:** Direct access to **Google Contacts** allows the agent to create new contacts from chat ("Add Faizan, his number is...") or update existing details.
    * **Audit Logging:** Every single interaction—what was asked, what was answered, and the timestamp—is appended to **Google Sheets** and **Airtable** for a permanent audit trail.

4.  **Extensibility via MCP**
    * The workflow includes **MCP Client** nodes. This allows the n8n agent to connect to external "Model Context Protocol" servers, enabling it to execute local Python scripts or access tools that don't have standard APIs.

---

## 📄 2. Smart Invoice-to-Sheet Pipeline

**Purpose:** Replaces manual data entry. The flow watches a Google Drive folder for new PDFs, uses AI to extract key fields, and appends a clean row to a master Finance Sheet.

### 🛠 Tech Stack
* **Trigger:** Google Drive Trigger (File Created)
* **OCR/Vision:** Google Gemini Vision or Mistral (via API)
* **Data Processing:** JSON Parser
* **Storage:** Google Sheets

### ⚙️ How It Works
1.  **Detection:** A specialized folder in Drive is monitored.
2.  **Extraction:** New PDFs are downloaded and sent to the Vision model with a prompt to "Extract Invoice Number, Date, Vendor, Total, and Tax as JSON."
3.  **Structuring:** The raw text response is cleaned and parsed into a valid JSON object.
4.  **Logging:** Data is mapped to specific columns in the Finance Tracker sheet.

---

## ✅ 3. AI-Based Invoice Intake & Approval System

**Purpose:** A governance layer for finance. Invoices are routed to managers for "Approve" or "Reject" decisions before payment.

### 🛠 Tech Stack
* **Input:** Email Trigger (IMAP) or Typeform
* **Logic:** n8n Approval Node (Wait for Email Click)
* **Notifications:** Gmail (SMTP)
* **Tracking:** Google Sheets

### ⚙️ How It Works
1.  **Intake:** Invoice received via email.
2.  **Routing:** n8n generates a unique "Approval Link" and emails it to the designated manager.
3.  **Pause:** The workflow *pauses* execution and waits for the manager to click the link.
4.  **Decision:**
    * *If Approved:* Invoice is marked "Paid" in the sheet, and a confirmation is sent to the vendor.
    * *If Rejected:* The sheet is updated, and the vendor gets a rejection notice with feedback.

---

## 🗺 4. Google Maps Lead Finder

**Purpose:** A scaling tool for sales. Scrapes and cleans business leads from Google Maps based on location/category.

### 🛠 Tech Stack
* **Data Source:** Google Maps API (Places Text Search) or Serper.dev
* **Processing:** JavaScript Code Node (Deduplication)
* **Validation:** Phone Number Parser
* **Output:** Google Sheets

### ⚙️ How It Works
1.  **Input:** User provides a list of keywords (e.g., "Dentists in Dubai") and ZIP codes.
2.  **Search:** The workflow iterates through the list, querying the Maps API for business names, phone numbers, and websites.
3.  **Cleaning:** Results are filtered to remove duplicates and entries without contact info.
4.  **Export:** A clean, actionable prospect list is generated in Sheets.

---

## 📧 5. Gmail Outreach + Smart Follow-Up Engine

**Purpose:** A "set and forget" sales engine. Sends personalized emails and automatically follows up only if the lead hasn't responded.

### 🛠 Tech Stack
* **Database:** Google Sheets (Lead Status)
* **Email:** Gmail Node (Send & Threading)
* **AI:** OpenAI GPT-4o (Personalization)
* **Logic:** Wait Nodes & If/Else Filters

### ⚙️ How It Works
1.  **Drafting:** AI reads the prospect's website/LinkedIn (if available) and writes a personalized opening line.
2.  **Sending:** The initial email is sent.
3.  **Monitoring:** The workflow waits for a set duration (e.g., 3 days).
4.  **Check:** It checks the thread for a reply.
    * *No Reply:* A polite follow-up is sent automatically.
    * *Replied:* The workflow stops and alerts the sales rep.

---

## 📚 6. AI Knowledge Assistant (RAG)

**Purpose:** An internal search engine. Employees ask questions and get answers based *only* on internal company files.

### 🛠 Tech Stack
* **Vector Database:** Pinecone
* **Embedding Model:** text-embedding-3-small (OpenAI) or Gemini Embedding
* **Chat Logic:** LangChain Retrieval QA
* **Source:** Google Drive

### ⚙️ How It Works
1.  **Ingestion:** New PDFs in Drive are automatically text-split and converted into vector embeddings.
2.  **Storage:** Vectors are stored in Pinecone.
3.  **Retrieval:** When a user asks a question, the system searches Pinecone for the most relevant document chunks.
4.  **Synthesis:** Gemini summarizes the chunks into a coherent answer, citing the source document.

---

## 📨 7. AI Email Support Assistant

**Purpose:** A Tier-1 support agent. Classifies customer intent and drafts responses, handling volume that would drown a human team.

### 🛠 Tech Stack
* **Trigger:** Gmail Trigger (New Email)
* **Classifier:** Google Gemini Flash (Fast & Cheap)
* **Complex Reasoner:** OpenAI GPT-4 (For hard cases)
* **Output:** Gmail Drafts

### ⚙️ How It Works
1.  **Classification:** Incoming emails are tagged by intent (e.g., "Refund," "Technical Issue," "Spam").
2.  **Routing:**
    * *Simple:* Gemini Flash drafts a quick response based on FAQs.
    * *Complex:* GPT-4 analyzes the issue and drafts a detailed troubleshooting guide.
3.  **Review:** The reply is saved as a **Draft**. The support agent just reviews and hits "Send."

---

## 🎤 8. Retell Voice AI — Calendar Checker

**Purpose:** A receptionist that never sleeps. Handles voice calls, checks live availability, and books appointments.

### 🛠 Tech Stack
* **Voice Engine:** Retell AI (Telephony & Speech-to-Text)
* **Logic:** n8n Webhooks
* **Calendar:** Google Calendar API
* **Knowledge:** Retell Vector DB (for FAQs)

### ⚙️ How It Works
1.  **Call Start:** Retell answers the phone and greets the caller.
2.  **Intent:** When the caller says "I want to book a meeting," Retell fires a webhook to n8n.
3.  **Availability:** n8n checks Google Calendar for free slots in the next 3 days and returns them to Retell.
4.  **Booking:** The caller picks a time. Retell sends the data back to n8n, which creates the Calendar event and sends a confirmation email.

---

## 🚀 Deployment Guide

1.  **Import:** Load the `.json` workflow files into your n8n instance.
2.  **Credentials:**
    * **Google Cloud:** Create a project with OAuth scopes for Calendar, Gmail, Drive, Sheets, and Contacts. Connect to n8n.
    * **AI Keys:** Add API keys for Gemini, Mistral, and OpenAI.
    * **Telegram:** Create a bot via BotFather and add the Token to the Telegram nodes.
3.  **Configuration:**
    * **Auth:** In Workflow #1 (Telegram Agent), update the **Switch Node** to include your specific Telegram `chat_id`. **This is critical for security.**
    * **IDs:** Replace placeholder IDs (Google Sheet ID, Calendar ID, Airtable Base ID) with your own asset IDs.
4.  **Webhooks:** For the Invoice and Voice flows, update the webhook URLs in your external services (e.g., Retell dashboard) to point to your production n8n instance.

## 🔐 Security Note

* **PII:** These workflows process personal data (emails, contacts). Ensure logs are secured.
* **Access Control:** The Telegram bot includes a hard-coded ID check. Do not remove this, or anyone on Telegram could manage your calendar.
* **Secrets:** Never commit your n8n credential exports or JSON files containing raw API keys to public repositories.

---

**Author:** Talha Shaikh
**License:** MIT
