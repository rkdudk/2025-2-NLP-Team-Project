# 2025-2 Artificial Intelligence Term Project: Hybrid RAG System

> **Team 10** | Ewha Womans University  
> **Topic:** Improving Benchmark Performance on `Ewha.pdf` & `MMLU-Pro` using Hybrid RAG

## 📌 Project Overview
[cite_start]This project aims to enhance Large Language Model (LLM) performance on specific domains without fine-tuning. [cite_start]We implemented a **Hybrid RAG System** that dynamically routes queries to specialized pipelines based on the input language, utilizing the **Upstage Solar-Pro API**[cite: 846, 896].

### 🎯 Objectives
* [cite_start]**No Fine-tuning:** Achieve high accuracy using only RAG and Prompt Engineering techniques.
* **Dual Domain Handling:**
    1.  [cite_start]**Korean:** Q&A based on *Ewha Womans University Regulations* (`Ewha.pdf`)[cite: 913].
    2.  [cite_start]**English:** Expert-level QA on *MMLU-Pro* (Law, Psychology, Business, Philosophy, History)[cite: 914].

---

## 👥 Team Members (Team 10)
| ID | Name | Role |
| :--- | :--- | :--- |
| **2171015** | **Park Sunwoo** | Pipeline Architecture, Ewha.pdf Retrieval Strategy |
| **2277002** | **Kim Gayoung** | MMLU-Pro Strategy, Prompt Engineering |
| **2277027** | **Lim Seoyen** | System Implementation, Optimization & Evaluation |

---

## 🏗️ System Architecture

Our system acts as a language-based router that directs questions to the most effective solver pipeline.

### 1. Language Router
* [cite_start]**Input:** Question from `testset.csv`[cite: 912].
* **Logic:** Detects Korean characters to classify the query source.
    * **Korean Detected:** Routes to **Ewha Regulation Pipeline**.
    * **English Detected:** Routes to **MMLU-Pro Pipeline**.

### 2. Ewha Regulation Pipeline (Korean)
Optimized for precise retrieval of university bylaws.
* **Data Processing:** * Converted PDF to **Markdown** to preserve `Chapter` > `Article` hierarchy.
    * Used **Camelot** (Lattice/Stream mode) for accurate **Table Extraction**.
* **Retrieval Strategy:** **Ensemble Retriever** combining:
    * **Parent Document Retriever:** Fetches larger context (Chapters).
    * **Dense Retriever:** Fetches specific details (Articles).
* **Inference:** **One-shot Prompting** with **Majority Voting** (5 iterations).

### 3. MMLU-Pro Pipeline (English)
[cite_start]Designed for high-reasoning tasks in 5 specialized domains[cite: 914].
* **External Knowledge:** * **OpenStax Textbooks:** Domain-specific knowledge base.
    * [cite_start]**Wikipedia:** Used the designated `Wikipedia-API` library for real-time fact-checking[cite: 981].
* **Strategy:** **Category-Specific Prompting**.
    1.  **Classification:** Identifies the domain (e.g., Law, History) and extracts 3 search keywords.
    2.  **Solver:** Applies domain-specific reasoning rules (e.g., legal doctrine application) to derive the answer.

---

## 📊 Performance

| Dataset | Strategy | Accuracy |
| :--- | :--- | :--- |
| **Ewha.pdf** | One-shot + Ensemble Retriever | **96.0%** |
| **MMLU-Pro** | Category-Specific Prompt | **80.0%** |
| **Overall** | Hybrid Routing Strategy | **~88%** |

---

## 🚀 How to Run

### 1. Prerequisites
* **Python 3.8+**
* [cite_start]**Upstage API Key** (Required for `solar-pro2` model)[cite: 896].
* **Dependencies:** Install required packages using the command below.
    ```bash
    pip install -r requirements.txt
    ```
    [cite_start]*(Note: `requirements.txt` includes `openai`, `langchain`, `wikipedia-api`, `faiss-cpu`, etc.)* [cite: 926, 982]

### 2. Execution
Run the main script to process the test set and generate the result file.
```bash
python run.py
