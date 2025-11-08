# 🩺 MediChatBot RAG
**AI-powered Medical & First-Aid Assistant built with n8n and Retrieval-Augmented Generation (RAG)**  

MediChatBot RAG provides instant, reliable answers to medical and first-aid questions by retrieving information from a Google Drive knowledge base.  
It combines **semantic search**, **vector embeddings**, and **conversational AI** to deliver context-aware, source-cited responses.

---

![MediChatBot](https://github.com/user-attachments/assets/e34cb7cb-e884-4822-8f71-20c47f0b916a)


## 🌐 Overview
This project demonstrates a **production-grade conversational healthcare assistant** using RAG architecture.  
It automatically ingests documents from Google Drive, processes them with Cohere embeddings, stores them in a Supabase vector database, and responds to user queries via webhook connections using Google Gemini.

Ideal for:
- Clinics or hospitals offering 24/7 AI-assisted support  
- Medical educators building interactive learning bots  
- NGOs providing first-aid information access  

---

## ✨ Key Features
- **Automated Knowledge Indexing** – Monitors a Google Drive folder for new/updated medical documents  
- **Intelligent Semantic Search** – Uses Cohere embeddings for context retrieval  
- **Conversational Memory** – Maintains dialogue continuity using buffer memory  
- **AI-Generated Responses** – Uses Google Gemini (PaLM) for human-like answers  
- **Source Attribution** – Includes document references in replies  
- **Real-Time Re-Indexing** – Updates automatically when Drive files change  

---

## 🧱 Architecture
Google Drive (Medical Knowledge Base)
↓
n8n Triggers (File Created/Updated)
↓
File Download + Conversion (PDF)
↓
Cohere Embeddings → Supabase Vector Store
↓
Webhook → AI Agent → Gemini Model
↓
Contextual Response + Source Citation


---

## 🧩 Workflow Visualization

### Document Ingestion Pipeline
1. Google Drive Trigger detects file upload or update  
2. File is downloaded and converted to PDF  
3. Cohere embeddings are generated  
4. Embeddings and metadata stored in Supabase  
5. Old entries deleted for clean indexing  

### Query Response Pipeline
1. User sends question to Webhook  
2. Agent retrieves top-K chunks from Supabase  
3. Gemini model generates a contextual reply  
4. Response returned to Webhook with citations  

---

## 🧠 Technology Stack
| Component | Role |
|------------|------|
| **n8n** | Workflow automation & orchestration |
| **Google Drive** | Document repository |
| **Supabase (pgvector)** | Vector database |
| **Cohere API** | Text embeddings (`embed-english-v3.0`) |
| **Google Gemini (PaLM)** | Chat language model |
| **Webhook** | Query endpoint |
| **LangChain (n8n nodes)** | RAG pipeline components |

---

## 💼 Use Cases
- 🏥 Hospital FAQ chatbot for patients and staff  
- 📚 Medical education assistant  
- 🩹 First-aid and emergency guidance bot  
- 💬 Integrate into web or mobile apps for quick health info  

---

## 🔧 Prerequisites
| Service | Access Needed |
|----------|---------------|
| **n8n** | Cloud or self-hosted v1.0+ |
| **Google Drive** | Folder for knowledge docs |
| **Supabase** | pgvector-enabled project |
| **Cohere API** | Embeddings key |
| **Google Gemini API** | Chat model key |
| **Webhook URL** | User query input |

---

## ⚙️ Quick Start (Setup Time ≈ 30 min)
1. **Import Workflow**  
   - In n8n: *Import from File → `MediChatBot RAG.json`*
2. **Set Credentials**  
   - Google Drive OAuth2 API  
   - Supabase API Key  
   - Cohere API Key  
   - Google Gemini (PaLM) API Key  
3. **Create Drive Folder** and share with your Service Account  
4. **Upload** sample PDF/DOCX medical files  
5. **Activate** the workflow and watch for automatic indexing  
6. **Send Test Query** to the Webhook URL  

---

## 🗂️ Project Structure
medichatbot-rag/
├── MediChatBot RAG.json
├── docs/
│ ├── SETUP.md
│ └── TROUBLESHOOTING.md
├── .env.example
└── README.md

📘 Setup Guide (Summary)
1️⃣ Import Workflow

File: MediChatBot RAG.json

Key nodes: Drive Trigger, Cohere Embeddings, Supabase Store, Gemini Chat, Webhook.

2️⃣ Configure Credentials
Service	            How to Connect
Google Drive	      OAuth2 API → Grant access to folder
Supabase	            Use project URL + service key
Cohere	            API Key from dashboard.cohere.com

Google Gemini	      Enable PaLM API on GCP → get key


| Metric             | Typical Value    |
| ------------------ | ---------------- |
| Response time      | 2 – 5 s          |
| Documents tested   | 400 +            |
| Retrieval accuracy | ≈ 88 % (Top-5)   |
| Estimated cost     | $10 – 30 / month |

| Parameter                | Description                             | Default    |
| ------------------------ | --------------------------------------- | ---------- |
| **Top K**                | Number of chunks retrieved              | 15         |
| **Chunk Size**           | Split size for embeddings               | 1000 chars |
| **Similarity Threshold** | Minimum match score                     | 0.7        |
| **Prompt**               | Update in AI Agent node for tone/domain | –          |


| Issue                     | Cause                      | Solution                                  |
| ------------------------- | -------------------------- | ----------------------------------------- |
| Workflow does not trigger | Wrong Drive folder ID      | Check folder and service account          |
| No embeddings stored      | Supabase key invalid       | Verify API credentials                    |
| Poor answers              | Few docs or low similarity | Increase Top K / update embeddings        |
| Webhook not responding    | Workflow inactive          | Set workflow to **Active**                |
| Slow response             | Large docs or API latency  | Increase chunk size / optimize embeddings |


🛡️ Security Notes

- Credentials managed inside n8n Credential Manager
- Never commit .env or .n8n files
- Rotate API keys every 90 days
- For demo use only — don’t upload personal health data

🤝 Contributing

- We welcome community enhancements!
- Open issues for bugs or ideas
- Submit pull requests for workflow improvements
- Share custom integrations (WhatsApp, Slack, etc.)


🔗 Resources

- n8n Docs
- Supabase Docs
- Cohere API Docs
- Google Gemini API




