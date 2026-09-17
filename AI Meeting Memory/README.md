# AI Meeting Memory and Task Tracking System
![AI Meeting Memory Workflow](workflow(2).png)
An AI-powered n8n workflow that turns completed meeting transcripts into structured summaries, action items, CRM updates, approval-based follow-ups, and task reminders.

## What It Does

The workflow receives a completed meeting through a webhook and sends the transcript to an AI model for analysis.

The extracted information is then routed to different business systems.

```text
Meeting Completed
        ↓
Webhook
        ↓
Normalize Transcript
        ↓
AI Meeting Analysis
        ↓
Parse Structured Output
        ↓
   ┌────┼──────────────┐
   ↓    ↓              ↓
Tasks  CRM       Approval Flow
   ↓    ↓              ↓
Notion HubSpot     Slack
                       ↓
                  Wait for Approval
                       ↓
                  Gmail Draft
```

A separate scheduled workflow checks incomplete tasks and sends a task digest.

```text
Every 24 Hours
      ↓
Fetch Incomplete Tasks
      ↓
Notion
      ↓
Task Digest
```

## Features

### AI Meeting Analysis

Processes meeting transcripts and extracts useful structured information from unstructured conversation.

### Action Item Extraction

Identifies tasks discussed during meetings and separates them into structured action items.

### Notion Task Management

Creates tasks from extracted action items for further tracking.

### CRM Updates

Sends relevant meeting information to HubSpot for CRM follow up.

### Approval Workflow

Uses Slack to introduce a human approval step before follow up actions continue.

### Gmail Follow Up

Creates an email draft based on the approved meeting information.

### Scheduled Task Monitoring

Periodically checks incomplete tasks and generates a task digest.

## Workflow Components

| Component         | Purpose                                 |
| ----------------- | --------------------------------------- |
| Webhook           | Receives completed meeting data         |
| JavaScript        | Normalizes incoming transcript data     |
| OpenAI            | Analyzes the meeting                    |
| JSON Parser       | Converts AI output into structured data |
| Notion            | Stores action items                     |
| HubSpot           | Handles CRM updates                     |
| Slack             | Handles approval                        |
| Gmail             | Creates follow up drafts                |
| Scheduled Trigger | Checks incomplete tasks                 |

## Input Example

A sample meeting payload is available in:

`examples/meeting-input.json`

Example input:

```json
{
  "meeting_id": "meeting_001",
  "title": "Project Planning Meeting",
  "transcript": "Discussed the new automation project. Yasir will prepare the technical architecture by Friday. Ahmed will review the API requirements.",
  "participants": [
    "Yasir",
    "Ahmed"
  ]
}
```

## Technology Stack

n8n

OpenAI

Notion

HubSpot

Slack

Gmail

Webhooks

JavaScript

JSON

## Project Structure

```text
AI Meeting Memory
│
├── examples
│   └── meeting-input.json
│
├── .env.example
├── .gitignore
├── README.md
└── workflow.json
```

## Setup

1. Import `workflow.json` into n8n.

2. Configure the required credentials.

3. Configure the Notion database.

4. Configure the OpenAI connection.

5. Configure HubSpot.

6. Configure Slack approval.

7. Configure Gmail.

8. Test the webhook using the sample payload in `examples/meeting-input.json`.

## Security

No API keys, passwords, tokens, or private credentials are included in this repository.

Use `.env.example` as a reference for the required configuration.

## Current Status

Portfolio demonstration.

Some integrations require environment specific configuration before they can be used in production.

## Planned Improvements

Structured AI output validation

Better error handling

Automatic retry handling

Meeting decision extraction

Meeting priority classification

Calendar integration

Automatic deadline reminders

Meeting history storage

Improved logging

Production monitoring
