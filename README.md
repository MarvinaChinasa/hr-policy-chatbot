# 🤖 HR Policy Intelligence Chatbot

> An enterprise-grade, zero-hallucination **Retrieval-Augmented Generation (RAG)** chatbot built to deliver instant, verifiable answers to employee workplace policy questions.

![License](https://img.shields.io/badge/License-MIT-blue.svg)
![Python](https://img.shields.io/badge/Python-3.10%2B-green)
![n8n](https://img.shields.io/badge/Orchestration-n8n-FF6D5A)
![VectorDB](https://img.shields.io/badge/VectorDB-Pinecone-000000)
![LLM](https://img.shields.io/badge/LLM-Groq%20%2F%20Llama%203.3%2070B-orange)

---

## 📌 Executive Summary

Navigating dense corporate policy handbooks (often spanning hundreds of pages) creates significant friction for employees and operational overhead for HR teams. The **HR Policy Intelligence Assistant** solves this by combining semantic vector search with an agentic orchestration workflow.

Employees ask questions in plain English through a responsive web interface, and the system retrieves precise policy clauses from vectorized company documentation before synthesizing an answer—complete with source citations.

## 🏗️ Architecture & Pipeline Flow

```text
[ Custom Web UI ]
       │
       ▼ (HTTP POST / JSON Payload)
[ n8n Webhook Trigger ]
       │
       ▼
[ AI Agent Workflow Node ]
       ├────► [ Primary LLM: Groq / Llama 3.3 70B ] ── (Sub-second Primary Inference)
       │           │
       │           └─► (Failover Route) ──► [ Fallback LLM: OpenAI gpt-4.1-mini ]
       │
       ├────► [ Simple Memory Window ] ──────────── (Preserves Chat Context via Session ID)
       │
       └────► [ Pinecone Vector Store Tool ]
                     │
                     ▼
             [ Cohere Embeddings ] ────────────── (Semantic Retrieval / Namespace: hr-policies)

---

### Key Workflow Highlights

* **Zero-Hallucination Guardrails:** Strict prompt instructions enforce that answers must originate *only* from ingested HR policy documents.
* **Session Management:** Tracks conversation history using dynamic `sessionId` payloads.
* **Semantic Retrieval:** Embeds policy documents via Cohere (`embed-english-v3.0`) into Pinecone vector namespaces.
* **High-Speed Inference & High-Availability Fallback:** Primary execution uses Groq processing (llama-3.3-70b-versatile) for sub-second responses, backed by an automated fallback route to OpenAI (gpt-4.1-mini) to guarantee zero-downtime execution during high traffic or rate-limiting events.

---

## 🚀 Tech Stack

* **Frontend:** HTML5, Tailwind CSS (Custom Emerald & Orange Theme), Lucide Icons, JavaScript (Fetch API)
* **Orchestration:** n8n Agentic Workflow
* **Vector Store & Retrieval:** Pinecone Vector DB
* **Embeddings Model:** Cohere (`embed-english-v3.0`)
* **Language Model (LLM):** Groq / Meta Llama 3.3 70B Versatile
* **FallBack Language Model:** Opeai / gpt-4.1-mini
* **Memory:** n8n Buffer Window Memory (Custom Session Key)

---

## 📂 Repository Structure

.
├── index.html                      # Responsive web application UI
├── hr_policy_chatbot_workflow.json  # Complete n8n agentic workflow export
├── docs/                           # Policy documentation samples
└── README.md                       # System documentation


---

## ⚙️ Local Setup & Deployment

### 1. Import n8n Workflow
1. Open your n8n instance canvas.
2. Click **Menu (`...`)** $\rightarrow$ **Import from File**.
3. Select `hr_policy_chatbot_workflow.json`.
4. Configure your API Credentials for **Groq**, **Pinecone**, and **Cohere**.

### 2. Configure Vector Index
* Index Name: `hr-policy-chatbot`
* Vector Namespace: `hr-policies`
* Embedding Dimensions: 1024 (Cohere `embed-english-v3.0`)

### 3. Launch Web Interface
1. Set your n8n Webhook node to **Active** and copy the **Production URL**.
2. Open `index.html` in your browser.
3. Click the **Webhook Endpoint** settings icon in the top header and paste your Production Webhook URL.

---

## 👥 Project Team & Acknowledgments

This project was developed as a capstone intelligence system under the **Generative AI Track (Cohort 3)**.

* **Marvina Chinasa Awunor** – *System Architecture, n8n Workflow Orchestration, Frontend Development*
* **Abubakar Abba Usman** – *Vector DB Indexing, Pinecone Namespace Management, Embedding Pipeline*
* **Daniel Ayuba Tishawa** – *Prompt Engineering, Knowledge Base Curation, System Testing & Evaluation*

---

## 📄 License
Distributed under the MIT License.

---

## 🏗️ Architecture & Pipeline Flow
