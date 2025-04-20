# Autogen-Studio Multi Agent Assistant

## Project Overview

A configurable multi-agent orchestration framework powered by AutoGen and OpenAI. This repository implements a **multi-agent personal assistant** using the AutoGen framework and OpenAI models (GPT-4 / GPT-4o). The assistant coordinates a team of specialized agents—handling tasks such as research, summarization, email drafting, scheduling, to‑do list management, and analytics—to autonomously fulfill complex user requests via a conversational interface.

The orchestration code serializes agent configurations and prompt definitions into a JSON file (`orchestrated_team_config.json`), which can be imported into **AutoGen Studio** for a no‑code UI experience, allowing visual inspection of system messages, prompt structures, and live agent interactions.

⚠ Note: The AutoGen framework is under active development; APIs and agent behavior may change in future releases. Check the official AutoGen repository for the latest updates.

## Architecture

![image](https://github.com/user-attachments/assets/4fcaffe8-252f-4b46-8da7-f3b3c6ed4040)


## Agent Roles & Responsibilities

- **Mehmet_Gur (UserProxyAgent)**  
  Acts as the end user, providing clarifications when needed.

- **Orchestrator (AssistantAgent)**  
  Oversees the workflow, delegates tasks per the plan from Intent_Task_Router, and triggers JSON export via `team.dump_component()`.

- **Input_Preprocessor (AssistantAgent)**  
  Cleans and normalizes user queries; outputs `Cleaned Query:`.

- **Intent_Task_Router (AssistantAgent)**  
  Analyzes cleaned queries, determines intents, and generates a step-by-step plan assigning tasks to agents.

- **Research_Agent (AssistantAgent)**  
  Gathers information on specified topics using GPT-4o’s browsing capabilities.

- **Summarization_Agent (AssistantAgent)**  
  Produces concise summaries based on length or bullet-point requirements.

- **Email_Drafting_Agent (AssistantAgent)**  
  Drafts email bodies without signatures or salutations.

- **Email_Processing_Agent (AssistantAgent)**  
  Performs sentiment analysis (`Sentiment:`) or invokes `save_email_draft` to persist drafts.

- **To_Do_List_Agent (AssistantAgent)**  
  Adds tasks to `todo_list.txt` via `add_todo_item`.

- **Scheduling_Calendar_Agent (AssistantAgent)**  
  Logs events to `calendar_log.txt` using `add_scheduled_event`.

- **Clarification_Agent (AssistantAgent)**  
  Asks targeted follow-up questions when required information is missing.

- **Analytics_Logging_Agent (AssistantAgent)**  
  Records workflow events in `assistant_log.txt` with `log_event`.

## Autogen Studio UI Demo


https://github.com/user-attachments/assets/8ddbeaa8-f740-4f2d-b46f-5c55e22990b6


## Installation & Setup

### 1. Clone the Repository

```bash
git clone https://github.com/mehmettgur/autogen-multiagent.git
cd autogen-multiagent
```

### 2. Create Virtual Environment & Install Dependencies

```bash
python3 -m venv venv
source venv/bin/activate    # Windows: venv\Scripts\activate

# Python 3.10 or higher
pip install -r requirements.txt
```

### 3. Configure Your OpenAI API Key Configure Your OpenAI API Key

#### Via JSON config file (`your_api_key.json`)

```json
[
  {
    "model": "gpt-4",
    "api_key": "YOUR_OPENAI_API_KEY"
  }
]
```

Replace `YOUR_OPENAI_API_KEY` with your actual key from OpenAI.

---

## License
This project is licensed under the MIT License. See the LICENSE file for details.
