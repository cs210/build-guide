+++
date = '2025-01-08T10:55:07-08:00'
draft = false
title = 'Extending LLMs'
+++

# Extending LLMs

Below are some ways to go beyond just LLMs and use your custom data. These include methods such as Retrieval Augmented Generation (RAG), finetuning, and even searching over tabular data.

## Retrieval Augmented Generation
Language models are typically pretrained on vast amounts of data, but they may require updated information or data tailored to a specific use case. Retraining a language model on a large amount of data might prove to be expensive. In many scenarios, extending large language models with external knowledge bases becomes essential to provide relevant and accurate outputs. This is where **Retrieval-Augmented Generation (RAG)** comes into play. RAG consists of two key components: a retrieval system to identify relevant items or contextual information and a mechanism to integrate that information into the model's output, often through prompting.

![Retrieval-Augmented Generation Concepts](https://python.langchain.com/assets/images/rag_concepts-4499b260d1053838a3e361fb54f376ec.png)

To implement a knowledge base for RAG, you often use an embedding model, which encodes information into a lower-dimensional space, and a vector database, which performs similarity searches within that space. Tools like [Chroma](https://www.trychroma.com/), [Pinecone](https://www.pinecone.io/), and [pgvector](https://github.com/pgvector/pgvector) are popular options for this purpose. These systems enable efficient retrieval of contextually relevant data to enhance the model's responses. Below is a simple code example demonstrating this process, and you can find several excellent tutorials for further exploration.

```python
# Make sure to pip install chromadb openai 
import chromadb
from chromadb.utils import embedding_functions
from chromadb.config import Settings

# Step 1: Initialize the Chroma client
chroma_client = chromadb.Client(
    Settings(
        persist_directory="./chroma_db",  # Path to store the database
        chroma_db_impl="duckdb+parquet",  # Database backend
    )
)

# Step 2: Define the embedding function (OpenAI in this case)
openai_ef = embedding_functions.OpenAIEmbeddingFunction(
    api_key="your_openai_api_key",  # Replace with your OpenAI API key
    model_name="text-embedding-ada-002",
)

# Step 3: Create or get a collection
collection = chroma_client.get_or_create_collection(
    name="knowledge_base", embedding_function=openai_ef
)

# Step 4: Add data to the collection
documents = [
    "The Eiffel Tower is located in Paris, France.",
    "The Great Wall of China is one of the Seven Wonders of the World.",
    "Python is a popular programming language for machine learning.",
    "The Amazon Rainforest is the largest rainforest in the world.",
    "Albert Einstein developed the theory of relativity."
]
doc_ids = [f"doc_{i}" for i in range(len(documents))]

collection.add(
    documents=documents,
    ids=doc_ids
)

# Step 5: Query the collection with a similar question
query = "Who created the theory of relativity?"

results = collection.query(
    query_texts=[query],
    n_results=3  # Return top 3 most similar results
)

# Step 6: Display results
print("Query:", query)
print("Most similar documents:")
for i, doc in enumerate(results["documents"][0]):
    print(f"{i + 1}. {doc}")
```

## Finetuning

## Tabular Data