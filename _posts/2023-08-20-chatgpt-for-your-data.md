---
layout: post
title: "ChatGPT for your data"
categories:
- programming
tags:
- AI
- ChatGPT
- LangChain
- OpenAI

permalink: "/chatgpt-for-your-data/"
---

<img src="{{ site.baseurl }}/assets/2023/data-information-knowledge-insight-wisdom.jpeg" alt="Data, information, knowledge, insight, wisdom" title="Data, information, knowledge, insight, wisdom" />

The everyday need to extract information from documents isn't exclusive to analysts or data scientists—it's a common requirement for all knowledge workers. Thanks to Large Language Models (LLMs), [embeddings](https://towardsdatascience.com/neural-network-embeddings-explained-4d028e6f0526), and [vector databases](https://www.pinecone.io/learn/vector-database/) you can create a ChatBot, which can answer your questions about a particular set of data.

It's a very powerful use case for building knowledge bases. Imagine that you want to become a triathlete. You probably have 100s of questions about how to even start. There are a lot of resources online to find answers, but it would be much better if you could just ask your questions and get answers right away.

ChatGPT is pretty good at answering questions you have, but it's not yet good enough when it comes to nuanced details. The rationale behind this lies in its limited access to the entirety of online data. Hence, there is a huge market opportunity for building domain-specific knowledge bases.

<h3>ChatBot for your data with LangChain and OpenAI</h3>

[LangChain](https://www.langchain.com/) is a framework for building LLM-based apps. Using LangChain, and OpenAI API we can create a Q&A app that points to chosen by you data source in a few lines of code.

To get started, you need Python, and a few packages:

```
pip install langchain
pip install openai
pip install chromadb GitPython bs4 tiktoken
``` 

You also need an OpenAI API key. You can get it at [https://platform.openai.com/account/api-keys](https://platform.openai.com/account/api-keys). 

New personal accounts get <span>$</span>5 free credit to use.

You need to put the OpenAI API key in `OPENAI_API_KEY` environmental variable. You can do that by adding the following line to your `~/.bash_profile` file on Mac:

```
export OPENAI_API_KEY=<YOUR_OPENAI_API_KEY>
```

Remember to run `source ~/.bash_profile` to load `OPENAI_API_KEY` into the environment.

<h4>Query data from text file</h4>

The simplest approach is to put your data into a text file.

This is a sample text file `data.txt` with a few details about me:

```
Jacob Jedryszek is a software engineer at Meta. He has experience in web and mobile development, product growth, cloud computing, and artificial intelligence.

He worked on the following products:
- 2014-2016 - Azure Portal
- 2016-2017 - Azure Mobile App
- 2017-2019 - Azure Search
- 2017-2019 - SeeingAI
- 2019-2021 - Facebook Marketplace
- 2022 - Super - Live Q&A platform for creators

His hobbies are:
- cycling
- triathlons
- hiking
- sailing
- soccer
- martial arts
```

This Python program allows you to query that text file:

{% highlight python %}
from langchain.document_loaders import TextLoader
from langchain.indexes import VectorstoreIndexCreator

loader = TextLoader("./data.txt")
index = VectorstoreIndexCreator().from_loaders([loader])

print(index.query("Who is Jacob?"))
{% endhighlight %}

The result of running the above program is:

```
> python qna-text.py
Jacob Jedryszek is a software engineer at Meta with experience in web 
and mobile development, product growth, cloud computing, and artificial 
intelligence. He has worked on several products, including Azure Portal, 
Azure Mobile App, Azure Search, SeeingAI, Facebook Marketplace, 
and Super. His hobbies include cycling, triathlons, hiking, sailing, 
soccer, and martial arts.
```

When I change the query to `When did Jacob work on SeeingAI?` I get the following answer:

```
> python qna-text.py
2017-2019
```

This is mind-blowing! With just 5 lines of code, you can easily extract insights from your data!

<h4>Query data from web page</h4>

You can also query data from a given URL. I recently wrote a blog post about weight loss. You can query it with LangChain by replacing `TextLoader` with `WebBaseLoader`:

{% highlight python %}
from langchain.document_loaders import WebBaseLoader
from langchain.indexes import VectorstoreIndexCreator

loader = WebBaseLoader("https://jj09.net/simple-path-to-weight-loss")
index = VectorstoreIndexCreator().from_loaders([loader])

print(index.query("How can I lose weight without exercising?"))
{% endhighlight %}

Running the above program gives the following answer:

```
> python qna-web.py
You can lose weight without exercising by counting calories and macros and eating fewer calories than you burn. A 500 calorie deficit per day can result in losing 1 pound per week.
```

<h4>Other loaders</h4>

As of today, there are a lot of different loaders available for LangChain. You can load data directly from PDF, Azure Storage, CSV files, Google Drive, Github, and more! You can learn how to use each loader at [LangChain Loaders docs](https://python.langchain.com/docs/integrations/document_loaders/).

<h3>Using local LLM</h3>

Using OpenAI API is pretty expensive. Depending on how large your document is you can quickly utilize free limit. Running 1000 queries on a document with ~3000 words would cost you <span>$7</span>. For more about pricing check [OpenAI API Pricing Calculator](https://gptforwork.com/tools/openai-chatgpt-api-pricing-calculator).

If you don't want to pay for OpenAI API, you can use one of the Large Language Models locally. OpenAI models are not open source, but there are a lot of alternatives. One of them is [GPT4All](https://gpt4all.io/). Iván Martínez created an awesome Github repo [privateGPT](https://github.com/imartinez/privateGPT). It uses [`sentence-transformers`](https://www.sbert.net/) python package to create embeddings with one of the [Open Source embedding models](https://huggingface.co/spaces/mteb/leaderboard), and [GPT4All](https://gpt4all.io/) - LLM wrapper to query your data with LangChain and one of the available Open Source LLMs. [This Youtube video](https://www.youtube.com/watch?v=jxSPx1bfl2M) shows step-by-step how to do it.

I got the best result by using [nous-hermes-13b.ggmlv3.q4_0.bin](https://huggingface.co/TheBloke/Nous-Hermes-13B-GGML/blob/main/nous-hermes-13b.ggmlv3.q4_0.bin) model. It's 7.32GB, while default [ggml-gpt4all-j-v1.3-groovy.bin](https://gpt4all.io/models/ggml-gpt4all-j-v1.3-groovy.bin) is 3.79GB, but it produces much better results.

<h3>Fine tunning LLM</h3>

Another option to build a "ChatGPT for your data" is through Fine-tuning. It involves taking a pre-trained large language model (LLM) and adapting it to comprehend and respond to specific questions related to your dataset. By further training the model on a narrower dataset containing questions and answers relevant to your domain, you can enhance its ability to provide accurate and contextually relevant responses.

Finetuning allows the chatbot to learn the nuances of your data, making it more proficient in answering questions accurately. This approach can be particularly useful when you have a specific dataset with domain-specific information, and you want the chatbot to be a knowledgeable and effective tool for interacting with that data.

This approach is much more complicated than using embeddings, requires multiple steps, and more computational power. Additionally, you have to retrain your model whenever your data changes, which is more expensive than creating embeddings.

To see a sample Fine-tuning process, check out [how to make GPT perform 10x for your use case](https://www.youtube.com/watch?v=Q9zv369Ggfk).

<h3>Summary</h3>

You can build Q&A ChatBot for your data with LangChain and OpenAI API. If you don't want to pay for OpenAI API, you can use the Open Source model locally. This still requires computational power but might be cheaper than paying for OpenAI API if you run it in production. 

You can also consider Fine-tuning the pre-trained model. It's more complicated, requires significant computational power, and you need to re-train your model whenever your dataset changes.

In the end, you can build products like [Chat with any PDF](https://chatpdf.com).

To learn more details, and how to build a more advanced ChatBot for knowledge base check out [LangChain Chat with Your Data](https://www.deeplearning.ai/short-courses/langchain-chat-with-your-data/).

If you want to learn more about LangChain Framework, I recommend [LangChain for LLM Application Development](https://www.deeplearning.ai/short-courses/langchain-for-llm-application-development/).

[LangChain documentation](https://docs.langchain.com/docs/) is also a pretty solid source of knowledge.