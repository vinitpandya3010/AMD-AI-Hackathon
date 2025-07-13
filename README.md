# AI Scheduling Assistant: An Advanced Agentic Workflow

![Python](https://img.shields.io/badge/Python-3.12-blue?style=for-the-badge&logo=python)
![Framework](https://img.shields.io/badge/Framework-LangGraph-orange?style=for-the-badge)
![API](https://img.shields.io/badge/API-Flask-black?style=for-the-badge&logo=flask)
![LLM](https://img.shields.io/badge/LLM-Llama_3.1-green?style=for-the-badge)
![Tools](https://img.shields.io/badge/Tools-Google_Calendar-purple?style=for-the-badge&logo=google-calendar)

This repository contains the complete submission for the Agentic AI Scheduling Assistant Hackathon. The project implements a sophisticated, autonomous AI agent capable of understanding natural language requests, checking real-world calendars, and intelligently scheduling meetings—even for globally distributed teams across multiple timezones.

---

## 🚀 Project Overview

The mission was to create an AI assistant that eliminates the back-and-forth of meeting coordination. This solution achieves that by implementing a true **Agentic AI** that can:

-   **Reason** like a human assistant to resolve scheduling conflicts.
-   **Act** independently to check calendars and propose optimal times.
-   **Integrate** seamlessly with external tools like Google Calendar.

The core of this project is not a simple script, but a stateful, reasoning engine that can handle complex, multi-step tasks with robustness and precision.

---

## 🛠️ Core Architecture

This solution was built using a modern, professional AI engineering stack designed for creating robust and scalable agents.

*   **Agentic Framework - LangGraph:** The heart of the solution is a stateful agent built with LangGraph. This allows for complex, cyclical reasoning—if a conflict is found, the agent can loop, find alternatives, and re-evaluate, perfectly mimicking a human thought process.

*   **High-Performance NLU - Llama 3.1 & vLLM:** Natural Language Understanding is powered by Meta's Llama 3.1-8B-Instruct model, served via the high-throughput vLLM inference server on the MI300 GPU. This ensures fast and accurate extraction of user intent.

*   **Data Integrity - Pydantic:** All data structures, especially the agent's state, are defined and validated using Pydantic. This eliminates an entire class of runtime errors and ensures data consistency throughout the workflow.

*   **Advanced Capability - Multi-Timezone Intelligence:** The agent's `find_available_slots` tool is designed to solve the difficult problem of scheduling for global teams. It performs the following logic:
    1.  Identifies the local timezone of each attendee (e.g., India, UK, US).
    2.  Calculates the standard working hours (9 AM - 6 PM) for each person in their local time.
    3.  Converts all local work-hour windows to a universal standard (UTC).
    4.  Calculates the **intersection** of all these UTC windows to find the "Golden Window" when everyone is at their desk.
    5.  Searches for an open meeting slot *only within this Golden Window*, ensuring a proposed time is reasonable for all participants.

---

## ⚙️ Setup and Execution Guide

Follow these steps to run the AI Scheduling Assistant.

### 1. Prerequisites
- Ensure you have access to the MI300 GPU Instance.
- Clone the project repository. Ensure the `Keys/` directory is present and contains valid Google Calendar tokens for `userone.amd@gmail.com`, `usertwo.amd@gmail.com`, and `userthree.amd@gmail.com`.

### 2. Start the vLLM Server
Open a new terminal in the Jupyter Lab environment and launch the Llama 3.1 model. Wait for the `Application startup complete.` message before proceeding.

```bash
HIP_VISIBLE_DEVICES=0 vllm serve Models/meta-llama/Meta-Llama-3.1-8B-Instruct \
        --gpu-memory-utilization 0.9 \
        --swap-space 16 \
        --disable-log-requests \
        --dtype float16 \
        --max-model-len 2048 \
        --tensor-parallel-size 1 \
        --host 0.0.0.0 \
        --port 4000 \
        --distributed-executor-backend "mp"



3. Run the Submission Notebook
Open the Submission New.ipynb notebook.
Run all cells from top to bottom.
Cell 0 will install any necessary Python dependencies. You must restart the kernel after this cell completes.
Cells 1-7 define the agent's architecture, tools, and the Flask API.
Cell 8 starts the Flask server in the background. The server will be listening for requests on port 5000.
The subsequent cells will run a comprehensive suite of tests, proving the agent's functionality.


📡 API Endpoint for Testing
The agent is exposed via a POST request to the /receive endpoint.
Method: POST
URL: http://<YOUR_INSTANCE_IP>:5000/receive
(Find your instance's public IP address in the startup log of the Flask server in Cell 8)
Headers: Content-Type: application/json
Body (raw JSON): Provide the input JSON in the specified format.



Sample Request Body:

{
    "Request_id": "api-test-001",
    "Datetime": "2025-07-21T10:00:00Z",
    "Location": "Virtual / Cross-Timezone",
    "From": "userone.amd@gmail.com",
    "Attendees": [
        {"email": "usertwo.amd@gmail.com"},
        {"email": "userthree.amd@gmail.com"}
    ],
    "Subject": "Global Sync for Q3 Planning",
    "EmailContent": "Hi team, let's connect for our Q3 planning session. Can we meet for an hour sometime next week?"
}

