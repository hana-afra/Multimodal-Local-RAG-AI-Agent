# 🤖 Multimodal Local AI Agent RAG System

**Production-Ready RAG System** - A comprehensive, self-hosted AI document assistant with advanced features including multi-modal document processing, intelligent reranking, query analytics, and automated error monitoring.

> **Note:** Built on top of [n8n-io/self-hosted-ai-starter-kit](https://github.com/n8n-io/self-hosted-ai-starter-kit)

---

## 🌟 Key Features

### 📚 **Intelligent Document Processing**
- **Multi-format Support**: PDF, DOCX, images with text extraction
- **Docling Integration**: Advanced PDF parsing with layout preservation
- **Automatic Metadata Extraction**: File name, type, size, department, upload date
- **Image Extraction**: Automatically extracts and serves images from documents
- **Department Filtering**: Organize and filter documents by department (Finance, HR, etc.)

### 🔍 **Advanced RAG Capabilities**
- **Vector Search**: Qdrant vector database for semantic search
- **AI Reranking**: Cohere reranker for improved result relevance
- **Confidence Scores**: Shows relevance percentage for each source
- **Source Citations**: Every answer includes clickable PDF links with metadata
- **Context-Aware Responses**: AI provides answers with full document context

### 📊 **Query Analytics Dashboard**
- **Real-time Metrics**: Total queries, average response time
- **Usage Patterns**: Most asked questions and most referenced documents
- **Recent Activity**: Last 10 queries with timestamps
- **Google Sheets Integration**: All data logged for deep analysis
- **Visual Dashboard**: Clean web interface for instant insights

### 🚨 **Error Monitoring & Alerting**
- **Automated Error Logging**: All workflow errors logged to Google Sheets
- **Email Notifications**: Instant alerts sent to admin email
- **Detailed Error Context**: Workflow name, node, timestamp, error message
- **Centralized Tracking**: Single spreadsheet for all system errors

### 🔐 **Enterprise-Ready Features**
- **Local Hosting**: All data stays on your infrastructure
- **No External API Costs**: Uses local Ollama models
- **Department Access Control**: Filter documents by department
- **Document Versioning**: Tracks upload dates and file metadata
- **Professional UI**: Clean, modern interface for end users

---

## 🏗️ **System Architecture**

```
┌─────────────────────────────────────────────────────────┐
│                    USER INTERFACE                        │
│  - Chat Interface                                        │
│  - Analytics Dashboard                                   │
│  - Document Viewer                                       │
└─────────────────┬───────────────────────────────────────┘
                  │
┌─────────────────▼───────────────────────────────────────┐
│              RAG WORKFLOW ENGINE                         │
│  ┌──────────────────────────────────────────────────┐  │
│  │ 1. Document Ingestion                            │  │
│  │    - Docling Processing                          │  │
│  │    - Metadata Extraction                         │  │
│  │    - Image Extraction                            │  │
│  │    - PDF File Serving                            │  │
│  └──────────────────────────────────────────────────┘  │
│  ┌──────────────────────────────────────────────────┐  │
│  │ 2. Vector Storage                                │  │
│  │    - Qdrant Vector DB                            │  │
│  │    - Embeddings (Ollama)                         │  │
│  │    - Metadata Storage                            │  │
│  └──────────────────────────────────────────────────┘  │
│  ┌──────────────────────────────────────────────────┐  │
│  │ 3. Query Processing                              │  │
│  │    - Vector Search                               │  │
│  │    - AI Reranking (Cohere)                       │  │
│  │    - Department Filtering                        │  │
│  └──────────────────────────────────────────────────┘  │
│  ┌──────────────────────────────────────────────────┐  │
│  │ 4. Response Generation                           │  │
│  │    - AI Agent (Ollama)                           │  │
│  │    - Source Citations                            │  │
│  │    - Confidence Scores                           │  │
│  └──────────────────────────────────────────────────┘  │
│  ┌──────────────────────────────────────────────────┐  │
│  │ 5. Analytics & Monitoring                        │  │
│  │    - Query Logging                               │  │
│  │    - Error Tracking                              │  │
│  │    - Email Alerts                                │  │
│  └──────────────────────────────────────────────────┘  │
└─────────────────────────────────────────────────────────┘
```

---

## 🚀 **Installation**

### **1. Clone Repository**
```bash
git clone https://github.com/hana-afra/Multimodal-Local-AI-Agent-RAG.git
cd Multimodal-Local-AI-Agent-RAG
cp .env.example .env
```

### **2. Configure Environment**
Edit `.env` file with your credentials:
```bash
# Update these values
COHERE_API_KEY=your_cohere_key
GOOGLE_SHEETS_CREDENTIALS=your_credentials
ADMIN_EMAIL=your-email@example.com
```

### **3. Start Services**
```bash
docker compose --profile cpu up -d
```

### **4. Access n8n**
- Open http://localhost:5678
- Complete initial setup
- Import workflows from `/workflows` folder

---

## 📖 **Usage Guide**

### **🔹 Uploading Documents**

1. Place PDF files in: `/data/shared/rag-files/pending/[department_name]/`
2. System automatically:
   - Processes with Docling
   - Extracts metadata and images
   - Moves PDFs to accessible folder
   - Indexes in Qdrant vector database
   - Logs to tracking system

**Supported Departments:**
- `finance_departement` - Finance documents
- Other folders automatically marked as "unknown"

---

### **🔹 Querying the System**

**Web Interface:**
- Navigate to chat interface: http://localhost:5678/workflow/[your-workflow-id]
- Ask questions in natural language
- Receive answers with:
  - Clickable PDF source links
  - Confidence scores (0-100%)
  - Document metadata

**Example Query:**
```
"What are the expense reimbursement policies?"
```

**Example Response:**
```
Expense reimbursement requires:
- Receipts for all purchases over $50
- Manager approval within 30 days
- Submission via finance portal



### **🔹 Analytics Dashboard**

**Access:** http://localhost:5678/webhook/analytics-dashboard

**Features:**
- Total queries processed
- Average response time
- Top 5 most asked questions
- Most referenced documents
- Recent query history
- Direct link to Google Sheet for detailed analysis

---

### **🔹 Error Monitoring**

**Automatic Logging:**
- All workflow errors logged to Google Sheets
- Email alerts sent to admin
- Includes: timestamp, workflow name, node, error message

**Access Error Logs:**
- [Your Google Sheet URL from Alert_Errors.json]

---



## 📊 **Workflows Included**

1. **ENHANCED_RAG** - Main chat interface with full RAG capabilities
2. **Query_Analytics_Dashboard** - Real-time analytics and metrics
3. **Alert_Errors** - Automated error monitoring and alerting

---

## 🔐 **Security & Privacy**

- ✅ **100% Local Processing** - No data sent to external APIs (except Cohere reranking)
- ✅ **No Data Storage** by LLM providers
- ✅ **Department-level Access Control**
- ✅ **Audit Trail** via query analytics
- ✅ **Error Monitoring** for system security


**🚀 Ready to revolutionize your document Q&A system? Get started now!**