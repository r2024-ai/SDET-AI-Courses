# Getting started with Practice LLM's and the approach to evaluate/Test

## 11. Demo of Practice RAG LLM's to evaluate and write test automation scripts

> From user perspective there is no differentiation whether  
it is a RAG based or a normal LLM. Overall it is a LLM model built on RAG frame. That's all.  

> When you come to testing the first thing what you need to remember is you cannot compare testing normal software application.

### Testing LLMs: A New Approach

* Traditional Software Testing

In traditional software testing, we directly assert on system  
responses. This approach involves comparing expected outputs  
with actual outputs from the system under test.  

* LLM Testing

Testing LLMs involves evaluating the quality of their responses  
using benchmark metrics. These metrics help "sess the model's  
performance based on relevance, accuracy, and other qualitative  
aspects.

## 12. Understanding implementation part of practice RAG LLM's to understand context

API - https://rahulshettyacademy.com/rag-llm/ask

Payload - 

```json
{
    "question": "How many articles are there in the Selenium WebDriver Python course?",
    "chat_history": []
}

```

## 13. Understand conversational LLM scenarios and how they are applied to RAG Arch

![alt text](image-1.png)

![alt text](image-2.png)

Conversational LLM scenarios refer to how Large Language Models (LLMs) engage in dialogues across different contexts, such as customer support, content generation, tutoring, and decision support. In **Retrieval-Augmented Generation (RAG) architecture**, LLMs are combined with information retrieval systems to enhance responses with external, up-to-date, and domain-specific knowledge.  

### **Conversational LLM Scenarios in RAG Architecture**  

1. **Customer Support & Chatbots**  
   - **Application**: Users ask product-related queries, and the LLM fetches relevant knowledge base articles before generating a response.  
   - **RAG Role**: Retrieves FAQs, manuals, and troubleshooting guides in real time, ensuring accurate and context-aware responses.  

2. **Enterprise Knowledge Management**  
   - **Application**: Employees seek information about policies, HR procedures, or IT support within an organization.  
   - **RAG Role**: Connects the LLM with internal documentation, enabling precise answers without needing extensive model fine-tuning.  

3. **Medical & Legal Assistance**  
   - **Application**: Doctors or lawyers ask questions, and the system provides contextually rich answers using medical journals or case law databases.  
   - **RAG Role**: Retrieves up-to-date legal precedents or medical research papers to enhance reliability and accuracy.  

4. **Personalized Tutoring & Learning Assistants**  
   - **Application**: Students ask subject-related questions, and the assistant provides structured explanations.  
   - **RAG Role**: Retrieves content from textbooks, research papers, and verified educational sources before generating an answer.  

5. **Code Assistance & DevOps Automation**  
   - **Application**: Developers seek help with debugging, code generation, or best practices.  
   - **RAG Role**: Retrieves documentation, Stack Overflow discussions, and API references to provide relevant and accurate responses.  

6. **Financial Advisory & Market Insights**  
   - **Application**: Investors query market trends, stock recommendations, or economic analyses.  
   - **RAG Role**: Pulls data from financial reports, SEC filings, and real-time news sources to ensure informed responses.  

### **How RAG Enhances Conversational LLMs**  

- **Accuracy & Freshness**: Retrieves real-time or updated information from external sources, reducing hallucinations.  
- **Domain Adaptability**: Eliminates the need for full retraining by dynamically integrating with structured and unstructured data.  
- **Context Awareness**: Maintains conversation history while fetching relevant information for improved user interactions.  



### Ragas Library

Ragas is a library that provides to supercharge the evaluation  
of LLM application. It is designed to help you evaluate your LLM applications with ease and confidence.

[Ragas](https://github.com/explodinggradients/ragas) is an **evaluation framework for Retrieval-Augmented Generation (RAG)** systems. It helps **assess retrieval quality, grounding, answer correctness, and hallucinations** in AI-generated responses.

---

## **🔍 Why Use Ragas?**
✅ Evaluates **retrieval relevance** and **faithfulness** of answers  
✅ Detects **hallucinations** (misleading or incorrect responses)  
✅ Computes **semantic similarity** of generated responses  
✅ Integrates with **LLMs like GPT-4 and embeddings like OpenAI, Cohere**  
✅ Supports **dataset-based testing** for continuous monitoring  

---

## **📌 Key Features of Ragas**
1. **Retrieval Quality Metrics** (Precision, Recall, MRR, NDCG)  
2. **Grounding Score** (Measures factual consistency)  
3. **Answer Correctness** (Ensures the LLM-generated answer aligns with retrieved context)  
4. **Hallucination Detection** (Identifies whether the response contains non-grounded claims)  
5. **End-to-End Evaluation** (Combines retrieval and generation evaluation)  

---

## **🛠️ How to Install & Use Ragas**
### **1️⃣ Install Ragas**
```sh
pip install ragas
```
or (if using `pip`)
```sh
pip install git+https://github.com/explodinggradients/ragas.git
```

---

### **2️⃣ Load & Prepare Data**
```python
from datasets import load_dataset

# Load a sample RAG dataset
dataset = load_dataset("explodinggradients/ragas_squad", split="test")
print(dataset[0])  # View a sample data point
```
📌 **Dataset Structure:**  
- `query`: The user's input  
- `contexts`: The retrieved documents  
- `answer`: The expected response  

---

### **3️⃣ Evaluate RAG Performance**
```python
from ragas import evaluate
from ragas.metrics import (
    context_precision, 
    context_recall, 
    faithfulness, 
    answer_correctness
)

# Compute retrieval and generation metrics
results = evaluate(
    dataset, 
    metrics=[context_precision, context_recall, faithfulness, answer_correctness]
)

print(results)  # Displays evaluation scores
```
📌 **Metrics Explanation:**  
- `context_precision`: Measures how many retrieved docs are relevant  
- `context_recall`: Checks if all relevant docs were retrieved  
- `faithfulness`: Ensures answer is grounded in retrieved documents  
- `answer_correctness`: Evaluates factual accuracy of AI response  

---

### **4️⃣ Detect Hallucinations**
```python
from ragas.metrics import hallucination

hallucination_score = evaluate(dataset, metrics=[hallucination])
print(hallucination_score)  # Lower is better
```
✔ **Low scores = fewer hallucinations**  
✔ **Helps fine-tune retrieval or improve LLM response generation**  

---

## **🚀 When to Use Ragas?**
✅ **Testing RAG Pipelines** in **LLM apps, chatbots, or QA systems**  
✅ **Comparing retrieval strategies** (BM25, FAISS, Hybrid Search)  
✅ **Tracking model drift** (Detecting AI-generated hallucinations over time)  
✅ **Automating quality checks** for **production-ready RAG systems**  

---

## **🎯 Final Thoughts**
**Ragas.io** makes RAG evaluation **easy, automated, and scalable**! 🚀  
Would you like **a demo script** to evaluate a custom **LLM + Retriever setup**? 😊


## Understand the Metric benchmarks for Document Retrieval system in LLM

Both **Context Recall** and **Context Precision** are metrics used to evaluate the   
effectiveness of a document retrieval system. They a assess different aspects of how well the system retrieves relevant documents in response to a query.

![alt text](image-3.png)