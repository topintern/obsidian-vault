---
kind: "study-reference"
title: "More Gen AIFrameworks"
collection: "AI and Machine Learning"
topic: "AI and Machine Learning"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/Lectures/AI/MoreGenAIFrameworks.ipynb"]
tags: ["career/library"]
source_status: "source-reference"
---

# More Gen AIFrameworks

[[The Climb/Career Library/Career Library]]

# Transformers

```python
!pip install -qqq transformers datasets evaluate accelerate
```

```python
%pip install -qq gradio
```

```python
from transformers import pipeline
```

## Text Classification

```python
classifier = pipeline("sentiment-analysis")
```

```python
classifier("Happy Christmas")[0]['label']
```

```python

twt_classifier = pipeline("sentiment-analysis", model="cardiffnlp/twitter-roberta-base-sentiment-latest")

```

```python
twt_classifier(["Sun rises in the east", "Sun sets in the west"])
```

## Image Classification

```python
img_classifier = pipeline(model="google/vit-base-patch16-224")
```

```python
img_classifier(images="https://www.argospetinsurance.co.uk/assets/uploads/2017/12/cat-pet-animal-domestic-104827.jpeg")
```

## Zero Shot Text Classification

```python
zs_clf = pipeline(model="facebook/bart-large-mnli")
```

## VQA

!sudo apt install -y tesseract-ocr
!pip install pytesseract

```python
!sudo apt install -y tesseract-ocr
!pip  install -qqq pytesseract
```

```python
from transformers import pipeline

vqa = pipeline(model="impira/layoutlm-document-qa")
output = vqa(
    image="https://huggingface.co/spaces/impira/docquery/resolve/2359223c1837a7587402bda0f2643382a6eefeab/invoice.png",
    question="What is the invoice number?",
)
# output[0]["score"] = round(output[0]["score"], 3)
output
```

```
# How to use transformers pipeline as a tool in langchain

# @tool
# def img_classifier(img):
#     return img_classifier(img)

# llm.bind_tools([img_classifier])
```

```python
import gradio as gr
gr.Interface.from_pipeline(zs_clf).launch(debug=True)
```

# CrewAI

```python
!pip install 'crewai[tools]'
```

```python
import os
import getpass
os.environ["OPENAI_API_KEY"] = getpass.getpass("OpenAI:")
os.environ["SERPER_API_KEY"] = getpass.getpass("Serper:")
```

```python
import os
from crewai import Agent, Task, Crew, Process
from crewai_tools import SerperDevTool



search_tool = SerperDevTool()

# Define your agents with roles and goals
researcher = Agent(
  role='Senior Research Analyst',
  goal='Uncover cutting-edge developments in AI and data science',
  backstory="""You work at a leading tech think tank.
  Your expertise lies in identifying emerging trends.
  You have a knack for dissecting complex data and presenting actionable insights.""",
  verbose=True,
  allow_delegation=False,
  # You can pass an optional llm attribute specifying what model you wanna use.
  # llm=ChatOpenAI(model_name="gpt-3.5", temperature=0.7),
  tools=[search_tool]
)
writer = Agent(
  role='Tech Content Strategist',
  goal='Craft compelling content on tech advancements',
  backstory="""You are a renowned Content Strategist, known for your insightful and engaging articles.
  You transform complex concepts into compelling narratives.""",
  verbose=True,
  allow_delegation=True
)

# Create tasks for your agents
task1 = Task(
  description="""Conduct a comprehensive analysis of the latest advancements in AI in 2024.
  Identify key trends, breakthrough technologies, and potential industry impacts.""",
  expected_output="Full analysis report in bullet points",
  agent=researcher
)

task2 = Task(
  description="""Using the insights provided, develop an engaging blog
  post that highlights the most significant AI advancements.
  Your post should be informative yet accessible, catering to a tech-savvy audience.
  Make it sound cool, avoid complex words so it doesn't sound like AI.""",
  expected_output="Full blog post of at least 4 paragraphs",
  agent=writer
)

# Instantiate your crew with a sequential process
crew = Crew(
  agents=[researcher, writer],
  tasks=[task1, task2],
  verbose=True,
  process = Process.sequential
)

# Get your crew to work!
result = crew.kickoff()

print("######################")
print(result)
```

# Llama Index

```python
%pip install llama-index
```

```python
from llama_index.llms.openai import OpenAI
```

```python
llm = OpenAI(model="gpt-4o-mini", temperature=0.1)
```

```python
!wget https://github.com/lerocha/chinook-database/raw/master/ChinookDatabase/DataSources/Chinook_Sqlite.sqlite
```

```python
from sqlalchemy import create_engine

engine = create_engine("sqlite:///Chinook_Sqlite.sqlite")
```

```python
from sqlalchemy import text
with engine.connect() as conn:
    print(conn.execute(text("SELECT * FROM album")).fetchall())
```

```python
from llama_index.core import SQLDatabase

sql_database = SQLDatabase(engine)
```

```python
from llama_index.core.query_engine import NLSQLTableQueryEngine

query_engine = NLSQLTableQueryEngine(
    sql_database=sql_database, llm=llm
)

```

```python
response = query_engine.query("List albums of 'AC/DC'")
```

```python
response.response
```



```python
list(response.metadata.values())[1]
```

```python
llm = OpenAI(model="gpt-4o-mini", temperature=0.1)

engine = create_engine("sqlite:///Chinook_Sqlite.sqlite") #sqlalchemy
sql_database = SQLDatabase(engine) # llamaindex's toolkit

query_engine = NLSQLTableQueryEngine(
    sql_database=sql_database, llm=llm
)

response = query_engine.query("List albums of 'AC/DC'")
print(f"Query: {list(response.metadata.values())[1]}\n Answer:{response.response}")
```

## Notebook conversion

Markdown and code cells are preserved. Execution outputs, widgets, and runtime state remain in the external notebook; no notebook code was executed.

## Source provenance

- [Original IPYNB](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/Lectures/AI/MoreGenAIFrameworks.ipynb) · CODING RESOURCES/Lectures/AI/MoreGenAIFrameworks.ipynb

Original files remain unchanged outside the vault. Imported code is a reference, not tested or certified.
