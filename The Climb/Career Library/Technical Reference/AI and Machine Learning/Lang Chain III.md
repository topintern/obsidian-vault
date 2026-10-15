---
kind: "study-reference"
title: "Lang Chain III"
collection: "AI and Machine Learning"
topic: "AI and Machine Learning"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/Lectures/AI/LangChain_III.ipynb"]
tags: ["career/library"]
source_status: "source-reference"
---

# Lang Chain III

[[The Climb/Career Library/Career Library]]

```python
!pip install langchain langchain-openai
```

```python
import os
os.environ["LANGCHAIN_TRACING_V2"]="true"
os.environ["LANGCHAIN_ENDPOINT"]="https://api.smith.langchain.com"
os.environ["LANGCHAIN_API_KEY"]="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"
os.environ["LANGCHAIN_PROJECT"]="chatbot-genai"
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

```

# InMemoryChatMessageHistory

```python
from langchain_core.chat_history import InMemoryChatMessageHistory

msg_store = InMemoryChatMessageHistory()
```

```python
msg_store
```

```python
msg_store.add_user_message("Hey")
```

```python
from langchain_core.messages import HumanMessage, AIMessage

msg_store.add_message(AIMessage("Hello"))
```

```python

```

# Structured Output

```python
from langchain_core.output_parsers import StrOutputParser

parser = StrOutputParser()
chain = llm | parser
```

```python
print(chain.invoke("Tell Me a Joke about cars, divide the output into setup, punchline and rating (1-10)"))
```

```python
print(chain.invoke("Tell Me a Joke about cars, divide the output into setup, punchline and rating (1-10). give output in xml tags"))
```

```python
print(chain.invoke("Tell Me a Joke about cats, divide the output into setup, punchline and rating (1-10) give output in json"))

```

```python
from langchain_core.pydantic_v1 import BaseModel, Field

class Joke(BaseModel): #defining a structure
  setup: str = Field(description="The setup of the joke")
  punchline: str = Field(description="The punchline to the joke")
  rating: int = Field(description="How funny the joke is (1-10)")
```

```python
cat_joke = Joke(setup="Why was the cat sitting on the computer?", punchline= "Because it wanted to keep an eye on the mouse!", rating =7) # I wish LLM could give me this
cat_joke
```

```python
cat_joke.rating
```

```python
# chain -> raw text -/-> parse get the required fields
# chain -> json/xml (may / maynot parse it all the time)

# chain -> Joke (pydantic object)
```

```python
structured_llm = llm.with_structured_output(Joke)
```

```python
joke = structured_llm.invoke("Tell Me a Joke about cats")

joke
```

```python
joke.rating
```

```python
from typing import Optional
class MovieStory(BaseModel):
  oneliner: str = Field(description="One Liner of the Movie Story")
  title: str = Field(description="Title of the Movie Story")
  subtitle: str = Field(description="SubTitle of the Movie Story")
  genre: str = Field(description="Genre of the Movie")
  inspirations: list[str] = Field(description="List of Movie that this story got inspired from?")
  probability_of_antagonist_dying: Optional[float]  = Field(description="probability of antagonist dying (0-1), if > 0.5")
  duration_of_movie: str  = Field(description="time of movie")
```

```python
movie_llm = llm.with_structured_output(MovieStory)
```





```python
print(llm.invoke("Tell me the story of Interstellar. Do not give me spoilers about someone's death").content)
```

```python
interstellar.inspirations[0]
```

```python
interstellar
```

```python

```

# Tool Calling

```python
# def flights_to_europe(month):  # mocking (simulating) the flight ticketing servers
#   """Estimates the avg flight cost in USD for a given month. Ex:DEC, JAN, MAR"""
#   if month in ["DEC", "MAY"]:
#     return 1500
#   else:
#     return 1200

def hotel_in_europe(month):  # mocking (simulating) the flight ticketing servers
  """Estimates the avg Hotel cost in USD for a given month. Ex:DEC, JAN, MAR"""
  if month in ["DEC", "MAY"]:
    return 1800
  else:
    return 1500

def flight_prices(origin: str, destination: str, date:str):  # mocking (simulating) the flight ticketing servers
  """Call to get prices of flights from {source} to {destination} on {date}"""
  # Calls to SkyScanner API
  # curl equivalent
  return None

tools = [flight_prices, hotel_in_europe]
```

```python
# "What is the flight price to europe in December" -> llm -> go call flights_to_europe with "DEC"
```

```python
llm_with_tools = llm.bind_tools(tools) # bind_tools will let llm know that "tools" are available to call
```

```python
res = llm_with_tools.invoke("What is the flight price from Bombay to New York on Next Thanksgiving")
res
```

```python
res.tool_calls
```

```python
res = llm_with_tools.invoke("What is the hotel price in europe in the month of 11")
res.tool_calls
```

```python
res = llm_with_tools.invoke("What is the hotel and flight price in europe during christmas")
res.tool_calls
```

```python
# tool calling is the ability of calling the right tool with right args/parameters when exposed to multiple tool choices
```

```python

```

```python
res = llm_with_tools.invoke("What is the hotel price in america in the month of 11")
res.content
```

```python

```

## Notebook conversion

Markdown and code cells are preserved. Execution outputs, widgets, and runtime state remain in the external notebook; no notebook code was executed.

## Source provenance

- [Original IPYNB](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/Lectures/AI/LangChain_III.ipynb) · CODING RESOURCES/Lectures/AI/LangChain_III.ipynb

Original files remain unchanged outside the vault. Imported code is a reference, not tested or certified.
