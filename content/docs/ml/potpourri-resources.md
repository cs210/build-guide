+++
date = '2025-01-08T10:55:07-08:00'
draft = false
title = 'A Potpourri of Resources'
weight = 3
+++

# A Potpourri of Resources
Below is a set of resources, ranging from popular AI/ML tooling to general advice.

## LLM Frameworks

- [Langchain](https://www.langchain.com/) is probably the most popular LLM framework. Using Langchain, you can spin up RAG pipelines, parse through PDFs and other unstructured data, and much more.
- [Vercel's AI SDK](https://sdk.vercel.ai/docs/introduction) is another SDK that can help developers build AI-powered applications. In particular, the library can help with integrating text generation, tool calling, and agentic workflows directly in your frontend code.
- [LlamaIndex](https://www.llamaindex.ai/) is another popular LLM framework that helps to enable use cases ranged from question-answering, chatbots, and even agents.

## General Advice

Below are some general tips, aggregated from industry experts and 210 alums.

### Buy first, then build

For initial functional prototyping and for most of the former part of your application's lifecycle, lean on existing APIs to do a lot of the heavy lifting. These models are already quite powerful and are able to handle almost all of the requests you send it. If certain users or design partners necessitate even more advanced functionality, though, consider working and finetuning your own LLMs.

### When unsure, lean on the literature 

Oftentimes, issues with performance lie in the technical reports. For instance, maybe your vector database isn't surfacing as great results as you think it should: it may be the case that your embedding model and vector database don't encode for the same type of similarity. Thus, leaning on the literature when unsure is a great way to build the muscle.

### Always make sure to have some form of evals
There are also tools to help with this, such as [Arize](https://arize.com/).