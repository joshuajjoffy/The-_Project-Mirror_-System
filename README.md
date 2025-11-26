🔄 Cross-Platform Project Sync System (The "Project Mirror")

📋 Overview

The Project Mirror System is a business process automation suite designed to keep engineering status (Trello) and management reporting (Google Sheets) in perfect sync.

This system ensures that stakeholders always have real-time visibility into project progress without needing access to technical boards. It eliminates manual status reporting by automatically syncing card movements and triggering instant email notifications when tasks are completed.

🚀 Key Features

Real-Time Kanban Sync: Instantly captures card movements in Trello via Webhooks.

Smart "Upsert" Logic: Automatically detects whether to create a new record or update an existing one in Google Sheets based on the unique Card ID.

Conditional Alerting: Uses Logic Gates (If/Else) to filter noise and only trigger notifications for "Done" tasks.

🛠️ Tech Stack

Orchestration: n8n

Frontend/Input: Trello (Kanban Board)

Database: Google Sheets

Communication: Gmail (SMTP)

⚙️ Architecture & Logic

The Sync Engine Workflow

Trigger: Watch Trello Board for updateCard or moveCard events.

Sync Node:

Input: Trello JSON Payload.

Action: Upsert row in Google Sheet where Column A (Card ID) matches Input ID.

Update: Set Status to new List Name and Timestamp to $now.

Logic Gate:

Condition: If Status == "Done"

True: Send "Task Complete" Email to Manager.

False: End workflow (Do not spam manager for "In Progress" tasks).

(Note: Upload a screenshot of your n8n workflow here)

📥 Example Notification

Subject: ✅ Task Complete: Fix Server API

Body:
Project Update:
The task "Fix Server API" has been successfully moved to DONE.
The Trello Board and Google Sheet are now in sync.

Card ID: 69272b...
Timestamp: 2025-11-26T14:30:00

🔧 How to Run

Prerequisites

Trello: Get your API Key and Token from the Trello Power-Up Admin portal.

Google Sheets: Create a sheet with headers: card_id, task_name, status, last_updated.

Installation

Import Workflow: Import the project_sync.json file.

Configure Credentials: Connect your Trello, Google Sheets, and Gmail accounts.

Activate: Toggle the workflow to "Active".

Built with n8n
