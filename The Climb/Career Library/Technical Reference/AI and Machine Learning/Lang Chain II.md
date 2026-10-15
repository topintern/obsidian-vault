---
kind: "study-reference"
title: "Lang Chain II"
collection: "AI and Machine Learning"
topic: "AI and Machine Learning"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/Lectures/AI/LangChain_II.ipynb"]
tags: ["career/library"]
source_status: "source-reference"
---

# Lang Chain II

[[The Climb/Career Library/Career Library]]

```python
import os
os.environ["LANGCHAIN_TRACING_V2"]="true"
os.environ["LANGCHAIN_ENDPOINT"]="https://api.smith.langchain.com"
os.environ["LANGCHAIN_API_KEY"]="<your api key>"
os.environ["LANGCHAIN_PROJECT"]="chatbot-genai"
```

```python
!pip install langchain langchain-groq
```

```python
from langchain_groq import ChatGroq
llm = ChatGroq(model="llama-3.1-8b-instant", groq_api_key="[credential redacted]")
llm = llm | parser
```

# Recipe Example

```python
from langchain_core.prompts import ChatPromptTemplate
from langchain_core.output_parsers import StrOutputParser

parser = StrOutputParser()

user_template = "Please recommend recipe considering the following details:Ingredients:{ingredients} Diet:{diet} Meal Type:{meal}"
messages_template = [
    ("user", user_template)
]

prompt_template = ChatPromptTemplate.from_messages(messages_template)


def recommend_recipe(ingredients, diet, meal, temp=1.0):
  llm = ChatGroq(model="llama-3.1-8b-instant", temperature=temp, groq_api_key="[credential redacted]")
  chain = prompt_template | llm | parser
  results = chain.invoke({
      "diet": diet,
      "ingredients": ingredients,
      "meal": meal
  })
  return results

```

```python
# print(recommend_recipe("milk,bread", "vegetarian", "breakfast", 1.2))
print(recommend_recipe("salmon", "gluten-free", "lunch"))
```

```python

```

```python

```

# ChatBot

```python
from langchain_core.messages import HumanMessage, AIMessage

llm.invoke([HumanMessage("Hi! I'm Michael")])
```

```python
llm.invoke([HumanMessage("What's my Name?")])

```

```python
llm.invoke(
    [
        HumanMessage("Hi! I'm Michael"),
        AIMessage("Nice to meet you, Michael. Is there something I can help you with or would you like to chat?"),
        HumanMessage("What's my Name?")
    ]
)
```

```python
from langchain_core.chat_history import InMemoryChatMessageHistory

msg_store = InMemoryChatMessageHistory()    # memory object
```

```python
from langchain_core.runnables.history import RunnableWithMessageHistory
```

```python
def get_session_history(session_id):
  if session_id == "mike":
    return mike_store
  elif session_id == "jack":
    return jack_store
```

```python
with_message_history = RunnableWithMessageHistory(
    # The underlying runnable
    llm,
    # A function that takes in a session id and returns a memory object
    get_session_history,

)
```

```python
config = {                # anything that llm chain expects, other than input
    "configurable":{
        "session_id": "bob"
    }
}

with_message_history.invoke(
    [HumanMessage("Who am I?")],
    config=config
  ) #Run1
```

```python
msg_store.messages
```

```python
with_message_history.invoke([HumanMessage("What's My Name?")]) #Run1
```

```python
msg_store.messages
```

```python

```

# Minimal ChatBot

```python
from langchain_groq import ChatGroq
from langchain_core.chat_history import InMemoryChatMessageHistory


llm = ChatGroq(model="llama-3.1-8b-instant", groq_api_key="[credential redacted]")
llm = llm | parser


msg_store = InMemoryChatMessageHistory()    # memory object

def get_session_history():
  return msg_store

llm_with_message_history = RunnableWithMessageHistory(llm,  get_session_history)
```

```python
def chat(human):
  return llm_with_message_history.invoke(
    [HumanMessage(human)],
  )
```

```python
while True:
  msg = input("Human > ")
  print("AI    > ", chat(msg))
```

```python

```

## Notebook conversion

Markdown and code cells are preserved. Execution outputs, widgets, and runtime state remain in the external notebook; no notebook code was executed.

## Source provenance

- [Original IPYNB](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/Lectures/AI/LangChain_II.ipynb) · CODING RESOURCES/Lectures/AI/LangChain_II.ipynb

Original files remain unchanged outside the vault. Imported code is a reference, not tested or certified.
