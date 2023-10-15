---
layout: post
title: "Generative AI: 10 things to know"
categories:
- programming
tags:
- AI
- GenAI

permalink: "/generative-ai-10-things-to-know/"
---

<img src="{{ site.baseurl }}/assets/2023/generative-ai.jpeg" title="Generative AI" title="Generative AI" />

Generative Artificial Intelligence (GenAI) has shown remarkable advancements in recent years and has the potential to revolutionize various industries by automating creative tasks, generating realistic content, and assisting humans in creative endeavors. GenAI is a subset of AI techniques and models that are designed to generate new text, images, videos, or audio content that is similar to what humans produce. This article explains the 10 most important things you need to know about the Generative AI world.

<h3>1. Large Language Model (LLM)</h3>

A large language model (LLM) is characterized by its large size. LLM can have over a trillion parameters, and take multiple Gigabytes of storage. Its size is enabled by AI accelerators, which can process vast amounts of text data, mostly scraped from the Internet. LLM is a [neural network](https://en.wikipedia.org/wiki/Artificial_neural_network) that can contain from tens of millions and up to billions of weights and is (pre-)trained using [self-supervised learning](https://en.wikipedia.org/wiki/Self-supervised_learning) and [semi-supervised learning](https://en.wikipedia.org/wiki/Weak_supervision).

Language models work by taking an input text and repeatedly predicting the next token or word. Up to 2020, fine-tuning was the only way a model could be adapted to be able to accomplish specific tasks. Larger-sized models, such as [GPT-4](https://openai.com/gpt-4) or [Llama 2](https://ai.meta.com/llama/), however, can be prompt-engineered to achieve similar results.

You can find a lot of open-source Large Language Models on [HuggingFace](https://huggingface.co/models), and build products on top of them!

<h3>2. Fine-tuning</h3>

You take a trained LLM and use new data to update its parameters for new settings or repurpose it for new applications. Fine-tuning can be done on the entire neural network, or on only a subset of its layers, in which case the layers that are not being fine-tuned are "frozen" (not updated during the backpropagation step).

To get a glimpse into the fine-tuning process check ["okay, but I want GPT to perform 10x for my specific use case" - Here is how](https://www.youtube.com/watch?v=Q9zv369Ggfk).

To learn more details about Fine-tuning LLMs I recommend:
- [Fine-tuning Large Language Models](https://www.deeplearning.ai/short-courses/finetuning-large-language-models/) from [DeepLearning.AI](https://www.deeplearning.ai/) 
- [Fine-tuning LLMs](https://teetracker.medium.com/fine-tuning-llms-9fe553a514d0)
- [A Complete Guide to Fine Tuning Large Language Models](https://www.simform.com/blog/completeguide-finetuning-llm/)

<h3>3. Prompt engineering</h3>

Prompt engineering is a technique used in working with AI models, especially in the context of text-to-text models. It involves crafting well-structured and specific instructions or queries, known as prompts, to guide the AI in generating desired outputs. These prompts help the AI understand the task and generate relevant and accurate responses. Prompt engineering can include providing context, examples, instructions, or even specifying styles to ensure the AI produces the intended results.

You might be heard about Zero-shot prompting or few-shot prompting. Zero-shot prompting involves instructing a model to perform a task or generate text without providing any specific examples or labeled data during inference. This is what we usually do when using ChatGPT.

Example of zero-shot prompt:

```
What's the sentiment of this review: "It doesnt work!"
```

ChatGPT response:

```
The sentiment of the review "It doesn't work!" is negative.
```

Few-shot prompting, on the other hand, provides the model with a few examples or context during inference.

Example of a few-shot prompt:

```
Great product, 10/10: positive
Didn't work very well: negative
Super helpful, worth it: positive
It doesnt work!:
```

ChatGPT response:

```
The sentiment of the review "It doesn't work!" is negative.
```

To learn more about Prompt Engineering I recommend [ChatGPT Prompt Engineering for Developers](https://learn.deeplearning.ai/chatgpt-prompt-eng) from [DeepLearning.AI](https://www.deeplearning.ai/).

<h3>4. Hallucination</h3>

In the context of Generative AI, "hallucination" refers to a situation where an AI model generates content that is not accurate or coherent based on the input or context. It essentially creates information that doesn't exist in the source data or doesn't align with the intended output. Hallucinations can occur when AI models extrapolate too much from the given data or when they lack proper training on specific aspects, leading to the generation of unrealistic or inaccurate content.

Imagine a language model trained on a large dataset of medical information. When asked to generate a description of a medical condition, the model responds with a detailed explanation that includes symptoms and treatments that don't exist in reality. This response is a hallucination because the AI has generated information that is not accurate based on its training data, creating a scenario that doesn't align with actual medical knowledge.

Hallucination is one of the biggest challenges in creating Large Language Models. It's often hard to distinguish hallucination from accurate information in AI-generated content. That's why it's important to critically evaluate AI outputs and cross-reference them with reliable sources before considering them as factual information.

<h3>5. Transformer</h3>

A Transformer is a type of deep learning model architecture used in natural language processing tasks. Transformers are designed to handle sequential data, like sentences in language, in a more effective and context-aware way. Thanks to transformers we can train LLMs faster.

The core innovation of the Transformer is its "self-attention" mechanism, which allows the model to weigh the importance of different words in a sentence relative to each other. This enables the model to capture contextual relationships between words, making it well-suited for tasks like machine translation, text summarization, question-answering, and more. Transformers have become the foundation for various state-of-the-art natural language processing models, including [GPT](https://en.wikipedia.org/wiki/Generative_pre-trained_transformer) (Generative Pre-trained Transformer) and [BERT](https://en.wikipedia.org/wiki/BERT_(language_model)) (Bidirectional Encoder Representations from Transformers).

The Transformer model is highly parallelizable, which makes it well-suited for training on large datasets using modern hardware such as GPUs or TPUs. It has been shown to achieve state-of-the-art performance on a wide range of natural language processing tasks, including machine translation, language modeling, and text classification.

<h3>6. GPT</h3>

GPT stands for "Generative Pre-trained Transformer." GPT models are designed to understand and generate human-like text by learning patterns from massive amounts of text data. The "Transformer" architecture they're based on enables them to consider the context of words and phrases in a text, making their generated content coherent and contextually relevant. These models have been widely used for tasks like text generation, language translation, and more.

[GPT-4](https://openai.com/gpt-4) is used by [ChatGPT](https://chat.openai.com/).

<h3>7. BERT</h3>

BERT stands for "Bidirectional Encoder Representations from Transformers." It's a sophisticated pre-trained language model developed by Google AI. BERT's key innovation is its bidirectional context understanding, meaning it considers both the left and right context of words in a sentence. This makes it particularly skilled at understanding the nuances of language and context.

BERT is often used as a base model for various natural language processing tasks, like text classification, question answering, sentiment analysis, and more. By fine-tuning BERT on specific tasks, it can provide impressive results due to its advanced contextual understanding.

There are a lot of [BERT-based models on HuggingFace](https://huggingface.co/models?sort=trending&search=bert).

<h3>8. Embeddings</h3>

Embeddings in AI are numerical representations of objects or concepts within a higher-dimensional space. They are used to capture the relationships and meanings between these objects in a way that a machine-learning model can understand and work with.

In natural language processing, word embeddings are commonly used to represent words as dense vectors. These vectors are designed so that similar words have similar embeddings, and their relative distances in the vector space reflect semantic relationships. Embeddings allow AI models to process and analyze textual data by converting words into numerical forms that retain their contextual meanings.

To create embeddings you need a pre-trained [embedding model](https://huggingface.co/blog/getting-started-with-embeddings). There are a lot of [open-source embedding models on HuggingFace](https://huggingface.co/spaces/mteb/leaderboard).

To learn more about embeddings check [Neural Network Embeddings Explained](https://towardsdatascience.com/neural-network-embeddings-explained-4d028e6f0526) - it's a great, detailed overview of embeddings.

<h3>9. Vector databases</h3>

Vector databases are specialized databases designed to efficiently store and query high-dimensional vector data. These databases are optimized for working with data that can be represented as vectors in a multi-dimensional space, such as embeddings from machine learning models or other numerical representations.

Vector databases offer efficient indexing and querying mechanisms that allow you to perform similarity searches, finding vectors that are closest in terms of distance to a given query vector. They are commonly used in various applications, including recommendation systems, content retrieval, image search, and natural language processing tasks where vector representations play a crucial role in understanding and comparing data points.

The most popular Vector databases are [Pinecone](https://www.pinecone.io/) and [chroma](https://www.trychroma.com/).

Other database engines are starting to introduce vector search capabilities:
- [MongoDB Vector Search](https://www.mongodb.com/blog/post/introducing-atlas-vector-search-build-intelligent-applications-semantic-search-ai)
- [Redis Vector Similarity](https://redis.io/docs/interact/search-and-query/search/vectors/)
- [Vector Search in Azure Search](https://www.youtube.com/watch?v=Bd9LWW4cxEU)
- [Elasticsearch Vector Database](https://www.elastic.co/elasticsearch/vector-database)

The most powerful application of Vector databases is to use them as [knowledge extensions or long-term memory for Large Language Models](https://www.linkedin.com/pulse/3-ways-vector-databases-take-your-llm-use-cases-next-level-mishra/). This is how I created [ChatGPT for your data](/chatgpt-for-your-data).

Check [What is a Vector Database?](https://www.pinecone.io/learn/vector-database/) from Pinecone to learn about details of how vector databases work.

<h3>10. Prompt injection</h3>

Prompt injection is a technique of adding carefully crafted prompts or instructions to the input of a language model to influence its generated output. This is commonly used in the context of fine-tuning or guiding the behavior of a generative AI model. By injecting prompts, developers can guide the model's responses toward specific themes, tones, or styles, making the generated content more aligned with their desired outcomes. Prompt injection is a way to shape the AI's creative process while maintaining control over the generated results.

Prompt injection can be also a vulnerability. Prompt Injection in the world of Generative AI is similar to what SQL Injection is in the world of databases. Check [Prompt injection attacks against GPT-3](https://simonwillison.net/2022/Sep/12/prompt-injection/) to learn more.

<h3>Summary</h3>

To learn more GenAI terms check out [Glossary of LLM and Generative AI](https://medium.com/@shuchaobi/glossary-of-llm-and-generative-ai-b3111da41da7).

Check out my previous post about [ChatGPT for your data](/chatgpt-for-your-data) where I created Q&A app for querying your own data with natural language. Like you would ask ChatGPT.