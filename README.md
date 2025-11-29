# 🌟 n8n Automation Hub  
### AI-Powered Workflow Collection for Real-World Business Teams

A refined set of **7 production-ready automation systems** built using n8n, AI models (Gemini, OpenAI, Mistral), Retell Voice AI, and common business tools. These flows eliminate repetitive work, improve accuracy, and help teams operate at a higher level without extra engineering overhead.

---

## 📄 1. Smart Invoice-to-Sheet Pipeline

**Purpose:**  
Replace manual invoice entry with an automated, AI-assisted pipeline.

**How it works:**  
- Detects new invoices in Google Drive  
- Uses AI OCR (Mistral) for multilingual text extraction  
- Captures vendor, date, totals, tax, line items  
- Inserts structured rows into Google Sheets  
- Optional add-ons: tax logic, currency conversion, validation, error handling  

**Best for:**  
Small finance teams, accountants, and businesses dependent on Google Sheets workflows.

---

## ✅ 2. AI-Based Invoice Intake & Approval System

**Purpose:**  
Centralize invoice intake and automate the approval loop.

**How it works:**  
- Accepts invoices via Gmail, Drive, or web uploads  
- AI classifies and extracts core fields  
- Routes invoices to approvers via email  
- Tracks approval/rejection status + comments in Google Sheets  
- Full traceability across the workflow  

**Best for:**  
Finance, procurement, and operations teams requiring structure and speed.

---

## 🗺 3. Google Maps Lead Finder

**Purpose:**  
Automate large-scale lead collection from Google Maps.

**How it works:**  
- Inputs: ZIP codes + business categories  
- Queries Google Maps API  
- Removes duplicates and noisy entries  
- Stores verified results in Google Sheets  
- Handles API rate limits with exponential backoff  

**Best for:**  
Sales and marketing teams that need clean, repeatable lead generation.

---

## 📧 4. Gmail Auto Outreach + Smart Follow-Up Engine

**Purpose:**  
Consistent outreach without manual tracking.

**How it works:**  
- Recipients + templates stored in Google Sheets  
- Sends initial outreach automatically  
- Detects who replied and who didn’t  
- Sends follow-ups only to non-responders  
- Avoids weekend sends to protect domain reputation  

**Best for:**  
Sales teams, freelancers, agencies, and consultants.

---

## 🤖 5. AI Knowledge Assistant (RAG Chatbot for Company Files)

**Purpose:**  
Instant access to company knowledge without searching through folders.

**How it works:**  
- Auto-detects new/updated files in Google Drive  
- Splits documents and generates embeddings (Gemini)  
- Stores them in Pinecone for fast semantic retrieval  
- Chat interface delivers context-rich answers  
- Short-term memory enables natural multi-turn conversations  

**Best for:**  
Teams with large document libraries (HR, operations, onboarding, sales enablement).

---

## 📨 6. AI Email Support Assistant with Smart Fallback

**Purpose:**  
Reliable, accurate, scalable email support that adapts to query complexity.

**How it works:**  
- Reads incoming customer support emails  
- Primary model (Gemini) handles quick replies  
- Secondary model (GPT) handles complex requests or fallback scenarios  
- Logs all interactions into Google Sheets  

**Best for:**  
SaaS teams, customer support teams, and small businesses handling high email volumes.

---

## 🎤 7. Retell Voice AI — Calendar Checker + Vector-Based Call Intelligence

**Purpose:**  
A fully automated **voice agent** that can check availability, validate meeting details, confirm appointments, store structured insights, and write results to Google Sheets — all via natural phone conversations.

**How it works:**  
- Retell AI handles the call using natural, human-like voice  
- The voice agent checks Google Calendar availability in real-time  
- Uses Retell’s **vector database** to reference internal knowledge (scripts, policies, FAQs)  
- Collects caller information through an inbuilt “call form”  
- Once the caller confirms, data is automatically pushed to Google Sheets  
- Final outputs include:  
  - Caller details  
  - Meeting date/time  
  - Intent or request classification  
  - Any additional notes captured from the conversation  

**Why it stands out:**  
This workflow blends **LLM reasoning + voice interactions + structured data logging** into a single automated system. It works as a receptionist, scheduler, and data logger — all in one.

**Best for:**  
Service businesses, consultants, operations teams, or anyone needing automated call handling + scheduling + recordkeeping.

---

# 🔎 Executive Summary

The **n8n Automation Hub** provides teams with AI-powered systems that are:

- **Operationally impactful** — focused on real business use cases  
- **Accurate** — AI models handle parsing, summarization, reasoning  
- **Scalable** — works from small teams to full operations  
- **Modular** — every workflow is standalone yet extendable  
- **Compatible** — integrates with Google Workspace, Pinecone, Retell, and APIs you already use  
- **Fast to deploy** — JSON imports + API keys + minor config

These workflows modernize everyday processes and give teams the speed and reliability of much larger organizations.

---

# 🚀 Deployment Steps

1. Import the provided workflow JSONs into your n8n instance  
2. Add required API keys (Google, Gemini, OpenAI, Pinecone, Retell)  
3. Update folder IDs, calendar IDs, email addresses, and sheet links  
4. Run end-to-end tests with sample data  
5. Deploy and customize based on team requirements  

---
