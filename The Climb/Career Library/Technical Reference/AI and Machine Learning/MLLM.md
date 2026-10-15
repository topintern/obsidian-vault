---
kind: "study-reference"
title: "MLLM"
collection: "AI and Machine Learning"
topic: "AI and Machine Learning"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/Lectures/AI/MLLM.ipynb"]
tags: ["career/library"]
source_status: "source-reference"
---

# MLLM

[[The Climb/Career Library/Career Library]]

```python
%pip install langchain langchain-openai
```

```python
url = "https://upload.wikimedia.org/wikipedia/commons/thumb/0/06/Startrails_above_Gunung_Bromo_-_Indonesia.jpg/586px-Startrails_above_Gunung_Bromo_-_Indonesia.jpg"
```

```python
import os
import getpass
os.environ["OPENAI_API_KEY"] = getpass.getpass("OPENAI_API_KEY:")
```

```python
from langchain_openai import ChatOpenAI

llm = ChatOpenAI(model_name="gpt-4o-mini")
```

## Pass image through url; It is supported only by limited models

```python
from langchain_core.messages import HumanMessage

```

```python
message = HumanMessage(
    content = [
        {
            "type": "image_url",
            "image_url": {
                "url": url
            }
        },
        {"type": "text", "text": "Describe the image in one sentence"}
    ]
)
```

```python
response = llm.invoke([message])
```

```python
print(response)
```

# Pass image as byte string

```python
import base64
import httpx
```

```python
def get_img_str(url):
    response = httpx.get(url)
    return base64.b64encode(response.content).decode("utf-8")
```

```python

```

```python
vol_image_str = get_img_str(url)
tor_image_str = get_img_str("https://upload.wikimedia.org/wikipedia/commons/1/1a/Dszpics1.jpg")
```

```python
message = HumanMessage(
    content = [
        {
            "type": "image_url",
            "image_url": {
                "url": f"data:image/jpeg;base64,{vol_image_str}",
            }
        },
         {
            "type": "image_url",
            "image_url": {
                "url": f"data:image/jpeg;base64,{tor_image_str}",
            }
        },
        {"type": "text", "text": "Describe the images in one sentence each"}
    ]
)
```

```python
response = llm.invoke([message])

```

```python
print(response)
```

```python
print(response.content)

```

```python
# inputs: img, medical_history (allergy)
# outputs: text explaining the edibility    # exp - 1
# outputs: is_allergetic, severity, ingredients, explanation  # exp - 2
```

# Real World Application

```python

import base64
import io
import gradio as gr
from langchain_core.messages import SystemMessage, HumanMessage
from langchain_openai import ChatOpenAI
from langchain_core.pydantic_v1 import BaseModel, Field

# from key import OPENAI_KEY

class AllergyReport(BaseModel):
    is_allergic:bool = Field(description="Is Allergic?")
    severity:int = Field(description="Allergy Severity (1-10)")
    ingredients: list[str] = Field(description="List of Allergic Ingredients, if Any")
    explanation: str = Field(description="Explanation of Allergies")


llm = ChatOpenAI(
    model="gpt-4o-mini",
    api_key=OPENAI_KEY
).with_structured_output(AllergyReport)


def process_img(image):
    buffered = io.BytesIO()
    image.save(buffered, format="JPEG")
    img_str = base64.b64encode(buffered.getvalue()).decode("utf-8")
    return img_str

def allergy_predictor(image, medical_history):
    img_str = process_img(image)
    messages = [
        SystemMessage(
            content="You are a helpful AI assistant that can identify potential food allergies based on an image of food ingredients and a user's medical history."
        ),
        HumanMessage(
            content=[
                {"type": "text", "text": f"Medical History: {medical_history}"},
                {"type": "image_url", "image_url": {"url": f"data:image/jpeg;base64,{img_str}"}}
            ]
        )
    ]
    res:AllergyReport = llm.invoke(messages)
    ingredients = [(i,) for i in res.ingredients]
    return res.is_allergic, res.severity, ingredients, res.explanation

demo = gr.Interface(
    fn=allergy_predictor,
    inputs=[
        gr.Image(type="pil", label="Food Ingredients"),
        gr.Textbox(label="Medical History of Allergies"),
    ],
    outputs=[
        gr.Checkbox(label="Is Allergic?"),
        gr.Slider(label="Severity", minimum=1, maximum=10),
        gr.List(label="", headers=["Ingredients"]),
        gr.TextArea(label="Explanation"),
    ],
    title="Safe Diet"
)

demo.launch()
```

## Notebook conversion

Markdown and code cells are preserved. Execution outputs, widgets, and runtime state remain in the external notebook; no notebook code was executed.

## Source provenance

- [Original IPYNB](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/Lectures/AI/MLLM.ipynb) · CODING RESOURCES/Lectures/AI/MLLM.ipynb

Original files remain unchanged outside the vault. Imported code is a reference, not tested or certified.
