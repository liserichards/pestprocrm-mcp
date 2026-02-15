# PestProCRM MCP Server

Connect [Claude](https://claude.ai) to your [PestPro CRM](https://www.pestprocrm.com) account using the [Model Context Protocol (MCP)](https://modelcontextprotocol.io). Manage customers, schedule appointments, send SMS messages, track payments, and generate reports — all through natural conversation.

## What is PestPro CRM?

[PestPro CRM](https://www.pestprocrm.com) is a customer relationship management platform built specifically for pest control professionals. It handles scheduling, invoicing, customer management, SMS communication, and payment collection so you can focus on running your business.

## How to Connect

### Claude.ai (Recommended)

1. Go to [claude.ai](https://claude.ai)
2. Open **Settings** → **Integrations** (or click the MCP icon)
3. Click **Add custom integration**
4. Enter the server URL:
   `https://www.pestprocrm.com/api/mcp`
5. Click **Connect** — you'll be redirected to log in with your PestProCRM account
6. Authorize Claude to access your data
7. Start chatting!

### Claude Desktop

1. Log into PestProCRM and go to **Settings** → **API Keys**
2. Click **Generate New Key** and copy the key (starts with `pp_live_`)
3. Clone this repo and build:
   ```bash
   git clone https://github.com/yourusername/pestprocrm-mcp.git
   cd pestprocrm-mcp
   npm install && npm run build
   ```
4. Add to your Claude Desktop config:
   - macOS: `~/Library/Application Support/Claude/claude_desktop_config.json`
   - Windows: `%APPDATA%\Claude\claude_desktop_config.json`
   ```json
   {
     "mcpServers": {
       "pestpro": {
         "command": "node",
         "args": ["/absolute/path/to/pestprocrm-mcp/dist/index.js"],
         "env": {
           "PESTPRO_API_URL": "https://www.pestprocrm.com",
           "PESTPRO_API_KEY": "pp_live_your-key-here"
         }
       }
     }
   }
   ```
5. Restart Claude Desktop

### Claude Code

Add to your project's `.mcp.json`:

```json
{
  "mcpServers": {
    "pestpro": {
      "command": "node",
      "args": ["/absolute/path/to/pestprocrm-mcp/dist/index.js"],
      "env": {
        "PESTPRO_API_URL": "https://www.pestprocrm.com",
        "PESTPRO_API_KEY": "pp_live_your-key-here"
      }
    }
  }
}
```

## Available Tools

### Customer Management

| Tool | Description |
|------|-------------|
| `search_customers` | Find customers by name, address, phone, or email |
| `get_customer` | Get full details for a specific customer |
| `create_customer` | Add a new customer with contact info, address, and service details |
| `update_customer` | Update customer information (name, phone, address, service plan, etc.) |

### Scheduling

| Tool | Description |
|------|-------------|
| `get_schedule` | View appointments for a date range |
| `book_appointment` | Schedule a new service appointment |
| `reschedule_appointment` | Move an appointment to a new date/time |
| `cancel_appointment` | Cancel an appointment with a reason |
| `log_drive_time` | Record drive time between jobs |
| `complete_visit` | Mark a service visit as completed with notes |

### SMS Messaging

| Tool | Description |
|------|-------------|
| `send_sms` | Send a text message to a customer |
| `get_sms_history` | View text message conversation history with a customer |

### Payments

| Tool | Description |
|------|-------------|
| `create_payment_link` | Generate a Stripe payment link to send to a customer |
| `get_payment_status` | Check payment status for a customer |
| `mark_payment_collected` | Record a cash, check, or external payment as collected |

### Reporting

| Tool | Description |
|------|-------------|
| `get_revenue_report` | Revenue summary for a date range |
| `get_daily_summary` | Summary of services, revenue, and activity for a specific day |
| `get_customer_metrics` | Customer count, churn rate, and growth metrics |

### Resources (Read-Only)

| Resource | Description |
|----------|-------------|
| `pestpro://customers` | Browse all customers |
| `pestpro://schedule/today` | Today's schedule |
| `pestpro://schedule/week` | This week's schedule |
| `pestpro://payments/outstanding` | Customers with outstanding payments |
| `pestpro://metrics` | Business metrics dashboard |

## Usage Examples

### 1. Look up a customer and check their balance

> "Find my customer John Smith and tell me if he has any outstanding payments"

Claude will search your customers, pull up John's details, and check his payment status — all in one response.

### 2. Schedule an appointment

> "Schedule a German roach treatment for Jane Doe next Tuesday at 2pm"

Claude will find the customer, check your availability, and book the appointment.

### 3. Send a payment reminder via text

> "Which customers owe me money? Send the overdue ones a friendly payment reminder with their payment link"

Claude will check outstanding payments, generate payment links, and text each overdue customer.

### 4. Get a daily schedule briefing

> "What does my schedule look like tomorrow?"

Claude will show you all appointments for the day with customer names, service types, addresses, and any open time slots.

### 5. Record a completed service

> "I just finished the service at Mary Johnson's house. Mark it complete — general pest, interior and exterior, no issues. She paid $75 cash"

Claude will mark the visit complete with your notes and record the cash payment.

### 6. Monthly business review

> "Give me a revenue report for last month compared to the month before. How many new customers did I add?"

Claude will pull revenue data and customer metrics to give you a business summary.

## Security

- **OAuth (Claude.ai):** Uses industry-standard OAuth 2.0 with PKCE. No API keys to manage — just log in through your browser.
- **API Keys (Desktop/Code):** Keys are stored locally in your Claude configuration. Never shared with third parties.
- All API calls are authenticated and scoped to your account only.
- API keys can be revoked at any time from **Settings** → **API Keys**.

## Troubleshooting

| Issue | Solution |
|-------|----------|
| Tools not appearing in Claude | Make sure the server built successfully and the path in your config is correct. Restart Claude Desktop. |
| "Authentication failed" | Your API key may have expired. Generate a new one in **Settings** → **API Keys**. |
| OAuth login not working | Make sure you have an active PestProCRM account at [pestprocrm.com](https://www.pestprocrm.com). |
| "Connection refused" | Verify `PESTPRO_API_URL` is correct. For local dev, make sure your app is running. |

## Links

- **PestPro CRM:** <https://www.pestprocrm.com>
- **Documentation:** <https://www.pestprocrm.com/docs>
- **MCP Docs:** <https://www.pestprocrm.com/docs/mcp>
- **MCP Protocol:** <https://modelcontextprotocol.io>

## License

MIT
