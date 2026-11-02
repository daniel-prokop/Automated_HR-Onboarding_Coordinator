# 🚀 Train Today - AI Onboarding Coordinator

An AI-powered onboarding workflow built with **n8n**, **Groq LLMs**, **Google Sheets**, **Gmail**, and **Notion**.

The project demonstrates how traditional workflow automation and AI Agents can work together to coordinate employee onboarding while maintaining appropriate human oversight.

Rather than automating the entire onboarding process, the workflow focuses on a realistic onboarding scenario that showcases:

- AI Agent orchestration
- Tool calling
- Human-in-the-loop workflows
- Structured task management
- Department-specific onboarding logic
- Hybrid automation architecture

Based on the WBS CODING SCHOOL project:

> The Onboarding Coordinator

---

# 📋 Project Goal

Employee onboarding often involves multiple departments, manual coordination, repetitive communication, and numerous system access requests.

This prototype demonstrates how an AI Agent can support onboarding by:

- interpreting onboarding checklists
- coordinating onboarding activities
- creating onboarding cases
- generating onboarding communications
- tracking onboarding tasks
- identifying where human approval is required

The solution intentionally avoids unrealistic full automation and instead follows practical business automation principles.

---

# 🏗 Architecture

```text
Start Onboarding
        ↓
Employee Information
        ↓
Required Data Validation
        ↓
Department Routing
        ↓
Checklist Selection
        ↓
AI Onboarding Coordinator Agent
        │
        ├──────── Gmail Draft Tool
        │
        ├──────── Google Sheets Task Tool
        │
        └──────── Notion Case Tool
        ↓
Onboarding Summary
```

---

# 🤖 Hybrid Automation Design

The workflow deliberately combines two automation approaches.

## Deterministic Workflow Logic

Traditional n8n workflow nodes handle predictable business rules:

- employee data validation
- onboarding initiation
- department routing
- checklist selection
- missing data handling

Typical nodes:

- Manual Trigger
- Set
- IF
- Switch
- Gmail

These tasks do not require AI reasoning and are therefore handled through standard workflow logic.

---

## Agentic Logic

The AI Agent is responsible for tasks that benefit from contextual reasoning and language generation.

Examples:

- onboarding task interpretation
- onboarding coordination
- communication drafting
- oversight classification
- tool selection
- final onboarding summaries

The workflow therefore demonstrates a genuine AI Agent architecture instead of simply calling an LLM within a traditional process.

---

# 🧠 AI Agent Responsibilities

The AI Agent acts as an Onboarding Coordinator.

Its responsibilities include:

✅ interpreting onboarding checklists

✅ identifying required onboarding tasks

✅ classifying human involvement requirements

✅ creating onboarding cases

✅ creating onboarding task records

✅ drafting onboarding communication

✅ orchestrating available tools

✅ generating onboarding completion summaries

The Agent must only use information provided by:

- employee data
- general onboarding checklist
- department-specific checklist

The Agent is explicitly restricted from inventing:

- policies
- systems
- licenses
- access rights
- meetings
- personnel
- company processes

---

# 🔧 Tool Calling

The Agent has access to three connected tools.

## 📧 Gmail Draft Tool

Used for creating onboarding communication drafts.

Examples:

- welcome email
- manager notification
- buddy request

Important:

The workflow creates drafts only.

Emails are never sent automatically.

```text
AI Agent
    ↓
Draft Email
    ↓
HR Review
    ↓
Human Approval
    ↓
Send
```

---

## 📊 Google Sheets Task Tool

Used as a lightweight onboarding tracker.

The Agent creates one task row for every onboarding activity.

Example tasks:

- Request Google Workspace account
- Request Slack access
- Schedule HR welcome meeting
- Schedule compliance training

All tasks initially receive:

```text
Status = Pending
```

---

## 📝 Notion Case Tool

Creates a single onboarding case per employee.

Example:

```text
Onboarding - Anna Schmidt - 2026-10-12
```

The Notion page acts as the central onboarding record.

---

# 👥 Human Oversight Model

The project demonstrates four levels of human involvement.

## Fully Automated

Low-risk, repetitive actions.

Example:

- onboarding task tracking

---

## Human in the Loop (HITL)

The system prepares actions that require approval.

Examples:

- onboarding emails
- employee records
- document processing
- HR updates

---

## Human on the Loop (HOTL)

Humans supervise process execution and intervene when necessary.

Examples:

- onboarding monitoring
- escalation handling
- task completion review

---

## Fully Human

Activities requiring contextual judgment remain human responsibilities.

Example:

```text
Selecting an onboarding buddy
```

The Agent is never allowed to choose an onboarding buddy.

---

# 🏢 Department-Specific Onboarding

The workflow supports department-specific onboarding processes.

## Marketing Department

Additional onboarding tasks include:

- HubSpot access
- Canva license
- Buffer access
- Google Ad Manager access
- Marketing vault access
- Brand guideline onboarding
- GDPR for Marketing training
- Marketing team introduction

---

## Other Departments

If no dedicated checklist exists:

- only the general onboarding checklist is used
- the Agent is informed that no department-specific checklist is available

This prevents AI hallucinating onboarding requirements.

---

# 📋 General Onboarding Checklist

Examples include:

- Create employee record
- Upload CV
- Upload contract
- Request workspace accounts
- Request Slack access
- Request Notion access
- Request password manager access
- Send welcome package
- Send welcome email
- Notify manager
- Schedule welcome meetings
- Schedule security training
- Schedule compliance training
- Confirm onboarding completion
- Schedule one-week check-in

---

# ✅ Validation & Error Handling

Before onboarding begins, required employee information is validated.

Required fields include:

- full name
- personal email
- company email
- role
- department
- manager name
- manager email
- start date

If information is missing:

```text
Validation Failure
        ↓
Create Missing Data Draft
        ↓
Human Follow-Up
```

The onboarding process does not continue until the necessary information is available.

---

# ⚡ Technology Stack

## Workflow Platform

- n8n Community Edition

## AI

- Groq
- openai/gpt-oss-20b

## Productivity Tools

- Gmail
- Google Sheets
- Notion

## Concepts Demonstrated

- AI Agents
- Tool Calling
- Human-in-the-Loop Design
- AI Governance
- Structured Automation
- Workflow Orchestration
- Task Management

---

# 🎯 Key Design Decisions

## Why use an AI Agent?

Because onboarding includes activities that benefit from:

- contextual interpretation
- communication generation
- tool orchestration
- process coordination

---

## Why not let the Agent do everything?

Deterministic business rules are more reliable in traditional workflow logic.

Example:

```text
Department = Marketing
```

should be handled by a workflow condition rather than an LLM decision.

---

## Why Gmail Drafts?

To preserve human approval before communication is sent.

---

## Why Google Sheets?

To provide a simple and transparent onboarding tracker.

---

## Why Notion?

To create a centralized onboarding case and documentation hub.

---

## Why keep some tasks human?

Not every onboarding decision should be automated.

Examples such as buddy assignments depend on:

- team dynamics
- workload
- availability
- interpersonal considerations

---

# 🧪 Test Scenarios

## Scenario 1 - Marketing Employee

Expected outcome:

- validation succeeds
- Marketing checklist is loaded
- onboarding case is created
- tasks are tracked
- communication drafts are generated

---

## Scenario 2 - Missing Employee Information

Expected outcome:

- validation fails
- missing data draft created
- AI Agent does not execute

---

## Scenario 3 - Non-Marketing Employee

Expected outcome:

- only the general checklist is used
- no Marketing-specific tasks are generated

---

# 🔮 Future Improvements

Potential enhancements include:

- workflow modularization via subworkflows
- approval workflows
- status monitoring agents
- multi-agent architecture
- HR system integrations
- onboarding dashboards
- automated onboarding status reviews

---

# 📚 Learning Objectives

This project demonstrates:

- AI-powered workflow automation
- Agentic AI design patterns
- Tool calling
- Human oversight strategies
- Workflow orchestration with n8n
- Practical business process automation

---

# 👤 Author

**Daniel Prokop**

Built as part of the WBS CODING SCHOOL AI & Automation curriculum.

---

# 📄 License

This project is intended for educational and portfolio purposes.

Feel free to adapt and extend it for your own learning and experimentation.
