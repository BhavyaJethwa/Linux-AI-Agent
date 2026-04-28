# Linux AI Agent

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Python](https://img.shields.io/badge/Python-3.10%2B-blue.svg)](https://www.python.org/)
[![FastAPI](https://img.shields.io/badge/FastAPI-0.100%2B-009688.svg)](https://fastapi.tiangolo.com/)
[![Docker](https://img.shields.io/badge/Docker-Compose-2496ED.svg)](https://www.docker.com/)

## Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Tech Stack](#tech-stack)
- [Architecture](#architecture)
- [Getting Started](#getting-started)
  - [Prerequisites](#prerequisites)
  - [Installation](#installation)
  - [Configuration](#configuration)
  - [Running the Application](#running-the-application)
- [CI/CD & Deployment](#cicd--deployment)
- [Usage](#usage)
- [Contributing](#contributing)
- [License](#license)
- [Acknowledgements](#acknowledgements)

---

## Overview

**Linux AI Agent** is an AI-driven operations assistant that automates and manages Linux server tasks through a conversational interface. It uses LangGraph and LangChain to orchestrate AI agents that can connect to remote Linux hosts over SSH (via Paramiko), execute commands, monitor system state, and return results — all accessible through a Streamlit dashboard backed by a FastAPI service.

---

## Features

- Conversational interface for executing and monitoring Linux server tasks.
- AI agent orchestration via LangGraph and LangChain for chaining prompts, actions, and multi-step workflows.
- SSH connectivity to remote Linux hosts using Paramiko.
- Interactive web dashboard built with Streamlit for real-time operations and output visualization.
- REST API built with FastAPI and Uvicorn for backend request handling and task execution.
- Cloud deployment on AWS (ECS task definitions included) for scalable, production-ready hosting.
- Docker-based containerization and local orchestration via `docker-compose`.
- GitHub Actions workflow for CI/CD automation.
- Modular architecture with a clear separation between the backend API, frontend dashboard, and agent orchestration layers.

---

## Tech Stack

| Layer | Technology |
|---|---|
| **Backend API** | Python, FastAPI, Uvicorn |
| **Frontend / Dashboard** | Streamlit |
| **AI / Agent Frameworks** | LangChain, LangGraph, LangChain-OpenAI |
| **LLM Provider** | OpenAI (via `langchain-openai`) |
| **SSH / Remote Execution** | Paramiko |
| **Containerization** | Docker, Docker Compose |
| **Cloud / Infrastructure** | AWS ECS (task definitions included) |
| **CI/CD** | GitHub Actions (`.github/workflows/`) |
| **Configuration** | python-dotenv (`.env` file) |

---

## Architecture

The repository is organized as follows:

```
Linux-AI-Agent/
├── backend/                        # FastAPI application and agent logic
├── frontend/                       # Streamlit dashboard
├── .github/workflows/              # GitHub Actions CI/CD pipelines
├── docker-compose.yaml             # Local development orchestration
├── ecs-task-def-backend.json       # AWS ECS task definition — backend
├── ecs-task-def-frontend.json      # AWS ECS task definition — frontend
├── requirements.txt                # Python dependencies
└── README.md
```

**Data flow:**

```
User Input (Streamlit)
      ↓
FastAPI Backend (REST API)
      ↓
Agent Orchestration Layer (LangGraph / LangChain + OpenAI)
      ↓
SSH to Target Linux Host (Paramiko)
      ↓
Command Execution & Output
      ↓
Results returned to Frontend
```

---

## Getting Started

### Prerequisites

- [Python 3.10+](https://www.python.org/downloads/)
- [Docker](https://docs.docker.com/get-docker/) and [Docker Compose](https://docs.docker.com/compose/install/)
- An [OpenAI API key](https://platform.openai.com/account/api-keys)
- SSH access credentials to the target Linux host(s)

### Installation

1. **Clone the repository:**

   ```bash
   git clone https://github.com/BhavyaJethwa/Linux-AI-Agent.git
   cd Linux-AI-Agent
   ```

2. **Create and activate a virtual environment:**

   ```bash
   python -m venv venv
   source venv/bin/activate        # macOS / Linux
   venv\Scripts\activate           # Windows
   ```

3. **Install dependencies:**

   ```bash
   pip install -r requirements.txt
   ```

### Configuration

Create a `.env` file in the project root and populate it with the required environment variables:

```env
# OpenAI
OPENAI_API_KEY=your_openai_api_key_here

# Target Linux Host (SSH)
SSH_HOST=your_server_ip_or_hostname
SSH_PORT=22
SSH_USER=your_ssh_username
SSH_PASSWORD=your_ssh_password        # or use SSH_KEY_PATH below
SSH_KEY_PATH=/path/to/private/key     # optional: path to SSH private key

# Backend
BACKEND_PORT=8000

# Frontend
FRONTEND_PORT=8501
```

> **Note:** Never commit your `.env` file. It is already listed in `.gitignore`.

### Running the Application

#### Option 1 — Docker Compose (recommended)

```bash
docker-compose up --build
```

This starts both the backend API and the Streamlit frontend. Visit:
- Frontend: `http://localhost:8501`
- Backend API docs: `http://localhost:8000/docs`

#### Option 2 — Run locally without Docker

Start the backend:

```bash
cd backend
uvicorn main:app --reload --port 8000
```

Start the frontend (in a separate terminal):

```bash
cd frontend
streamlit run app.py
```

---

## CI/CD & Deployment

### GitHub Actions

The `.github/workflows/` directory contains the CI/CD pipeline configuration. On every push to `main`, the pipeline:

1. Runs linting and tests.
2. Builds Docker images for the backend and frontend.
3. Pushes images to a container registry.
4. Deploys to AWS ECS using the included task definitions.

### AWS ECS Deployment

Production task definitions are provided for both services:

- `ecs-task-def-backend.json` — backend FastAPI service
- `ecs-task-def-frontend.json` — frontend Streamlit service

Update the image URIs and environment variables in these files to match your AWS ECR repository and deployment environment before deploying.

---

## Usage

1. Open the Streamlit dashboard at `http://localhost:8501`.
2. Enter the natural-language task or command you want to run on your Linux server (e.g., *"Check disk usage on the server"* or *"List all running processes"*).
3. The AI agent will translate your request into the appropriate shell commands, execute them over SSH, and display the results in the dashboard.

---

## Contributing

Contributions are welcome! To contribute:

1. Fork the repository.
2. Create a new branch: `git checkout -b feature/your-feature-name`
3. Make your changes and commit: `git commit -m "Add your feature"`
4. Push to your fork: `git push origin feature/your-feature-name`
5. Open a Pull Request against the `main` branch.

Please ensure your code follows the existing style and that any new dependencies are added to `requirements.txt`.

---

## License

This project is licensed under the [MIT License](LICENSE).

---

## Acknowledgements

- [LangChain](https://www.langchain.com/) and [LangGraph](https://github.com/langchain-ai/langgraph) for the agent orchestration framework.
- [OpenAI](https://openai.com/) for the underlying language model.
- [Paramiko](https://www.paramiko.org/) for SSH connectivity.
- [FastAPI](https://fastapi.tiangolo.com/) for the backend API framework.
- [Streamlit](https://streamlit.io/) for the interactive frontend dashboard.
