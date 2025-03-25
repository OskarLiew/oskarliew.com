---
title: "How Vector DBs search millions of vectors in millionths of seconds"
date: 2025-03-25T21:15:19+01:00
draft: true
tags:
  - Algorithms
  - Vector databases
---

When the GPT craze started in 2023, the vector database became one of the hottest technologies around, with startup companies like Pinecone raising money at $750M evaluations. The reason they took off was because Retrieval Augmented Generation (RAG) emerged as a way of connecting GPTs to external data sources and to add long-term memory to the models.

A new type of search method, utilizing deep embedding models, called semantic similarity search had started showing a lot of promise. These models capture the semantic content of texts into embedding vectors, unlike traditional search methods, which typically encode keywords. This characteristic made semantic similarity search a perfect fit for digital assistants like ChatGPT, because the same natural language queries that users sent to the model could also be used for information retrieval without being sensitive to specific keywords.

The vector databases facilitated this use case by specializing in fast and accurate retrieval of high-dimensional vectors. The retrieval works because the embedding vector of the query and content will often be near each other in the vector space and the vector database is really good at finding nearest neighbours. Vectors, which are just sequences of numbers, can of course be stored in any old database, but vector databases have a special indexing algorithm that makes them exceptionally efficient for this use case.

Nowadays there exists a plethora of vector databases and even plugins for traditional databases, like postgres, but the vast majority of them are still based on the same base algorithm, _Hierarchical Navigable Small Worlds (HNSW)_. In this article I will describe in detail how HNSW works and show how to implement the algorithm in pure no-frills python.

## Hierachical Navigable Small Worlds

HNSW is an approximate nearest neighbour search algorithm that sacrifices some retrieval accuracy and memory in exchange for speed. A naive nearest neighbour search would compare a query vector to all stored vectors, which would end up taking \\(\mathcal{O}(N)\\) time for each query. HNSW, on the other hand reduces the time complexity to \\(\mathcal{O}(\log n)\\) by being selective in which vector comparisons are made.

- Background
  - Why are vector DBs used
- What makes them specialized? HNSW
- Explain the issue with naive search
- Show that search can be made faster using NSW
- Show how it can be expanded to HNSW
