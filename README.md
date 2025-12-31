# AI Food Recommendation Chatbot: Multi-Agent RAG System

## Project Overview

The AI Food Recommendation Chatbot is a sophisticated multi-agent system aimed at providing personalized, context-aware food recommendations through natural conversation. Built upon a Retrieval-Augmented Generation (RAG) paradigm, the system leverages advanced user modeling, conversational memory, semantic retrieval, and explainable reranking to optimize food suggestions for individual users. Its modular agents, robust data engineering, and user clustering ensure relevance, scalability, and adaptability for varying user behaviors and food contexts.

---

## Workflow Overview

### Workflow Steps

### 1. User Input
Users engage the chatbot with food-related queries or preferences  
(e.g., “Show me spicy veg biryani under 300”).

---

### 2. Conversational Agent
- **Intent Classification**  
  Determines the intent of the user such as greeting, goodbye, preference updation, recommendation request, or preference specification.
- **Slot Extraction**  
  Extracts structured information from the conversation such as dietary type, cuisine, dish, price range, etc.
- **Memory Updation**  
  Updates session memory to retain user preferences and conversational context.

---

### 3. Recommendation Sufficiency Check
- Decides whether sufficient information is available to generate recommendations.
- If not, asks targeted follow-up questions.
- If yes, triggers retrieval and re-ranking.

---

### 4. Retrieval Agent
- **Query Enhancer**  
  Transforms structured slots into optimized semantic search queries and filters.
- **Retrieval from Shards**  
  Performs semantic searches over distributed, sharded databases of food items.

---

### 5. Re-ranking Agent
- **Condition Generation & Evaluation**  
  Generates context-sensitive and explainable ranking rules based on the user’s food journey and menu diversity.
- **Evaluator & Top-10 Identifier**  
  Scores, explains, and selects the top 10 most relevant food items.

---

### 6. Output
- Presents ranked recommendations or additional clarification questions.
- The interaction loop continues until user satisfaction is achieved.

---

## Folder Description

- **Python Files**  
  Contains all core Python scripts required to run the system. The codebase is modular to support easy scalability and future enhancements.

- **User_clustering_file**  
  Contains files related to the user clustering module. K-Means++ is used for clustering users into behavioral personas.

- **Application**  
  Contains frontend files built using Gradio and their integration with the orchestrator.

- **Data Cleaning and Feature Engineering**  
  Includes all preprocessing scripts and notebooks for cleaning datasets and engineering features.

- **Embedding and Shards Creation**  
  Contains scripts and notebooks for generating embeddings and creating database shards. The shard download link is provided below.

- **Demo_final_compressed.mp4**  
  Demo video showcasing the complete application flow with multiple usage scenarios.

- **Case_presentation.pdf**  
  Presentation describing the motivation, usability, and key findings of the project.

- **Report.pdf**  
  Detailed technical report explaining system architecture, methodology, and implementation.

---

## Solution Architecture

### 1. Conversational Agent
**File:** `conversation_agent.py`

- Intent Classification using LLMs with fallback pattern recognition (`intent_classifier.py`)
- Slot Extraction using prompt-based methods and rule-based logic (`slot_extract.py`, `query_enhancer.py`)
- Stateful Memory Management (`memory.py`)
- Outputs structured preferences and user intent for pipeline orchestration

---

### 2. Recommendation Sufficiency Check
- Embedded within `conversation_agent.py`
- Checks availability of essential constraints such as dietary preference and price range
- Routes control flow based on information completeness

---

### 3. Retrieval Agent
**Files:** `shards_retrieval.py`, `orchestrator.py`

- Query refinement and optimization using `query_enhancer.py`
- Distributed semantic search over ChromaDB shards using dense embeddings (`embeddings.py`)
- Designed for scalability and low-latency retrieval

---

### 4. Re-ranking Agent
**Files:** `rerank.py`, `rerank_prompts.py`

- Context-aware and explainable re-ranking using user session context
- Evaluates food diversity, preference alignment, and relevance
- Produces transparent reasoning for final recommendations

---

### 5. Embeddings & Shard Creation
**Files:** `embeddings.py`, `shards_creation.ipynb`

- Uses Sentence-Transformers to vectorize food and menu items
- Large databases are split into multiple shards for efficient parallel retrieval

---

### 6. User Clustering & Data Pre-processing
**Files:**  
`user_clustering_agent.py`, `User_Clustering_agent.ipynb`,  
`derived_feature_engineering.ipynb`, `2-cuisines.ipynb`,  
`zomato_restaurant_data_cleaning.ipynb`

- User segmentation using K-Means++ clustering based on behavioral patterns
- Feature engineering includes veg ratio, pricing tiers, cuisine affinity, etc.
- Enables deeper personalization and persona-driven recommendations

---

## Deep Dive: File Responsibilities

| File / Notebook | Description |
|----------------|-------------|
| conversation_agent.py | Manages dialogue flow, intent detection, slot extraction, and memory |
| intent_classifier.py | LLM and fallback-based intent classification |
| slot_extract.py | Structured slot extraction from user input |
| memory.py | Tracks conversation history and dialogue state |
| response_generator.py | Generates user-facing responses and follow-ups |
| query_enhancer.py | Builds optimized semantic queries and filters |
| shards_retrieval.py | Executes distributed semantic search on ChromaDB shards |
| embeddings.py | Embedding model setup and vector generation |
| shards_creation.ipynb | Step-by-step embedding and shard generation |
| rerank.py, rerank_prompts.py | Contextual re-ranking and reasoning logic |
| User_Clustering_agent.ipynb | User clustering and persona modeling pipeline |
| derived_feature_engineering.ipynb | Feature engineering and data augmentation |
| 2-cuisines.ipynb | Cuisine-level feature analysis |
| zomato_restaurant_data_cleaning.ipynb | Dataset cleaning and standardization |
| orchestrator.py | Central controller connecting all agents |
| utils.py | Utility functions, enums, and configuration constants |
| app.py | Gradio-based frontend integrated with orchestrator |

---

## Data & Model Preparation

### Data Sources
- Food Recommendation Dataset (schemersays):  
  https://www.kaggle.com/datasets/schemersays/food-recommendation-system
- Zomato Restaurants Dataset (bharathdevanaboina):  
  https://www.kaggle.com/datasets/bharathdevanaboina/zomato-restaurants-dataset
- Zomato Database (anas123siddiqui):  
  https://www.kaggle.com/datasets/anas123siddiqui/zomato-database

All datasets are cleaned, deduplicated, and merged for reliability.

---

### Feature Engineering
- Behavioral features
- Pricing tiers
- Cuisine affinity
- Dietary sensitivity indicators

---

### Embeddings & Sharding
- All food items are embedded using dense vector representations
- Stored in scalable database shards  
- **Shard Download Link:**  
  https://drive.google.com/drive/folders/1yYOu3G_TZ9srSL8hK5-hdkgP7m9wUXic

---

### User Clustering
- K-Means++ clustering assigns users to behavioral personas
- Personas guide filtering, ranking, and recommendation logic
