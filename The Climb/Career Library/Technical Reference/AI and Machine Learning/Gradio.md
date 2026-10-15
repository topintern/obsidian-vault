---
kind: "study-reference"
title: "Gradio"
collection: "AI and Machine Learning"
topic: "AI and Machine Learning"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/Lectures/AI/Gradio.ipynb"]
tags: ["career/library"]
source_status: "source-reference"
---

# Gradio

[[The Climb/Career Library/Career Library]]

```python
%pip install --upgrade --quiet  langchain-google-genai langchain langchain-openai langgraph langchain-community
```

```python
import getpass
import os

if "GOOGLE_API_KEY" not in os.environ:
    os.environ["GOOGLE_API_KEY"] = getpass.getpass("Provide your Google API key here")
```

```python
from langchain_google_genai import GoogleGenerativeAIEmbeddings

embeddings = GoogleGenerativeAIEmbeddings(model="models/embedding-001")

def cosine_similarity(text1, text2):
    embedding1 = embeddings.embed_query(text1)
    embedding2 = embeddings.embed_query(text2)
    dot_product = sum(embedding1[i] * embedding2[i] for i in range(len(embedding1)))
    magnitude1 = sum(embedding1[i] ** 2 for i in range(len(embedding1))) ** 0.5
    magnitude2 = sum(embedding2[i] ** 2 for i in range(len(embedding2))) ** 0.5
    return dot_product / (magnitude1 * magnitude2)
```

# Gradio

```python
%pip install gradio
```

```python
import gradio as gr

demo = gr.Interface(fn=cosine_similarity, inputs=["textbox","textbox"], outputs="textbox")

demo.launch(debug=True, share=True, auth=("user", "pass"))
```

```python

```

# ChatBot

```python
import getpass
api_key = getpass.getpass("OpenAI Key:")

import os
os.environ["TAVILY_API_KEY"] = getpass.getpass("Tavily API:")
```

```python
from langchain_openai import ChatOpenAI
from langchain_community.tools import TavilySearchResults
from langgraph.checkpoint.memory import MemorySaver
from langgraph.prebuilt import create_react_agent  #ReAcT is a prompting technique that we will see in further sessions

llm = ChatOpenAI(
    model="gpt-4o-mini",
    api_key=api_key
)

search = TavilySearchResults(max_results=5)  # google search alternativex
tools = [search]

memory = MemorySaver()

agent_executor_with_memory = create_react_agent(llm, tools, checkpointer=memory)

config = {"configurable":{"thread_id": "mike"}}
```



```python
import gradio as gr

def chat(message, history):
    res = agent_executor_with_memory.invoke({"messages": message}, config)
    return res["messages"][-1].content

def save():
    print(list(memory.list(config)))
    return True

save_btn = gr.Button(save)
gr.ChatInterface(chat, retry_btn=save_btn).launch(debug=True, share=True, auth=("user", "genai"))
```

```python

```

## Notebook conversion

Markdown and code cells are preserved. Execution outputs, widgets, and runtime state remain in the external notebook; no notebook code was executed.

## Source provenance

- [Original IPYNB](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/Lectures/AI/Gradio.ipynb) · CODING RESOURCES/Lectures/AI/Gradio.ipynb

Original files remain unchanged outside the vault. Imported code is a reference, not tested or certified.
