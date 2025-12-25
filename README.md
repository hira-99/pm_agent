# Personal Manager Agent

A learning project demonstrating the creation of an AI-powered personal manager-assistant using the OpenAI SDK library. This project showcases the implementation of multi-agent systems with tools, handoffs, guardrails, and response monitoring.

## Overview

This project implements an intelligent personal manager that helps break down tasks into manageable steps. The agent can operate in two modes—serious and humorous—generating email responses that are both informative and engaging. The system uses a manager agent to evaluate multiple drafts and select the best one before automatically formatting and sending it via email.

## Features

### 🤖 Multi-Agent System
- **Helpful Agent**: Breaks down tasks into smaller, actionable steps in a serious, professional manner
- **Funny Agent**: Provides task breakdowns with humor, jokes, and puns to make work more enjoyable
- **Manager Agent**: Evaluates multiple email drafts from different agents and selects the best one
- **Email Manager Agent**: Handles email formatting (subject generation, HTML conversion) and sending

### 🛠️ Tools & Handoffs
- **Agent Tools**: Each agent is exposed as a tool that can be called by other agents
- **Handoffs**: Seamless transfer of work between agents using the handoff mechanism
- **Email Tools**: Custom tools for subject writing, HTML conversion, and email sending via Resend API

### 🛡️ Guardrails & Safety
- **Input Guardrails**: Name-checking guardrail to prevent including personal names in messages
- **Monitoring**: Response tracing and monitoring using the `trace` decorator to track agent execution

### 📧 Email Integration
- Automatic email formatting with HTML conversion
- Dynamic subject line generation
- Email delivery via Resend API

## Architecture

```
User Request
    ↓
Manager Agent (with guardrails)
    ↓
    ├─→ Helpful Agent Tool (generates serious draft)
    └─→ Funny Agent Tool (generates humorous draft)
    ↓
Manager evaluates and selects best draft
    ↓
Email Manager Agent (handoff)
    ├─→ Subject Writer Tool
    ├─→ HTML Converter Tool
    └─→ Send Email Tool
    ↓
Email Sent
```

## Technology Stack

- **OpenAI Agents SDK**: Core framework for building multi-agent systems
- **OpenAI GPT-4o-mini**: Language model for all agents
- **Resend API**: Email delivery service
- **Python**: Programming language
- **Python-dotenv**: Environment variable management

## Setup

1. **Install Dependencies**
   ```bash
   pip install -r requirements.txt
   # or using uv
   uv sync
   ```

2. **Environment Variables**
   Create a `.env` file with the following variables:
   ```
   OPENAI_API_KEY=your_openai_api_key
   RESEND_API_KEY=your_resend_api_key
   GMAIL_TO=your_email@example.com
   ```

3. **Run the Notebook**
   Open `openai_agent.ipynb` in Jupyter and execute the cells to interact with the agent system.

## Usage

```python
message = "Send out an email addressed to Dear Test from Hira"

with trace("Hira's Manager"):
    result = await Runner.run(careful_sales_manager, message)
```

The manager agent will:
1. Generate drafts using both the helpful and funny agents
2. Evaluate all drafts and select the best one
3. Hand off the selected draft to the Email Manager
4. Format and send the email automatically

## Key Concepts Demonstrated

- **Agent Creation**: Defining agents with specific roles, goals, and instructions
- **Tool Conversion**: Converting agents into tools that can be used by other agents
- **Handoffs**: Passing work between agents for specialized processing
- **Guardrails**: Implementing safety checks and validation at the input level
- **Monitoring**: Using tracing to monitor and debug agent execution flows
- **Output Types**: Using Pydantic models for structured agent outputs

## Project Structure

```
personal_manager/
├── openai_agent.ipynb    # Main notebook with agent implementation
├── pyproject.toml        # Project dependencies
├── requirements.txt      # Python dependencies
├── README.md            # This file
└── .env                 # Environment variables (create this)
```

## Learning Outcomes

This project serves as a practical exploration of:
- Building multi-agent AI systems
- Implementing agent orchestration and coordination
- Creating reusable agent tools
- Establishing guardrails for AI safety
- Integrating external APIs (email services)
- Monitoring and debugging agent workflows

## Notes

This is a learning project designed to explore the capabilities of the OpenAI Agents SDK and multi-agent system design patterns. The agent demonstrates how different specialized agents can work together to accomplish complex tasks through collaboration and handoffs.

## License

This is a personal learning project.
