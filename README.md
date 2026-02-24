# rag-dbms-qaa-sys
RAG-Based DBMS Question Answering System
Overview
This project implements a Retrieval-Augmented Generation (RAG) system for answering DBMS conceptual questions using PDF-based course materials.

Requirements
Python 3.9+
Jupyter Notebook
google-generativeai (Gemini API) / OpenAI API
PyPDF2 or pdfplumber
Installation
!pip install langchain chromadb pypdf sentence-transformers python-dotenv google-generativeai !pip install -U langchain langchain-community langchain-core langchain-text-splitters chromadb !pip install -U langchain-huggingface

Create .env file
GEMINI_API_KEY=Your_API_Key_Here
