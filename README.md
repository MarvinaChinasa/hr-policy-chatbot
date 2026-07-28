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

---

## 🏗️ Architecture & Pipeline Flow

```text
[ Custom Web UI ]
       │
       ▼ (HTTP POST / JSON Payload)
[ n8n Webhook Trigger ]
       │
       ▼
[ AI Agent Workflow Node ]
       ├────► [ Groq Chat Model (Llama 3.3 70B) ] ── (Synthesizes Answer)
       ├────► [ Simple Memory Window ] ──────────── (Preserves Chat Context via Session ID)
       └────► [ Pinecone Vector Store Tool ]
                     │
                     ▼
             [ Cohere Embeddings ] ────────────── (Semantic Retrieval / Namespace: hr-policies)
