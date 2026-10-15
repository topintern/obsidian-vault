---
resume_title: "Python - Software Engineer AI Systems - TestSprite Senior AI Engineer - AI System Design & Implement"
kind: "resume-bank-entry"
resume_kind: "Supporting material"
resume_owner: "Unconfirmed"
resume_family: "Python"
resume_families: ["Python"]
resume_role: "Software Engineer AI Systems"
resume_company: ""
resume_context: "Python LangGraph OpenAI API RAG Pinecone FastAPI / 6 YOE / Software Engineer AI Systems / TestSprite Senior AI Engineer"
resume_experience_labels: ["6 YOE"]
resume_source_modified: "2026-04-21"
resume_review: "unreviewed"
resume_favorite: false
resume_pdf: []
resume_word: []
source_paths: ["D:\\HDD F\\downloads\\CV\\Resumes\\Python\\Python LangGraph OpenAI API RAG Pinecone FastAPI\\6 YOE\\Software Engineer AI Systems\\TestSprite Senior AI Engineer\\AI System Design & Implementation A.txt"]
source_sha256: ["0448540429367a0ff73d90f38a7183d1503687e16b61d0c6ed230c1f16cfb9a3"]
imported: "2026-10-14"
tags: ["career/resumes"]
---

# Python - Software Engineer AI Systems - TestSprite Senior AI Engineer - AI System Design & Implement

[[Resume Bank]] · [[Resume Catalogue.base]] · [[Tailoring Desk]]

> [!info] Imported source version
> Content and experience labels are preserved, not independently verified. No master resume or submission approval has been assigned.

> [!warning] Identity or source context needs review
> This item is labelled **Unconfirmed** and is separated from the default Neel resume view. Do not reuse another person's or an example's career claims.

## Original files

No PDF or Word document accompanies this source. The external source is preserved below; no upload-ready document was generated.

## Readable content

AI System Design & Implementation: Agentic Web Automation Framework
Overview and Purpose
I designed and built an Agentic AI System at Epik Solutions to automate the extraction and analysis of competitor product data. The primary goal was to move beyond brittle, selector-based scraping scripts to a system that could navigate dynamic web applications autonomously. This mattered because manual market analysis was lagging behind real-time pricing shifts; by automating this, we achieved a 15% increase in market share through rapid strategic pricing adjustments.

Technical Responsibility
I was the Lead Engineer for this project. I architected the end-to-end flow, from the orchestration layer to the headless browser deployment. My responsibilities included:

Designing the LangGraph state machines to manage multi-step navigation logic.

Implementing the Playwright integration within AWS Lambda.

Developing custom prompt engineering strategies to interpret DOM elements and handle navigation errors.

Tool Selection: Build vs. Buy
Existing Tools (LangGraph & Playwright): I chose LangGraph for orchestration because its cyclic graph capabilities are superior to linear chains for "self-healing" workflows—if an agent hits a popup or unexpected UI change, it can loop back and re-plan. I used Playwright for the browser layer due to its robust "auto-wait" features and superior TypeScript support compared to Selenium.

Built from Scratch (Context Reduction Layer): I built a custom HTML/DOM Minifier. Passing raw HTML to an LLM is token-expensive and introduces noise. I developed a utility to strip non-interactive elements and minify the DOM into a "semantic map" that focused only on buttons, inputs, and text content, which reduced token usage by 60% and improved reasoning accuracy.

Tradeoffs and Hindsight
Tradeoff (Latency vs. Accuracy): I initially used GPT-4 for every navigation step to ensure high accuracy. However, this was slow and costly. I eventually moved to a "router" model: using a faster, smaller model (GPT-3.5/4o-mini) to identify simple elements and only "escalating" to a larger model when the agent signaled it was "stuck" or encountered a complex data table.

Hindsight: If I were to rebuild this today, I would implement a Vector-based UI Discovery system. Instead of re-parsing the page every time, I would store successful "navigation paths" in a vector database to allow the agent to "remember" how to reach specific data points, only falling back to full LLM reasoning when the site structure changes significantly.

## Source provenance

Source modification date is filesystem metadata, not a verified authorship date. This is a one-time import snapshot; later external edits are not automatically synced.

- [Python / Python LangGraph OpenAI API RAG Pinecone FastAPI / 6 YOE / Software Engineer AI Systems / TestSprite Senior AI Engineer / AI System Design & Implementation A.txt](file:///D:/HDD%20F/downloads/CV/Resumes/Python/Python%20LangGraph%20OpenAI%20API%20RAG%20Pinecone%20FastAPI/6%20YOE/Software%20Engineer%20AI%20Systems/TestSprite%20Senior%20AI%20Engineer/AI%20System%20Design%20%26%20Implementation%20A.txt)

For claim checks, consult [[Claims to Reconcile]] and supporting experience evidence before tailoring.
