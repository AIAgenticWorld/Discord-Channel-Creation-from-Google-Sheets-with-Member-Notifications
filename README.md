<img width="710" height="138" alt="image" src="https://github.com/user-attachments/assets/061b64e8-e1b3-47f0-bd66-b8766a736655" />

# 🔧 Automated Discord Channel Creation Workflow

This workflow provides an automated **Discord channel creation** solution powered by **n8n**, Google Sheets, and Discord API. It eliminates manual setup and ensures consistent team communication—ideal for agencies, dev teams, and project-based organizations.

---

## ✨ Key Features

- 🔍 **Automated Monitoring** – Watches Google Sheets for new entries needing Discord channels.
- 📢 **Discord Integration** – Creates channels using the Discord API with custom names and categories.
- 📊 **Smart Filtering** – Skips entries with already-created channels.
- 📧 **Member Notifications** – Sends well-formatted announcements with project details.
- 📈 **Status Tracking** – Updates Google Sheets with Discord channel IDs and statuses.
- 🔄 **Sequential Processing** – Ensures entries are handled in order.
- ⚡ **Error Handling** – Built-in validation and error messaging.
- 📝 **Customizable Templates** – Easy to edit Discord messages and mentions.

---

## 🎯 What This Workflow Does

### Input Sources

- **Google Sheets** – New entries requiring Discord channels.
- **Discord Configuration** – Server ID, bot token, category ID.
- **Notification Settings** – User mentions and roles.

### Processing Steps

1. **Monitor Trigger** – Detects new Google Sheet rows.
2. **Validate Entry** – Checks for incomplete or duplicate rows.
3. **Channel Creation** – Creates a new Discord channel.
4. **Google Sheet Update** – Stores channel ID and status.
5. **Status Check** – Confirms successful channel setup.
6. **Notification Dispatch** – Sends formatted message(s) in the channel.
7. **Follow-Up** – Sends any extra project info.
8. **Mark as Complete** – Updates final status in the sheet.

---

## 🧾 Output Data Points

| Field                | Description                                 | Example                                 |
|---------------------|---------------------------------------------|-----------------------------------------|
| Entry ID            | Unique ID for the sheet entry               | `ENTRY-2025-001`                        |
| Title/Name          | Project or entry name                       | `New Marketing Campaign`               |
| Category/Type       | Entry category                              | `Marketing Project`                    |
| Discord Channel ID  | Created Discord channel ID                  | `1234567890123456789`                  |
| Channel URL         | Direct link to channel                      | `https://discord.com/channels/...`     |
| Creation Status     | Current status                              | `Discord Created, Message Sent`        |
| Timestamp           | Completion time                             | `2025-06-06T09:00:00Z`                 |

---

## 🚀 Setup Instructions

### ✅ Prerequisites

- n8n instance (self-hosted or cloud)
- Google account with access to Google Sheets
- Discord bot with necessary permissions
- 10–15 minutes for setup

---

### 1. Import the Workflow

1. Copy JSON workflow code.
2. In n8n → Workflows → `+ Add workflow` → `Import from JSON`.
3. Paste the code and click **Import**.

---

### 2. Configure Discord Integration

#### Create Discord Bot:

- Go to [Discord Developer Portal](https://discord.com/developers/applications)
- Create a new application and add a bot.
- Copy bot token.

#### Add Bot to Server:

- Give permissions: `Manage Channels`, `Send Messages`, `Read Messages`.

#### Set Credentials in n8n:

- Go to `Credentials` → `+ Add` → **Discord Bot API**
- Paste your bot token → Test connection

#### Update Discord Info in Workflow:

- Add your **Server ID** and **Category ID** in all Discord nodes.

---

### 3. Configure Google Sheets Integration

#### Create a Google Sheet:

- Name: `Discord Channel Requests`
- Required Columns:
  - Column A: `Timestamp`
  - Column B: `Entry Name/Title`
  - Column C: `Category/Type`
  - Column D: `Description`
  - Column E: `Contact/Owner Information`
  - Column F: `Entry ID`
  - Column G: `Discord ID` *(auto-filled)*
  - Column H: `Status` *(auto-filled)*

#### Set Credentials:

- In n8n: `Credentials` → `+ Add` → **Google Sheets OAuth2 API**
- Complete OAuth flow and test connection

---

### 4. Update Workflow Settings

- Replace Google Sheet ID in `Monitor New Project Entries` node
- Select the correct sheet name
- Replace Discord bot credentials, guild ID, and category ID
- Customize team notifications or roles

---

### 5. Test & Activate

1. Add test row in Google Sheet (leave channel ID empty)
2. Activate the workflow in n8n
3. Check:
   - Discord channel created
   - Messages sent
   - Sheet updated with status

---

## 📖 Usage Guide

### Adding New Channel Requests

1. Open the linked Google Sheet.
2. Add a new row with all required info.
3. Leave the "Discord ID" and "Status" columns blank.
4. The workflow will run automatically within a few minutes.

---

### Understanding Statuses

| Status                          | Meaning                              |
|----------------------------------|--------------------------------------|
| _(blank)_                        | Entry not yet processed              |
| `Discord Created`               | Channel created, message not sent   |
| `Discord Created, Message Sent` | Full process complete                |
| `Error: <Message>`              | Issue encountered                    |

---

### Customizing Member Notifications

- Edit the `Send Project Announcement` and `Send Additional Project Details` nodes
- Replace `@everyone` with `@role` or specific user tags
- Use Discord markdown to style messages

---

## 🔧 Customization Options

### Add More Data Fields

- Update Sheet, message nodes, and Discord fields to include:
  - Budget
  - Deadlines
  - Priority
  - Owner/team

### Modify Discord Channel Structure

```json
"name": "{{ $json['Category/Type'] }}-{{ $json['Entry ID'] }}",
"topic": "Channel for {{ $json['Title/Name'] }} - {{ $json['Category/Type'] }}"
📄 License

MIT License

Copyright (c) 2025
