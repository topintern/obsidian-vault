---
kind: "study-reference"
title: "RAG I"
collection: "AI and Machine Learning"
topic: "AI and Machine Learning"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/Lectures/AI/RAG_I.ipynb"]
tags: ["career/library"]
source_status: "source-reference"
---

# RAG I

[[The Climb/Career Library/Career Library]]

```python
!pip install langchain_community tiktoken langchain-openai langchainhub chromadb langchain beautifulsoup4 langchain_chroma
```

```python
import os
os.environ['LANGCHAIN_TRACING_V2'] = 'true'
os.environ['LANGCHAIN_ENDPOINT'] = 'https://api.smith.langchain.com'
os.environ['LANGCHAIN_API_KEY'] = "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"
os.environ["LANGCHAIN_PROJECT"]="rag"
```

```python
import getpass
os.environ['OPENAI_API_KEY'] = getpass.getpass("OPENAI_API_KEY:")
```

# Cosine Similarity

```python
question = "What kind of pets do I like?"

doc1 = "My favorite pet is a cat"
doc2 = "I drove all night"
docs = [doc1, doc2]
```

```python
from langchain_openai import OpenAIEmbeddings

emb = OpenAIEmbeddings()
```

```python
question_vector = emb.embed_query(question)
```

```python
doc1_vector = emb.embed_query(doc1)
doc2_vector = emb.embed_query(doc2)

```

```python
len(doc2_vector)
```

```python
import numpy as np

def cosine_similarity(vec1, vec2):
    dot_product = np.dot(vec1, vec2)
    norm_vec1 = np.linalg.norm(vec1)
    norm_vec2 = np.linalg.norm(vec2)
    return dot_product / (norm_vec1 * norm_vec2)
```

```python
cosine_similarity(question_vector, doc1_vector) #high
```

```python
cosine_similarity(question_vector, doc2_vector) #low
```

```python
cosine_similarity(question_vector, emb.embed_query("What sort of animals do I love?")) #higher
```

# Indexing

```python
blog = "https://lilianweng.github.io/posts/2023-06-23-agent/"

from langchain_community.document_loaders import WebBaseLoader

loader = WebBaseLoader(blog)
```

```python
blog_docs = loader.load()
```

```python
blog_docs[0]
```

```python
# big blog -> chunks
from langchain.text_splitter import RecursiveCharacterTextSplitter
text_splitter = RecursiveCharacterTextSplitter.from_tiktoken_encoder(
    chunk_size=300,
    chunk_overlap=50)
```

```python
blog_chunks = text_splitter.split_documents(blog_docs)
```

```python
# VecDB

from langchain_chroma import Chroma

vector_store = Chroma(
    collection_name="blog",
    embedding_function=emb,
    persist_directory="./chroma_langchain_db",  # Where to save data locally, remove if not neccesary
)
```

```python
vector_store.add_documents(documents=blog_chunks)
```

# Retriever

```python
# retriever = vector_store.as_retriever(search_type="similarity_score_threshold", search_kwargs={"score_threshold": 0.5})
retriever = vector_store.as_retriever(search_kwargs={"k": 5})
```

```python
docs = retriever.get_relevant_documents("What is Task Decomposition?")
```

```python
len(docs)
```

```python

```

# Generation

```python
# from langchain_openai import ChatOpenAI
# from langchain.prompts import ChatPromptTemplate

# template = """Answer the question based on the following context:
# <context>
# {context}
# </context>

# Question: {question}
# """

# prompt = ChatPromptTemplate.from_template(template)
# prompt
```

```python
# set the LANGCHAIN_API_KEY environment variable (create key in settings)
from langchain import hub
prompt = hub.pull("rlm/rag-prompt")
```

```python
prompt
```

```python
from langchain_core.output_parsers import StrOutputParser
from langchain_openai import ChatOpenAI

llm = ChatOpenAI(model_name="gpt-4o-mini")
parser = StrOutputParser()
```

```python
from langchain_core.runnables import RunnablePassthrough

rag_chain = (
    {"context":retriever, "question":RunnablePassthrough()}
    | prompt
    | llm
    | parser
)
```

```python
rag_chain.invoke("what is task decomposition?")
```

```python

```

## Notebook conversion

Markdown and code cells are preserved. Execution outputs, widgets, and runtime state remain in the external notebook; no notebook code was executed.

## Source provenance

- [Original IPYNB](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/Lectures/AI/RAG_I.ipynb) · CODING RESOURCES/Lectures/AI/RAG_I.ipynb

Original files remain unchanged outside the vault. Imported code is a reference, not tested or certified.
