# 2025-2 Artificial Intelligence Term Project: Hybrid RAG System

> **Team 10** | Ewha Womans University  
> **Topic:** Improving Benchmark Performance on `Ewha.pdf` & `MMLU-Pro` using Hybrid RAG

## 📌 Project Overview
This project aims to enhance Large Language Model (LLM) performance on specific domains without fine-tuning. We implemented a **Hybrid RAG System** that dynamically routes queries to specialized pipelines based on the input language, utilizing the **Upstage Solar-Pro API**

### 🎯 Objectives
* **No Fine-tuning:** Achieve high accuracy using only RAG and Prompt Engineering techniques.
* **Dual Domain Handling:**
    1.  **Korean:** Q&A based on *Ewha Womans University Regulations* (`Ewha.pdf`)
    2.  **English:** Expert-level QA on *MMLU-Pro* (Law, Psychology, Business, Philosophy, History)

---

## 🏗️ System Architecture
<img width="785" height="368" alt="스크린샷 2025-12-17 15 32 57" src="https://github.com/user-attachments/assets/70277bc1-6934-4a7e-9531-b6831b156ba0" />




## 📊 Performance

| Dataset | Strategy | Accuracy |
| :--- | :--- | :--- |
| **Ewha.pdf** | One-shot + Ensemble Retriever | **96.0%** |
| **MMLU-Pro** | Category-Specific Prompt | **80.0%** |
| **Overall** | Hybrid Routing Strategy | **~88%** |



