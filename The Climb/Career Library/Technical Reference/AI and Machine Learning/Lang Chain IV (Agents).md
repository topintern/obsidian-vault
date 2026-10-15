---
kind: "study-reference"
title: "Lang Chain IV (Agents)"
collection: "AI and Machine Learning"
topic: "AI and Machine Learning"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/Lectures/AI/LangChain_IV_(Agents).ipynb"]
tags: ["career/library"]
source_status: "source-reference"
---

# Lang Chain IV (Agents)

[[The Climb/Career Library/Career Library]]

```python
!pip install -qqqU langchain langchain-openai langchain-community langgraph
```

```python
import os
os.environ["LANGCHAIN_TRACING_V2"]="true"
os.environ["LANGCHAIN_ENDPOINT"]="https://api.smith.langchain.com"
os.environ["LANGCHAIN_API_KEY"]="lsv2_pt_ff68d77a1f28476f96aasdasda920bc33"
os.environ["LANGCHAIN_PROJECT"]="lc-4"
```

```python
import getpass
api_key = getpass.getpass("OpenAI Key:")
```

```python
from langchain_openai import ChatOpenAI

llm = ChatOpenAI(
    model="gpt-4o-mini",
    api_key=api_key
)
```

```python
llm.invoke("Tell me a big story about World War 2")
```

# Streaming

```python
for chunk in llm.stream("Tell me a big story about World War 2"):
  print(chunk.content, end="|", flush=True)
```

# Agent

```python
import os
os.environ["TAVILY_API_KEY"] = getpass.getpass("Tavily API:")
```

```python
from langchain_community.tools import TavilySearchResults

search = TavilySearchResults(max_results=5)  # google search alternativex
```

```python
search.invoke("Who won gold in javelin throw in recent olympics")
```

```python
tools = [search]
```

## Tool Calling

```python
llm_with_tools = llm.bind_tools(tools)
```

```python
res = llm_with_tools.invoke("Search in the internet. Who created history by becoming the first Indian to win an athletics gold medal at the Olympics by winning the men's javelin throw at Tokyo 2020?")
print("Content:",res.content)
print("Tool Calls:", res.tool_calls)
```

## Agent Creation

```python
from langgraph.prebuilt import create_react_agent  #ReAcT is a prompting technique that we will see in further sessions

agent_executor = create_react_agent(llm, tools)
```

```python
agent_executor.invoke({"messages": "Hi"})
```

```python
res = agent_executor.invoke({"messages": "What's the weather in Delhi?"})

```

```python
res["messages"][0]
```

```python
res["messages"][1]
```

```python
res["messages"][2]
```

```python
print(res["messages"][3].content)

```

The current weather in Delhi is as follows:

- **Temperature**: 29.4°C (feels like 31.6°C)
- **Condition**: Mist
- **Humidity**: 89%
- **Wind**: 6.1 kph from the West-Southwest
- **Visibility**: 4 km

The temperature is expected to vary today with a maximum of approximately 35.96°C and a minimum of around 26.05°C.

For more details, you can check the [Hindustan Times](https://www.hindustantimes.com/cities/delhi-news/delhi-weather-today-aqi-and-rain-forecast-updates-august-30-2024-101724981404005.html) or [WeatherAPI](https://www.weatherapi.com/).

```python
for chunk in agent_executor.stream({"messages": "What's the weather in Delhi?"}):
  print(chunk)
  print("-------")
```

# Memory

```python
res = agent_executor.invoke({"messages": "What's the weather in Delhi?"})
print(res["messages"][-1].content)
```

```python
res = agent_executor.invoke({"messages": "Is it likely to rain there today?"}) # Lack of Memory
print(res["messages"][-1].content)
```

```python
from langgraph.checkpoint.memory import MemorySaver

memory = MemorySaver()
```

```python
agent_executor_with_memory = create_react_agent(llm, tools, checkpointer=memory)
```

```python
config = {"configurable":{"thread_id": "mike"}}
```

```python
for chunk in agent_executor_with_memory.stream({"messages": "What's the weather in Delhi?"}, config):
  print(chunk)
  print("-------")
```

```python
for chunk in agent_executor_with_memory.stream({"messages": "Is it likely to rain there today?"}, config):
  print(chunk)
  print("-------")
```

```python

```

# Agentic ChatBot With Search Capabilities

```python

```

```python
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
while True:
  msg = input("Human > ")
  res = agent_executor_with_memory.invoke({"messages": msg}, config)
  print("AI    > ", res["messages"][-1].content)
```

```python

```

## Notebook conversion

Markdown and code cells are preserved. Execution outputs, widgets, and runtime state remain in the external notebook; no notebook code was executed.

## Source provenance

- [Original IPYNB](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/Lectures/AI/LangChain_IV_(Agents).ipynb) · CODING RESOURCES/Lectures/AI/LangChain_IV_(Agents).ipynb

Original files remain unchanged outside the vault. Imported code is a reference, not tested or certified.
