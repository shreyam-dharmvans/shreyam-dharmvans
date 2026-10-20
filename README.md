<div align="center">

# Hi there, I'm Shreyam Dharmvans 👋

### **Backend Engineer &bull; GenAI & Big Data Systems**

I build scalable backend systems, AI agent workflows, and data processing pipelines.

<p align="center">
  <a href="mailto:sdharmvans@gmail.com"><img src="https://img.shields.io/badge/Email-sdharmvans%40gmail.com-EA4335?style=flat-square&logo=gmail&logoColor=white" alt="Email" /></a>
  <a href="https://www.linkedin.com/in/shreyam-dharmvans-222b00317"><img src="https://img.shields.io/badge/LinkedIn-shreyam--dharmvans-0A66C2?style=flat-square&logo=linkedin&logoColor=white" alt="LinkedIn" /></a>
  <a href="https://github.com/shreyam-dharmvans"><img src="https://img.shields.io/badge/GitHub-shreyam--dharmvans-181717?style=flat-square&logo=github&logoColor=white" alt="GitHub" /></a>
  <a href="https://leetcode.com/u/shreyam-dharmvans/"><img src="https://img.shields.io/badge/LeetCode-Profile-FFA116?style=flat-square&logo=leetcode&logoColor=white" alt="LeetCode" /></a>
</p>

---

</div>

## 👨‍💻 About Me

I am a Software Engineer currently working at **Nagarro**, with a strong focus on **Backend Development**, **Generative AI applications**, and **Big Data pipelines**:

- ⚙️ **Backend Engineering**: Writing clean, performant APIs in Node.js, Express, and FastAPI, optimizing database queries, and setting up caching layers with Redis.
- 🤖 **GenAI & Agent Workflows**: Building stateful AI workflows using **LangGraph** and connecting AI coding assistants to live runtime context via the **Model Context Protocol (MCP)**.
- 📊 **Big Data & Cloud Data**: Designing data pipelines using **PySpark**, **Azure Databricks**, **Azure Data Factory**, and the **Medallion Architecture (Delta Lake)**.

---

## 🚀 Projects in Detail

### ⚡ 1. EasyMetrics — Real-Time API Performance Monitor & AI SRE Agent

> 🌐 **Live Platform:** [easy-metrics.centralindia.cloudapp.azure.com](https://easy-metrics.centralindia.cloudapp.azure.com)  
> 📦 **NPM Package:** [`@easy-metrics/node`](https://www.npmjs.com/package/@easy-metrics/node)  
> 💻 **GitHub Repository:** [github.com/shreyam-dharmvans/easy-metrics](https://github.com/shreyam-dharmvans/easy-metrics)  
> 🛠️ **Technologies Used:** `Node.js`, `TypeScript`, `Next.js`, `Express`, `Python (FastAPI)`, `LangGraph`, `FastMCP`, `PostgreSQL`, `Prisma`, `Docker`, `Azure VM`

#### 🛑 The Problem it Solves:
When a backend API endpoint is slow (for example, a checkout API taking 3 seconds), it is made up of many internal steps: auth checks, complex database queries with multiple JOINs, third-party payment calls (like Stripe), and database updates. 

Terminal logs typically only show:
```text
POST /api/orders/checkout - 200 OK (3,120ms)
```
Developers cannot tell from the outside *which exact step* caused the delay. Even worse, when developers ask AI assistants like Cursor or Claude *"Why is this route slow?"*, the AI cannot see what happened at runtime and is forced to guess, often suggesting pointless code tweaks or telling developers to litter their code with temporary `console.time()` statements.

#### 💡 How EasyMetrics Works:
1. **Zero-Code Setup via NPM Package (`@easy-metrics/node`)**:
   - Developers install the package and run their server with one flag:
     ```bash
     node --import @easy-metrics/node/register app.js
     ```
   - It automatically hooks into Express routes, database queries, and external HTTP calls **without changing a single line of business code**.
   - Spans are recorded in-memory in under $0.05\text{ms}$ and sent asynchronously in background batches every 2 seconds, meaning the host application never experiences slowdowns or crashes.

2. **Visual Request Waterfall Timeline**:
   - The Next.js dashboard visualizes the entire execution lifecycle for every single request. Developers can click on any slow request and immediately spot the culprit:
     ```text
     POST /api/orders/checkout (Total: 2,840ms)
     ├── 1. Auth Middleware ............................ [12ms]   ✅
     ├── 2. SELECT * FROM orders JOIN items ... ........ [2,480ms] ❌ (Bottleneck: Missing Index)
     ├── 3. POST https://api.stripe.com/v1/charges ..... [310ms]  ✅
     └── 4. UPDATE orders SET status = 'paid' .......... [38ms]   ✅
     ```

3. **Connecting AI Coding Tools via Model Context Protocol (MCP)**:
   - EasyMetrics includes a **FastMCP server** supporting both **Streamable HTTP** and **Server-Sent Events (SSE)**.
   - Developers can connect Cursor, Claude Desktop, or Antigravity directly to their EasyMetrics instance.
   - When an endpoint is slow, the AI reads live runtime data through the MCP tools and provides verified, accurate fixes (such as writing the exact missing database index).

4. **Autonomous AI SRE Copilot (LangGraph + FastAPI)**:
   - Built a Python backend service using **FastAPI** and **LangGraph** to act as an automated reliability assistant.
   - Features persistent state checkpointing in PostgreSQL (`AsyncPostgresSaver`), enabling multi-turn diagnostic conversations that persist across browser reloads.
   - Includes automatic tool self-healing (if a custom SQL query has a typo, it reads the error and corrects itself) and token budgeting to stay within strict API limits.

5. **Deployment & DevOps**:
   - Entire full-stack system is containerized with **Docker Compose** and runs on an **Azure Virtual Machine** with custom SSL and health checks.

---

### 🗺️ 2. LearnPro — AI-Powered Learning Roadmap Platform

> 🌐 **Live Demo:** [learning-roadmap-pi.vercel.app](https://learning-roadmap-pi.vercel.app)  
> 💻 **GitHub Repository:** [github.com/shreyam-dharmvans/learnpro](https://github.com/shreyam-dharmvans/learnpro)  
> 🛠️ **Technologies Used:** `Next.js 15`, `TypeScript`, `Gemini 2.5 Flash`, `MongoDB`, `Async Queues`, `NextAuth`, `Tailwind CSS`

#### 🛑 The Problem it Solves:
People wanting to learn new technical topics often get overwhelmed by disorganized internet tutorials or generic wall-of-text responses from AI chats. Moreover, generating personalized curriculum on the fly often leads to slow page loads and blocking operations if emails/notifications run on the same server thread.

#### 💡 How LearnPro Works:
1. **Dynamic Roadmap Synthesis**:
   - Uses **Gemini 2.5 Flash** with strict structured JSON schema generation to dynamically build tailored, step-by-step learning milestones based on user skill level and goals.
   - Streams curriculum elements to the frontend for fast, sub-second perceived load times.

2. **Decoupled Asynchronous Background Queues**:
   - To send daily learning reminder emails and progress summaries to users, the application decouples background tasks from user requests using an **asynchronous producer-worker queue**.
   - This ensures scheduled email generation never slows down or blocks user interactions on the web app.

3. **Secure Auth & Clean Data Store**:
   - Features Google OAuth integration using **NextAuth** for one-click onboarding.
   - Stores user roadmap milestones, active progress, and preferences reliably in **MongoDB**.

---

### 🧱 3. Big Data Pipelines & Medallion Architecture

> 🛠️ **Technologies Used:** `PySpark`, `Azure Databricks`, `Azure Data Factory (ADF)`, `ADLS Gen 2`, `Delta Lake`, `MS SQL`

#### 🛑 The Challenge:
In enterprise environments, raw data (such as IoT telemetry, logs, and transaction streams) arrives continuously in high volumes and mixed formats (JSON, CSV, semi-structured). Storing raw data directly in application databases leads to query timeouts, high storage costs, and corrupt records.

#### 💡 How the Medallion Architecture Solves This:
I design and implement data pipelines following the **Medallion Lakehouse pattern** on Azure:

```text
[ Raw Data Sources: IoT / Logs / DBs ]
                 │
                 ▼ (Azure Data Factory Ingestion)
┌────────────────────────────────────────────────────────┐
│  BRONZE LAYER (Azure Data Lake Gen 2)                  │
│  • Raw, unparsed data stored as-is in Delta format      │
│  • Preserves raw history with zero data loss           │
└────────────────────────────────────────────────────────┘
                 │
                 ▼ (PySpark Cleaning & Validation)
┌────────────────────────────────────────────────────────┐
│  SILVER LAYER (Validated & Enriched)                   │
│  • Schema enforcement, deduplication, null filtering   │
│  • ACID transactions powered by Delta Lake             │
└────────────────────────────────────────────────────────┘
                 │
                 ▼ (PySpark Aggregations & Business Logic)
┌────────────────────────────────────────────────────────┐
│  GOLD LAYER (Curated Business Marts)                   │
│  • Aggregated tables, clean KPIs, optimized for SQL    │
│  • Ready for analytics, reporting, and backend queries │
└────────────────────────────────────────────────────────┘
```

- **Azure Data Factory (ADF)**: Configured automated ingestion workflows with dynamic parameters and event-based triggers to move incoming data into ADLS Gen 2.
- **PySpark Transformations**: Wrote batch and streaming transformations in **Azure Databricks**, handling schema evolution, watermarking, and windowed aggregations.
- **Delta Lake**: Implemented Delta Lake on top of ADLS Gen 2 to enable ACID transactions, time travel, and unified batch and streaming data processing.

---

## 🛠️ Technical Skills

<table>
  <tr>
    <td width="24%"><b>Backend Engineering</b></td>
    <td>
      <img src="https://img.shields.io/badge/Node.js-339933?style=flat-square&logo=node.js&logoColor=white" />
      <img src="https://img.shields.io/badge/Express.js-000000?style=flat-square&logo=express&logoColor=white" />
      <img src="https://img.shields.io/badge/Next.js-000000?style=flat-square&logo=next.js&logoColor=white" />
      <img src="https://img.shields.io/badge/FastAPI-009688?style=flat-square&logo=fastapi&logoColor=white" />
      <img src="https://img.shields.io/badge/REST_APIs-02569B?style=flat-square" />
    </td>
  </tr>
  <tr>
    <td><b>Languages</b></td>
    <td>
      <img src="https://img.shields.io/badge/TypeScript-3178C6?style=flat-square&logo=typescript&logoColor=white" />
      <img src="https://img.shields.io/badge/JavaScript-F7DF1E?style=flat-square&logo=javascript&logoColor=black" />
      <img src="https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white" />
      <img src="https://img.shields.io/badge/Java-ED8B00?style=flat-square&logo=openjdk&logoColor=white" />
      <img src="https://img.shields.io/badge/SQL-4479A1?style=flat-square&logo=postgresql&logoColor=white" />
    </td>
  </tr>
  <tr>
    <td><b>GenAI & Agents</b></td>
    <td>
      <img src="https://img.shields.io/badge/Model_Context_Protocol_(MCP)-8A2BE2?style=flat-square" />
      <img src="https://img.shields.io/badge/LangGraph-1C3C3C?style=flat-square" />
      <img src="https://img.shields.io/badge/LangChain-121212?style=flat-square&logo=chainlink&logoColor=white" />
      <img src="https://img.shields.io/badge/RAG_Workflows-4B0082?style=flat-square" />
    </td>
  </tr>
  <tr>
    <td><b>Big Data & Cloud Data</b></td>
    <td>
      <img src="https://img.shields.io/badge/PySpark-E25A1C?style=flat-square&logo=apachespark&logoColor=white" />
      <img src="https://img.shields.io/badge/Azure_Databricks-FF3621?style=flat-square&logo=databricks&logoColor=white" />
      <img src="https://img.shields.io/badge/Azure_Data_Factory-0078D4?style=flat-square&logo=microsoftazure&logoColor=white" />
      <img src="https://img.shields.io/badge/ADLS_Gen_2-0089D6?style=flat-square&logo=microsoftazure&logoColor=white" />
      <img src="https://img.shields.io/badge/Delta_Lake-00ADD8?style=flat-square" />
    </td>
  </tr>
  <tr>
    <td><b>Databases & Caching</b></td>
    <td>
      <img src="https://img.shields.io/badge/PostgreSQL-4169E1?style=flat-square&logo=postgresql&logoColor=white" />
      <img src="https://img.shields.io/badge/Redis-DC382D?style=flat-square&logo=redis&logoColor=white" />
      <img src="https://img.shields.io/badge/MongoDB-47A248?style=flat-square&logo=mongodb&logoColor=white" />
      <img src="https://img.shields.io/badge/Prisma_ORM-2D3748?style=flat-square&logo=prisma&logoColor=white" />
      <img src="https://img.shields.io/badge/MS_SQL-CC292B?style=flat-square&logo=microsoftsqlserver&logoColor=white" />
    </td>
  </tr>
  <tr>
    <td><b>Cloud & Tools</b></td>
    <td>
      <img src="https://img.shields.io/badge/Docker-2496ED?style=flat-square&logo=docker&logoColor=white" />
      <img src="https://img.shields.io/badge/Microsoft_Azure-0078D4?style=flat-square&logo=microsoftazure&logoColor=white" />
      <img src="https://img.shields.io/badge/AWS-232F3E?style=flat-square&logo=amazonwebservices&logoColor=white" />
      <img src="https://img.shields.io/badge/GitHub_Actions-2088FF?style=flat-square&logo=github-actions&logoColor=white" />
      <img src="https://img.shields.io/badge/Git-F05032?style=flat-square&logo=git&logoColor=white" />
    </td>
  </tr>
</table>

---

## 📬 Contact & Links

- 💼 **LinkedIn**: [linkedin.com/in/shreyam-dharmvans-222b00317](https://www.linkedin.com/in/shreyam-dharmvans-222b00317)
- 📧 **Email**: [sdharmvans@gmail.com](mailto:sdharmvans@gmail.com)
- 💻 **GitHub**: [github.com/shreyam-dharmvans](https://github.com/shreyam-dharmvans)
- 🧩 **LeetCode**: [leetcode.com/u/shreyam-dharmvans/](https://leetcode.com/u/shreyam-dharmvans/)
