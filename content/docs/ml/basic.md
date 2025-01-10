+++
date = '2025-01-08T10:55:07-08:00'
draft = false
title = 'Basic ML'
+++

# Basic ML

Below are some snippets for common ML use cases such as NLP -- namely, LLMs -- computer vision, and even standard statistical ML.

[TO-DO: ADD FINETUNING]

## Large Language Models (LLMs)

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

## Computer Vision

Similar to LLMs, there are several Vision APIs available that can be used for quick experimentation. All of the larger cloud platforms have existing offerings -- namely [GCP](https://cloud.google.com/vision/docs) and [Azure](https://learn.microsoft.com/en-us/azure/ai-services/computer-vision/) -- but it's also important to note that many of the SOTA models are already multimodal. For instance, [GPT-4V](https://platform.openai.com/docs/guides/vision?lang=node) already has strong vision capabilities:


```python3
from openai import OpenAI
client = OpenAI()

response = client.chat.completions.create(
    model="gpt-4o-mini",
    messages=[
        {
            "role": "user",
            "content": [
                {"type": "text", "text": "What's in this image?"},
                {
                    "type": "image_url",
                    "image_url": {
                        "url": "https://upload.wikimedia.org/wikipedia/commons/thumb/d/dd/Gfp-wisconsin-madison-the-nature-boardwalk.jpg/2560px-Gfp-wisconsin-madison-the-nature-boardwalk.jpg",
                    },
                },
            ],
        }
    ],
    max_tokens=300,
)

print(response.choices[0])
```

For using custom models, the [`torchvision`](https://pytorch.org/vision/stable/index.html#module-torchvision) is a good place to start. An often common use case is to take a pre-trained image classification or segmentation model and further finetuning it for a specific task. This is also known as transfer learning, and there are several [tutorials](https://pytorch.org/tutorials/beginner/transfer_learning_tutorial.html) out there for the task.

## Statistical ML

Finally, for simple problems, statistical techniques may be sufficient.