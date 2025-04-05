# Teams Data Extraction Pipeline

A Python-based pipeline to extract Microsoft Teams messages via Graph API and store them in PostgreSQL.

## 📋 Overview
- Extracts Teams messages, channels, and user data
- Stores structured data in PostgreSQL
- Uses Microsoft Graph API for data extraction
- Batch processing with parallel execution

## 🚀 Getting Started

### Prerequisites
- Python 3.6+
- PostgreSQL database
- Microsoft Azure App credentials:
  - Client ID
  - Client Secret
  - Tenant ID

### Installation
1. Clone repository:
```bash
git clone https://github.com/sam-yak/samyak_glynac_data_exchange.git
cd samyak_glynac_data_exchange
```
### Create virtual environment:

```bash
python -m venv venv
source venv/bin/activate  # Linux/MacOS
# venv\Scripts\activate  # Windows
```
### Install dependencies:
```bash
pip install -r requirements.txt
```
### Configuration

Create .env file:

```env

# Microsoft Identity
CLIENT_ID=your_azure_client_id
CLIENT_SECRET=your_azure_client_secret
TENANT_ID=your_azure_tenant_id

# PostgreSQL
DB_HOST=your_db_host
DB_NAME=your_db_name
DB_USER=your_db_user
DB_PASSWORD=your_db_password
DB_PORT=5432
```
# Usage

Run full pipeline:

```bash
python main.py
```
Individual components:

```bash

# Extract messages to JSON
python teams_batch_extract.py

# Load JSON into database
python store_teams.py
```
# 📂 Folder Structure

Copy
├── teams_json/          # Extracted Teams messages (JSON)
├── auth_token.py        # Microsoft Graph authentication
├── extract_messages.py  # Core extraction logic
├── fetch_users.py       # Database user queries
├── store_teams.py       # Database insertion
├── main.py              # Main pipeline
└── config.py            # Configuration loader

# 🗄️ Database Schema

```sql

CREATE TABLE chat_data_field_test (
    platform TEXT,
    chat_id TEXT PRIMARY KEY,
    chat_from TEXT,
    channel TEXT,
    message TEXT,
    thread_id TEXT,
    timestamp TIMESTAMP,
    mentioned_users TEXT,
    date_extracted TIMESTAMP
);
```
# 🔧 Troubleshooting

Common issues:

403 Forbidden: Verify Azure AD app permissions
Database Connection Issues: Check .env credentials
Empty JSON Files: Ensure target users have Teams activity
