# Linux-Agent

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

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
- [CI/CD & Deployment](#cicd-and-deployment)  
- [Usage](#usage)  
- [Contributing](#contributing)  
- [License](#license)  
- [Acknowledgements](#acknowledgements)

## Overview  
**Linux-Agent** is an AI-driven operations assistant built to automate and manage Linux server operations using a conversational interface. The system leverages modern AI tooling and cloud infrastructure to provide agents that can monitor, control, and react to Linux hosts via chat, streamlit dashboard, and backend integration.

## Features  
- Conversational interface for executing and monitoring Linux server tasks.  
- Agent orchestration using LangGraph and LangChain for chaining prompts, actions and workflows.  
- Web dashboard using Streamlit for interactive operations and visualization.  
- REST API built with Flask for backend request handling, task execution and status tracking.  
- Cloud deployment on AWS (e.g., ECS task definitions included) for scalable hosting.  
- Docker-based containerization and orchestration with `docker-compose` and cloud task definitions.  
- GitHub Actions workflow for CI/CD automation.  
- Modular architecture with clear separation between backend, frontend and orchestration layers.

## Tech Stack  
- **Backend**: Python, Flask  
- **Frontend / Dashboard**: Streamlit  
- **AI / Agent Frameworks**: LangChain, LangGraph  
- **Containerization / Orchestration**: Docker, Docker-Compose  
- **Cloud / Infrastructure**: AWS (ECS task definitions included)  
- **CI/CD**: GitHub Actions (in `.github/workflows`)  
- **Storage / Configuration**: (Please add any DB, cache, or config tech used)  
- **Other Tools / Libraries**: (e.g., requirements in `requirements.txt`)  
- **Infrastructure as Code / Task Definitions**: `ecs-task-def-backend.json`, `ecs-task-def-frontend.json`

## Architecture  
The repository is organised into:  
- `backend/` — the Flask API implementation and business logic.  
- `frontend/` — the Streamlit application for user interaction.  
- `.github/workflows/` — GitHub Actions CI/CD pipelines.  
- `docker-compose.yaml` — local development orchestration.  
- `ecs-task-def-backend.json` & `ecs-task-def-frontend.json` — AWS ECS task definitions for production deployment.

Data flows from user input (via Streamlit or chat) → the backend API → the agent orchestration layer (LangGraph/LangChain) → executes tasks on target Linux hosts → returns results/status back to frontend.
