<a id="readme-top"></a>

<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&height=220&section=header&text=RAG%20%E2%80%A2%20n8n&fontSize=52&fontColor=ffffff&animation=fadeIn&color=0:2563EB,100:60A5FA" width="100%" alt="RAG n8n banner" />

# RAG n8n

[![Typing SVG](https://readme-typing-svg.demolab.com/?font=Fira+Code\&weight=600\&size=28\&duration=3000\&pause=900\&color=2563EB\&center=true\&vCenter=true\&width=960\&height=60\&lines=Build+a+RAG+pipeline+with+n8n+%F0%9F%A4%96;Upload+documents.+Create+embeddings.+Ask+questions.+%F0%9F%93%9A;Powered+by+OpenAI+%2B+vector+retrieval+%E2%9A%A1)](https://github.com/)

A practical **Retrieval-Augmented Generation (RAG)** workflow built with **n8n** that lets you upload PDF or CSV files, index their contents into an in-memory vector store, and chat with an AI agent that retrieves relevant information before generating an answer.

<p>
  <img src="https://img.shields.io/badge/n8n-Workflow-FE6A16?style=for-the-badge&logo=n8n&logoColor=white" alt="n8n" />
  <img src="https://img.shields.io/badge/OpenAI-Embeddings%20%2B%20GPT--5%20mini-412991?style=for-the-badge&logo=openai&logoColor=white" alt="OpenAI" />
  <img src="https://img.shields.io/badge/RAG-Retrieval%20Augmented%20Generation-2563EB?style=for-the-badge" alt="RAG" />
  <img src="https://img.shields.io/badge/Vector%20Store-In%20Memory-0F172A?style=for-the-badge" alt="Vector Store" />
</p>

---
<div align="center">
  <img width="1859" height="829" alt="image" src="https://github.com/user-attachments/assets/e875dc78-ca57-4cd7-8327-485fda44ab38" alt="DevProject" width="900" />
</div>

## 📖 Table of Contents

* [About the Project](#-about-the-project)
* [How It Works](#-how-it-works)
* [Features](#-features)
* [Tech Stack](#-tech-stack)
* [Getting Started](#-getting-started)
* [Usage](#-usage)
* [License](#-license)
* [Contact](#-contact)

---

## 🧭 About the Project

**RAG n8n** is an n8n workflow for building a simple Retrieval-Augmented Generation pipeline without having to build the orchestration layer from scratch.

The workflow has two main paths:

**Document ingestion**

Upload a `.pdf` or `.csv` file through an n8n form, load the document, generate OpenAI embeddings, and insert the resulting vectors into an in-memory vector store.

**Question answering**

Send a message through the n8n chat trigger. The AI Agent can query the vector store as a retrieval tool, retrieve relevant knowledge, and generate a response using OpenAI's `gpt-5-mini` model.

A windowed memory component is also connected to the agent so recent conversation context can be maintained between messages.

This makes the template a useful starting point for document Q&A, knowledge assistants, RAG experiments, and n8n-based AI prototypes.

---

## 🔄 How It Works

```text
                    ┌──────────────────────┐
                    │   Upload PDF / CSV   │
                    └──────────┬───────────┘
                               │
                               ▼
                    ┌──────────────────────┐
                    │   Default Data       │
                    │       Loader         │
                    └──────────┬───────────┘
                               │
                               ▼
                    ┌──────────────────────┐
                    │   OpenAI Embeddings  │
                    └──────────┬───────────┘
                               │
                               ▼
                    ┌──────────────────────┐
                    │  Simple Vector Store │
                    │       (Insert)       │
                    └──────────────────────┘


User Message ──► Chat Trigger ──► AI Agent ──► GPT-5 mini
                                   │
                                   ├────────► Simple Memory
                                   │
                                   └────────► Vector Store Retriever
                                                  │
                                                  ▼
                                           Relevant Knowledge
```

The retrieval side of the workflow exposes the vector store to the AI Agent as a tool with the description:

```text
Use this knowledge base to answer questions from the user
```

This allows the agent to retrieve information from the uploaded knowledge base when answering questions.

---

## ✨ Features

|     | Feature                    | Description                                                             |
| :-: | -------------------------- | ----------------------------------------------------------------------- |
|  📤 | **Document Upload**        | Upload `.pdf` and `.csv` files through an n8n form trigger.             |
|  📚 | **Document Loading**       | Uses n8n's default binary data loader to process uploaded files.        |
|  🧠 | **OpenAI Embeddings**      | Converts document content into vector embeddings using OpenAI.          |
| 🗂️ | **In-Memory Vector Store** | Stores embeddings using n8n's Simple Vector Store.                      |
|  🔎 | **Vector Retrieval**       | Makes the vector store available to the AI Agent as a retrieval tool.   |
|  🤖 | **AI Agent**               | Combines retrieval, memory, and model generation in one agent workflow. |
|  💬 | **GPT-5 mini**             | Uses OpenAI's `gpt-5-mini` chat model for response generation.          |
|  🧾 | **Conversation Memory**    | Maintains recent conversational context using windowed memory.          |
|  🎨 | **Custom Upload UI**       | Includes a dark blue glassmorphism design for the uploader form.        |

---


## 🧰 Tech Stack

<div align="center">

<img src="https://img.shields.io/badge/n8n-FE6A16?style=for-the-badge&logo=n8n&logoColor=white" />
<img src="https://img.shields.io/badge/OpenAI-412991?style=for-the-badge&logo=openai&logoColor=white" />
<img src="https://img.shields.io/badge/LangChain-1C3C3C?style=for-the-badge&logo=langchain&logoColor=white" />
<img src="https://img.shields.io/badge/RAG-2563EB?style=for-the-badge" />
<img src="https://img.shields.io/badge/Vector%20Search-0F172A?style=for-the-badge" />
<img src="https://img.shields.io/badge/PDF%20%2B%20CSV-Supported-475569?style=for-the-badge" />

</div>

<p align="center">
<sub>n8n handles workflow orchestration, while OpenAI provides document embeddings and the chat model used by the AI Agent.</sub>
</p>

---



## ⚙️ Getting Started

### Prerequisites

* A running **n8n** instance
* An **OpenAI API key**
* An OpenAI credential configured in n8n
* A browser for accessing the n8n interfaces

### Installation

```bash
# Clone the repository
git clone https://github.com/kasrakr/RAG-n8n.git

# Enter the project
cd RAG-n8n
```

### Import the workflow

1. Open your n8n instance.
2. Select **Import from File**.
3. Choose `RAG n8n.json`.
4. Open the imported workflow.
5. Configure your OpenAI credentials.
6. Save the workflow.
7. Activate the workflow when ready.

> **Note:** The exported workflow references an OpenAI credential named `OpenAI account`. After importing the workflow, map this to your own n8n OpenAI credential.

---

## 🧭 Usage

### 1. Upload a document

Open the **uploader** form and upload one of the supported file types:

```text
.pdf
.csv
```

The document is loaded and sent to the OpenAI embedding node.

### 2. Store the embeddings

The generated vectors are inserted into the Simple Vector Store using:

```text
vector_store_key
```

### 3. Start a conversation

Use the **chat trigger** and ask a question related to the uploaded document.

### 4. Retrieve relevant information

The AI Agent can use the vector store as a retrieval tool and search the indexed knowledge base for relevant information.

### 5. Generate the answer

The retrieved context is combined with the conversation and passed to the OpenAI chat model:

```text
gpt-5-mini
```

### 6. Continue the conversation

The **Simple Memory** node maintains recent context so follow-up questions can remain connected to the conversation.

---





## 📄 License

Distributed under the **MIT License**. See [`LICENSE`](./LICENSE) for details.

---

## 📬 Contact

**Kasra Karimian**

<div align="center">

<a href="https://github.com/kasrakr">
  <img src="https://img.shields.io/badge/GitHub-181717?style=for-the-badge&logo=github&logoColor=white" />
</a>

<a href="https://linkedin.com/in/kasrakarimian">
  <img src="https://img.shields.io/badge/LinkedIn-A855F7?style=for-the-badge&logo=linkedin&logoColor=white&labelColor=1E1B4B" alt="LinkedIn" />
</a>

<a href="https://t.me/lowkasra">
  <img src="https://img.shields.io/badge/Telegram-8B5CF6?style=for-the-badge&logo=telegram&logoColor=white&labelColor=1E1B4B" alt="Telegram" />
</a>

<a href="mailto:kasrakarimaian84@gmail.com">
  <img src="https://img.shields.io/badge/Email-6D28D9?style=for-the-badge&logo=gmail&logoColor=white&labelColor=1E1B4B" alt="Email" />
</a>

</div>

---

<img src="https://capsule-render.vercel.app/api?type=waving&height=160&color=0:60A5FA,100:1D4ED8&section=footer&animation=fadeIn" width="100%"/>
