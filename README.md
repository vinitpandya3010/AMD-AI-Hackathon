# AI Scheduling Assistant: An Advanced Agentic Workflow Solution

![Flask](https://img.shields.io/badge/Flask-black?style=for-the-badge&logo=flask)
![vLLM](https://img.shields.io/badge/vLLM-Inference-orange?style=for-the-badge)

## 🚀 Project Overview

This project implements a sophisticated, autonomous AI assistant designed to eliminate the friction of meeting coordination. Leveraging a powerful agentic architecture built with **LangGraph**, the assistant can understand natural language requests, interact with real-world tools like Google Calendar, and reason through complex scheduling conflicts—including those spanning multiple timezones—to find optimal meeting times for all attendees.

The core mission is to create an intelligent system that goes beyond simple automation, acting as a true digital assistant that handles scheduling autonomously from start to finish.

## ✨ Key Features & Implementation

This solution was designed to meet and exceed the hackathon's core requirements for an agentic system.

| Required Feature | Status | Implementation Details |
| :--- | :--- | :--- |
| **Autonomous Coordination** | ✅ **Implemented** | The agent takes a single JSON request and handles the entire workflow—NLU, conflict detection, rescheduling, and formatting—with zero human intervention. |
| **Dynamic Adaptability** | ✅ **Implemented** | The **LangGraph** workflow includes conditional routing. When a calendar conflict is detected, the agent automatically pivots to a `find_alternatives` branch to find a new slot. |
| **Natural Language Interaction** | ✅ **Implemented** | The agent uses a Llama 3.1 model served via vLLM to robustly parse unstructured requests like "Let's meet tomorrow afternoon" into structured, actionable data. |
| **Calendar Integration** | ✅ **Implemented** |![Python](https://img.shields.io/badge/Python-3.12-blue.svg)
![Framework](https://img.shields.io/badge/Framework-LangGraph-orange.svg)
![API](https://img.shields.io/badge/API-Flask-black.svg)
![LLM](https://img.shields.io/badge/LLM-Llama_3.1-green.svg)
![Tools](https://img.shields.io/badge/Tools-Pydantic_&_Google_Calendar-purple.svg)

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

*   **Agentic Framework - LangGraph:** The heart of the solution is a stateful agent built with LangGraph. This allows for complex, cyclical reasoning—if a conflict is found, the agent can loop back, find alternatives, and re-evaluate, perfectly mimicking a human thought process.

*   **High-Performance NLU - Llama 3.1 & vLLM:** Natural Language Understanding is powered by Meta's Llama 3.1-8B-Instruct model, served via the high-throughput vLLM inference server on the MI300 GPU. This ensures fast and accurate extraction of user intent.

*   **Data Integrity - Pydantic:** All data structures, especially the agent's state, are defined and validated using Pydantic. This eliminates an entire class of runtime errors and ensures data consistency throughout the workflow.

*   **External Tools - Google Calendar API:** The agent is equipped with tools to connect to the Google Calendar API, allowing it to fetch real-world availability for all attendees.

*   **Stand The agent is equipped with a `get_calendar_events` tool that connects directly to the Google Calendar API using user-specific OAuth tokens to fetch real-world availability. |
| **Cross-Timezone Scheduling** | ✅ **Implemented** | A standout advanced feature. The agent finds optimal meeting times for globally distributed teams by calculating the overlapping "Golden Window" of their respective working hours. |

## 🛠️ Technical Architecture

This project is built on a professional, modular, and robust agentic stack.

1.  **API Endpoint (`Flask`):** A lightweight Flask server provides the `/receive` endpoint, acting as the front door for all incoming scheduling requests.

2.  **Agent Brain (`LangGraph`):** The core of the system is a stateful graph that defines the agent's reasoning process. This allows for complex, multi-step logic with conditional branches for handling errors and conflicts, which is impossible with a simple LLM chain.

3.  **LLM Integration (`LangChain` + `vLLM`):** The agent communicates with a `meta-llama/Meta-Llama-3.1-8B-Instruct` model hosted on a high-performance `vLLM` inference server for all Natural Language Understanding tasks.

4.  **Structured Data (`Pydantic`):** All data, including the agent's internal state (`AgentState`), is defined and validated using Pydantic models. This ensures data integrity and eliminates a common source of bugs.

5.  **Agent Tools:** The agent has access to a suite of specialized tools:
    *   `extract_meeting_details_from_email`: Parses the user's email content.
    *   `get_calendar_events`: Fetches busy/free information from Google Calendars.
    *   `find_available_slots`: The core logic for conflict resolution and multi-timezone optimization.

### 🌐out Feature - Multi-Timezone Intelligence:** The agent's most advanced feature is its ability to handle globally distributed teams. It calculates the overlapping working hours (the "Golden Window") for attendees in different countries (e.g., India, UK, USA) and intelligently searches for a suitable meeting time within that window, demonstrating a superior level of reasoning.

---

## ✅ Features & Success Metrics

This agent successfully meets and exceeds the hackathon's key requirements.

| Feature / Metric           | Status | Verification                                                                                                                                      |
| :------------------------- | :----: | :------------------------------------------------------------------------------------------------------------------------------------------------ |
| **Autonomous Coordination**  |   ✅   | The entire workflow is automated after the initial request.                                                                                       |
| **Dynamic Adaptability**     |   ✅   | The agent successfully detects calendar conflicts and automatically finds and proposes alternative time slots.                                      |
| **Natural Language Interaction** |   ✅   | The LLM successfully parses requests like "next Thursday" or "tomorrow morning."                                                                |
| **Calendar Integration** Advanced Capability: Multi-Timezone Scheduling

The agent's `find_available_slots` tool is designed to solve the difficult problem of scheduling for global teams. It performs the following logic:
1.  Identifies the local timezone of each attendee (e.g., India, UK, US).
2.  Calculates the standard working hours (9 AM - 6 PM) for each person in their local time.
3.  Converts all local work-hour windows to a universal standard (UTC).
4.  Calculates the **intersection** of all these UTC windows to find the "Golden Window" when everyone is at their desk.
5.  Searches for an open meeting slot *only within this Golden Window*, ensuring a proposed time is reasonable for all participants.

## ⚙️ Setup and Execution Guide

Follow these steps to run the AI Scheduling Assistant.

### 1. Prerequisites
Ensure you have cloned the hackathon repository and the `Keys/` directory with Google Calendar tokens is present.

### 2. Environment Setup
The provided     |   ✅   | The agent correctly reads pre-existing events from attendees' Google Calendars to determine availability.                                           |
| **Accuracy**               |   ✅   | The agent's scheduling logic is precise, and the final output JSON perfectly matches the required specification.                                    |
| **Creativeness in Approach** |   ✅   | The use of **LangGraph** for stateful reasoning and the implementation of **multi-timezone scheduling** represent a highly innovative approach. |

---

## ⚙️ Setup and Execution Guide

Follow these steps to run the AI Scheduling Assistant.

### Prerequisites `Submission New.ipynb` notebook is self-contained. **Run `Cell 0`** to install all required Python dependencies.
```bash
# This command is inside Cell 0
!pip install -q --upgrade \
    langchain langchain-core langchain-community langgraph langsmith \
    langchain-openai dateparser pytz google-api-python-client \
    google-auth-oauthlib requests



HIP_VISIBLE_DEVICES=0 vllm serve Models Llama 3.1 model using the following command. Wait for the `Application startup complete.` message before proceeding.

```bash
HIP_VISIBLE_DEVICES=0 vllm serve Models/meta-llama/Meta-L/meta-llama/Meta-Llama-3.1-8B-Instruct \
        --gpu-memory-utilization 0.9 \
        --swap-space 16 \
        --disable-loglama-3.1-8B-Instruct \
        --gpu-memory-utilization 0.9 \
        --swap-space 16 \
        --disable-log-requests \
        --dtype-requests \
        --dtype float16 \
        --max-model-len 2048 float16 \
        --max-model-len 2048 \
        --tensor-parallel-size 1 \
        --host 0.0.0.0 \
        --port 4 \
        --tensor-parallel-size 1 \
        --host 0.0.0.0000 \
        --distributed-executor-backend "mp"


    --port 4000 \
    --distributed-executor-backend "mp"

Wait for the Submission Notebook

1.  Open the `Submission New.ipynb` notebook.
2.  **Run all the server to display `INFO:     Application startup complete.`

### 4. Run the Agent Notebook
Return to ` cells from top to bottom.**
    *   **Cell 0** will install any necessary dependencies. **You must restart the kernel after this cell completes.**
    *   **Cells 1-7** define the agent's architecture,Submission New.ipynb` and run all cells from top to bottom (`Cell 1` through `Cell 15`). This will:
1.  Import all libraries and define the agent's logic.
2.  Start the Flask API server in the background on **port 5000**.
3.  Execute a comprehensive test tools, and the Flask API.
    *   **Cell 8** starts the Flask server in the background. The server will be listening for requests on port `5000`.
    *   The subsequent cells will run a comprehensive suite of tests, proving the agent's functionality.

---

## 📡 API Endpoint for Testing

The agent is exposed suite to validate all agent functionalities.

## 🧪 How to Test the API

Once the Flask server is running, you can test it from anywhere on the network.

### Using Postman
1.  **Method:** `POST`
2 via a POST request to the `/receive` endpoint.

*   **Method:** `POST`
*   **URL:** `http://<YOUR_INSTANCE_IP>:5000/receive`
    *(Find your instance's public IP.  **URL:** `http://<YOUR_INSTANCE_IP>:5000/receive` (The IP address is shown in the Flask startup logs).
3.  **Body:** Select `raw` and `JSON`. address in the startup log of the Flask server in Cell 8)*
*   **Headers:** `Content-Type: application/json`
*   **Body (raw JSON):** Provide the input JSON in the specified format.

####
4.  **Content:** Paste the content of a valid `input.json` file.

**Sample `input.json` for Timezone Test:**
```json
{
    "Request_id": "postman-timezone-test-001",
    "Datetime": "2025-07-21T10:00:00Z",
    "Location": "Virtual / Cross-Timezone",
     Sample Request Body:

```json
{
    "Request_id": "api-test-001",
    "Datetime": "2025-07-21T10:00:00Z",
    "Location": "Virtual / Cross-Timezone",
    "From": "userone.amd@gmail.com",
    "Attendees": [
        {
            "email": "usertwo.amd@gmail.com"
        },
        {
            "email": "userthree."From": "userone.amd@gmail.com",
    "Attendees": [
        {"email": "usertwo.amd@gmail.com"},
        {"email": "userthree.amd@gmail.amd@gmail.com"
        }
    ],
    "Subject": "Global Sync for Q3 Planning",
    "EmailContent": "Hi team, let's connect for our Q3 planning session. Can we meet for an hour sometime tomorrow morning?"
}


### Final Output Format
The API will return a JSON object that precisely matches the structure specified in the hackathon according to the hackathon specification.