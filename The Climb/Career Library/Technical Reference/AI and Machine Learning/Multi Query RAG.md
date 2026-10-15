---
kind: "study-reference"
title: "Multi Query RAG"
collection: "AI and Machine Learning"
topic: "AI and Machine Learning"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/Lectures/AI/MultiQuery_RAG.ipynb"]
tags: ["career/library"]
source_status: "source-reference"
---

# Multi Query RAG

[[The Climb/Career Library/Career Library]]

> Visualising the Chain

```python
!pip install langchain_community tiktoken langchain-openai langchainhub chromadb langchain beautifulsoup4 langchain_chroma grandalf
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

```python
from langchain_openai import OpenAIEmbeddings
from langchain_core.output_parsers import StrOutputParser
from langchain_openai import ChatOpenAI

llm = ChatOpenAI(model_name="gpt-4o-mini")
parser = StrOutputParser()
emb = OpenAIEmbeddings()
```

```python
from langchain.prompts import ChatPromptTemplate

# Multi Query: Different Perspectives
template = """You are an AI language model assistant. Your task is to generate four
different versions of the given user question to retrieve relevant documents from a vector
database. By generating multiple perspectives on the user question, your goal is to help
the user overcome some of the limitations of the distance-based similarity search.
Provide these alternative questions separated by newlines. Original question: {question}"""
prompt_perspectives = ChatPromptTemplate.from_template(template)
```

```python

```

```python
generate_queries_chain = prompt_perspectives | llm | parser
```

```python
queries = generate_queries_chain.invoke({"question":"What is task decomposition for LLM agents?"})
```

```python

filtered_queries = [q.strip() for q in queries.split("\n") if q.strip()]

```

```python
type(queries), type(filtered_queries)
```

generate_queries_chain = prompt_perspectives | llm | parser

The above chain gives output of str. But I need list of str

```python
def remove_empty_queries(queries: str) -> list[str]:
    return [q.strip() for q in queries.split("\n") if q.strip()]

def capitalize(queries: list[str]) -> list[str]:
    return [q.upper() for q in queries]
```

```python
generate_queries_list_chain = prompt_perspectives | llm | parser | remove_empty_queries # this is how, you add custom functions to the chain
```

```python
queries_list = generate_queries_list_chain.invoke({"question":"What is task decomposition for LLM agents?"})
```

```python
queries_list
```

```python
generate_queries_list_chain_cap = prompt_perspectives | llm | parser | remove_empty_queries | capitalize # this is how, you add custom functions to the chain
```

```python
queries_cap_list = generate_queries_list_chain_cap.invoke({"question":"What is task decomposition for LLM agents?"})
```

```python
queries_cap_list
```

```python
generate_queries_list_chain_cap.get_graph().print_ascii() #visualing the chain
```

```python
generate_queries = generate_queries_list_chain
```

```python
# Indexing
from langchain_chroma import Chroma
from langchain_community.document_loaders import WebBaseLoader

from langchain.text_splitter import RecursiveCharacterTextSplitter


vector_store = Chroma(
    collection_name="blog",
    embedding_function=emb,
    persist_directory="./chroma_langchain_db",  # Where to save data locally, remove if not neccesary
)

blog = "https://lilianweng.github.io/posts/2023-06-23-agent/"


loader = WebBaseLoader(blog)
blog_docs = loader.load()
text_splitter = RecursiveCharacterTextSplitter.from_tiktoken_encoder(
    chunk_size=300,
    chunk_overlap=50)

blog_chunks = text_splitter.split_documents(blog_docs)
vector_store.add_documents(documents=blog_chunks)
```

```python
retriever = vector_store.as_retriever(search_kwargs={"k": 3})
```

```python

```

```python
retrieval_chain = generate_queries | retriever.map()
```



```python
res = retrieval_chain.invoke({"question":"What is task decomposition for LLM agents?"})
```

```python
type(res), type(res[0]), type(res[0][0])
```

```python
len(res), len(res[0])
```

```python
# res = [
#     [D1, D2, D3], #given by retriver for Q1
#     [D5, D4, D3], #given by retriver for Q2
#     [D0, D2, D1], #...
#     [D0, D9, D2],
# ]

    # merged_docs = []
    # for doc_list in docs:
    #     merged_docs.extend(doc_list)


# res = [D1, D2, D3, D5, D4, D3, D0, D2, D1, D0, D9, D2]

# remove_duplicate_docs

# res = [D1, D2, D3, D4, D5, D0, D9]
```

```python
from langchain.load import dumps, loads

def remove_duplicate_docs(docs):
    hashable_docs = [dumps(doc) for doc in docs]
    unique_docs = list(set(hashable_docs))
    return [loads(doc) for doc in unique_docs]

# def merge_docs(docs: list[list[Document]]) -> list[Document]:
def merge_docs(docs):
    merged_docs = []
    for doc_list in docs:
        merged_docs.extend(doc_list)
    return merged_docs


```

```python
list(set(["D1", "D2", "D1", "D3"]))
```

```python
merge_res = merge_docs(res)
```

```python
len(merge_res)
```

```python
merge_res[0]
```

```python
retrieval_chain_w_merge = generate_queries | retriever.map() | merge_docs | remove_duplicate_docs
```

```python
all_queries_docs = retrieval_chain_w_merge.invoke({"question":"What is task decomposition for LLM agents?"})
```

```python
len(all_queries_docs), all_queries_docs[0]
```

```python
d1 = all_queries_docs[0]
d2 = all_queries_docs[1]
```

```python
type(d1)
set([d1,d2])
```

```python
dumped_d1 = dumps(d1)
dumped_d1
```

```python
loaded_d1 = loads(dumped_d1)
loaded_d1
```

```python
retrieval_chain = retrieval_chain_w_merge
```

```python
retrieval_chain.get_graph().print_ascii()
```

```python
from operator import itemgetter
template = """Answer the following question based on this context:

{context}

Question: {question}
"""

prompt = ChatPromptTemplate.from_template(template)


rag_chain = (
    # {"context":retrieval_chain, "question":RunnablePassthrough()}
    {"context":retrieval_chain, "question":itemgetter("question")}
    | prompt
    | llm
    | parser
)
```

```python
rag_chain.invoke({"question":"What is task decomposition for LLM agents?"})
```

```python
rag_chain.get_graph().print_ascii()
```

```python

```

## Notebook conversion

Markdown and code cells are preserved. Execution outputs, widgets, and runtime state remain in the external notebook; no notebook code was executed.

## Source provenance

- [Original IPYNB](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/Lectures/AI/MultiQuery_RAG.ipynb) · CODING RESOURCES/Lectures/AI/MultiQuery_RAG.ipynb

Original files remain unchanged outside the vault. Imported code is a reference, not tested or certified.
