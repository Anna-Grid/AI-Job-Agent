# 🤖 AI-Job-Agent: Autonomous Career Assistant

An intelligent ETL pipeline and AI agent designed to automate the job search process. The system parses vacancies from multiple platforms, scores them based on candidate profile relevance, and generates tailored application materials using LLMs.

## 🚀 Overview

This project was born out of a need to streamline the job hunting process for Data Engineering roles. It transforms a manual search into a fully automated, containerized workflow.

### Key Features:
- **Multi-Source Scraper**: Aggregates job listings via REST APIs and RSS feeds (RemoteOK, BerlinStartupJobs, WeWorkRemotely).
- **LLM-Powered Scoring**: Uses OpenAI `gpt-4o-mini` to analyze job descriptions and assign a relevance score (0-10).
- **Dynamic Content Generation**: Automatically generates tailored CVs (Markdown) and Cover Letters (Text) in either **English or German**, depending on the job requirements.
- **Persistent Data Tracking**: Syncs application history to a local CSV database and a live **Google Sheets** dashboard via Google Sheets API.
- **Smart Caching**: Implements a local JSON cache to minimize API costs and prevent redundant processing.
- **Production Ready**: Fully dockerized and designed to run as a scheduled `cron` job on a remote server.

## 🛠️ Tech Stack
- **Language**: Python 3.11
- **AI**: OpenAI API (GPT-4o-mini)
- **Automation**: Docker, Cron
- **Data**: Google Sheets API, Jinja2 (Templating), BeautifulSoup4, Pandas
- **DevOps**: Linux (Ubuntu Server), Docker Volumes

## 🏗️ Architecture Detail

### 1. Orchestration (`main.py`)
Coordinates the flow from parsing to data logging. It ensures that only high-score vacancies (>7/10) trigger the expensive generation phase.

### 2. AI Generator with Language Detection
The agent dynamically detects if a job requires German (C1/Native markers) and adjusts the output language accordingly. It uses a structured JSON-mode response to populate document templates.

### 3. Google Sheets Integration
Acts as a "Data Lake" for tracking. Every successful generation is appended to a spreadsheet for real-time monitoring of the search progress.

## 📦 How to Run

1. **Clone and Configure**:
   ```bash
   git clone <your-repo-link>
   # Add your .env and google_credentials.json
