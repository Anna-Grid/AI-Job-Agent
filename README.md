# 🤖 AI-Job-Agent: Autonomous Career Assistant
![Status](https://img.shields.io/badge/status-active-success)
![Dockerized](https://img.shields.io/badge/docker-ready-blue)
![License](https://img.shields.io/badge/license-MIT-lightgrey)

#### 🛠 Tech Stack

![Python](https://img.shields.io/badge/Python-3.11-blue?logo=python&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-Data_Analysis-150458?logo=pandas&logoColor=white)
![SQL](https://img.shields.io/badge/SQL-Data_Modeling-orange?logo=postgresql&logoColor=white)

![Docker](https://img.shields.io/badge/Docker-Containerization-2496ED?logo=docker&logoColor=white)
![Linux](https://img.shields.io/badge/Linux-Bash_%7C_Cron-E34F26?logo=linux&logoColor=white)

![OpenAI](https://img.shields.io/badge/OpenAI-LLM_Integration-412991?logo=openai&logoColor=white)
![NLP](https://img.shields.io/badge/NLP-Text_Processing-yellow)

![Google Sheets](https://img.shields.io/badge/Google_Sheets-API_Integration-34A853?logo=googlesheets&logoColor=white)
![ETL](https://img.shields.io/badge/Data-ETL_Pipeline-success)
![Jinja2](https://img.shields.io/badge/Jinja2-Templating-B41717)

An intelligent ETL pipeline and AI agent designed to automate the job search process. The system parses vacancies from multiple platforms, scores them based on candidate profile relevance, and generates tailored application materials using LLMs.

## 🚀 Overview

This project was built to streamline the job hunting process for Data Engineering roles. It transforms a manual search into a fully automated, containerized workflow.

### Key Features:
- **Multi-Source Scraper**: Aggregates job listings via REST APIs and RSS feeds (RemoteOK, BerlinStartupJobs, WeWorkRemotely).
- **LLM-Powered Scoring**: Uses OpenAI `gpt-4o-mini` to analyze job descriptions and assign a relevance score (0–10).
- **Dynamic Content Generation**: Automatically generates tailored CVs (Markdown) and cover letters (text) in either **English or German**, depending on job requirements.
- **Persistent Data Tracking**: Syncs application history to a local CSV datastore and a live **Google Sheets** dashboard via the Google Sheets API.
- **Smart Caching**: Implements a local JSON-based cache to minimize API costs and prevent redundant processing.
- **Production-Ready**: Fully containerized with Docker and designed to run as a scheduled `cron` job on a remote server.
- **Observability**: Structured logging for tracking pipeline execution and debugging.

## 🛠️ Tech Stack
- **Language**: Python 3.11
- **AI**: OpenAI API (`gpt-4o-mini`)
- **Automation**: Docker, Cron
- **Data**: Google Sheets API, Jinja2 (templating), BeautifulSoup4, Pandas
- **DevOps**: Linux (Ubuntu Server), Docker volumes

## 🏗️ Architecture Detail

### 1. Orchestration (`main.py`)
Coordinates the full pipeline: parsing → scoring → generation → persistence.  
Applies a threshold filter so that only high-relevance vacancies (>7/10) trigger the expensive LLM generation phase.

### 2. AI Generator with Language Detection
The agent dynamically detects whether a job requires German (e.g., C1/native indicators) and adjusts the output language accordingly.  
Uses structured JSON responses to reliably populate CV and cover letter templates.

### 3. Google Sheets Integration
Acts as a lightweight "data lake" for tracking applications.  
Each processed job is appended to a spreadsheet, enabling real-time monitoring of the pipeline.
