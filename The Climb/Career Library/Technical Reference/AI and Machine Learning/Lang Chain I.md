---
kind: "study-reference"
title: "Lang Chain I"
collection: "AI and Machine Learning"
topic: "AI and Machine Learning"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/Lectures/AI/LangChain_I.ipynb"]
tags: ["career/library"]
source_status: "source-reference"
---

# Lang Chain I

[[The Climb/Career Library/Career Library]]

# ChatModels

```python
!pip install langchain #core langchain package
!pip install -U langchain-google-genai #partner packages
!pip install -qU langchain-groq #partner packages
```

```python
from langchain_google_genai import ChatGoogleGenerativeAI

llm_google = ChatGoogleGenerativeAI(model="gemini-1.5-pro-exp-0801", google_api_key="[credential redacted]")
```

```python
from langchain_groq import ChatGroq

llm = ChatGroq(model="llama-3.1-8b-instant", temperature=0.2, groq_api_key="[credential redacted]")
```

```python
def generate(query, model):
  if model=="google":
    llm = llm_google
  elif model=="groq":
    llm = llm_groq
  res = llm.invoke(query)
  return res.content
```

```python
query = "what is the best way to learn the math behind llms"
print(generate(query, "google"))
print("______"*50)
print(generate(query, "groq"))
```

# OutputParser

```python
from langchain_groq import ChatGroq

llm = ChatGroq(model="llama-3.1-8b-instant", groq_api_key="[credential redacted]")
```

```python
from langchain_core.output_parsers import StrOutputParser

parser = StrOutputParser()
```

```python
chain = llm | parser   # "hey" -> llm -> parser -> "How's it going? Is there something I can help you with or would you like to chat?"
```

```python
chain.invoke("hey")
```

# Messages/Prompts

```python
# Ask LLM to act as English to Italian Translator
# System: You are a translator. Translate the following from English into Italian.
# User: Hi
# >>>>>
# Assistant: Ciao
```

```python
from langchain_core.messages import HumanMessage, SystemMessage

s_msg = SystemMessage(content="You are a translator. Translate the following from English into Tamil.")
h_msg = HumanMessage(content="Hi")

messages = [
    s_msg,
    h_msg
]
messages
```

```python
chain = llm
chain.invoke(messages)
```

# PromptTemplate

```python
system_template = "You are a translator. Translate the following from English into {language}."
user_template = "{text}"
messages_template = [
    ("system", system_template),
    ("user", user_template)
]
```

```python
from langchain_core.prompts import ChatPromptTemplate
prompt_template = ChatPromptTemplate.from_messages(messages_template)
```

```python
prompt_template
```

```python
prompt_template.invoke({"language":"Tamil", "text": "hi"})
```

```python
# {"language":"Tamil", "text": "hi"} -> prompt_template -> llm -> output_parser -> "Vanakkam"
```

```python
chain = prompt_template | llm_groq | parser
```

```python
chain.invoke({"language":"Tamil", "text": "hi"})
```

```python
chain.invoke({"language":"Telugu", "text": "hi"})
```

```python
chain.invoke({"language":"Italian", "text": "Bye"})
```

```python
chain.invoke({"language":"Italian", "text": "Hi"})

```

```python

```



## Notebook conversion

Markdown and code cells are preserved. Execution outputs, widgets, and runtime state remain in the external notebook; no notebook code was executed.

## Source provenance

- [Original IPYNB](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/Lectures/AI/LangChain_I.ipynb) · CODING RESOURCES/Lectures/AI/LangChain_I.ipynb

Original files remain unchanged outside the vault. Imported code is a reference, not tested or certified.
