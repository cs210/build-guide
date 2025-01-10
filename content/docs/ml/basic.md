+++
date = '2025-01-08T10:55:07-08:00'
draft = false
title = 'Basic ML'
+++

# Basic ML

Below are some snippets for common ML use cases such as NLP -- namely, LLMs -- computer vision, and even standard statistical ML.

Our advice? *For initial functional prototyping and for most of the former part of your application's lifecycle, lean on existing APIs to do a lot of the heavy lifting.* These models are already quite powerful and are able to handle almost all of the requests you send it. If certain users or design partners necessitate even more advanced functionality, though, consider working and finetuning your own LLMs.

## Large Language Models (LLMs)
[TO-DO: ADD FINETUNING]

### Using APIs

For initial iteration, using LLM APIs is probably the best way to go. There are several models out there, each with their own strengths. Below is an example using the [OpenAI API](https://platform.openai.com/docs/quickstart?language-preference=python) to make a call to a language model:

```python3
from openai import OpenAI
client = OpenAI()

completion = client.chat.completions.create(
    model="gpt-4o-mini",
    messages=[
        {"role": "system", "content": "You are a helpful assistant."},
        {
            "role": "user",
            "content": "Write a haiku about recursion in programming."
        }
    ]
)

print(completion.choices[0].message)
```

### Custom Open-Source Models

As you continue to iterate, you may want to leverage the power of open-source models. For this, Hugging Face -- in particular, the [SentenceTransformers](https://huggingface.co/sentence-transformers) module -- will be your best friend. Just specify your language model and you'll be good to go:

```python3
from sentence_transformers import SentenceTransformer
model = SentenceTransformer('paraphrase-MiniLM-L6-v2')

# Sentences we want to encode. Example:
sentence = ['This framework generates embeddings for each input sentence']

# Sentences are encoded by calling model.encode()
embedding = model.encode(sentence)
```

Of course, utilizing an open-source model will also mean figuring out how to serve the model. There are a plethora of tools for this, including [Modal](https://modal.com/), [Baseten](https://www.baseten.co/), [Together AI](https://www.together.ai/), and many others.

