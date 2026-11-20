# DICE MCP server for ChatGPT and Claude

Connect ChatGPT, Claude and any AI agent to your DICE promoter account through Cotlet.dev. The live integration guide documents 15 hosted operations for events, ticket tiers, sales and guest lists.

## What can I ask?

> Summarize weekly ticket sales by ticket type, with returns and transfers.

> Prepare an event draft from my booking brief.

> Show the current price tiers and prepare the next ticket release for my approval.

> Export the door list for tonight's event.

> Draft a door-time update and show it to me before sending it to ticket holders.

## Connect ChatGPT and Claude

1. [Get access](https://cotlet.dev/signup?app=dice).
2. Open DICE in the Cotlet.dev Cloud Browser, sign in to your own MIO account and enable it for agents.
3. Add `https://cotlet.dev/mcp/v1/connect` as the connector URL in ChatGPT or Claude and sign in with Cotlet.dev.

Codex, Claude Code and other clients using an API key connect to `https://cotlet.dev/mcp/v1`. Create a key in the Cotlet.dev console and configure your client:

```json
{
  "mcpServers": {
    "cotlet": {
      "url": "https://cotlet.dev/mcp/v1",
      "headers": {
        "Authorization": "Bearer ${COTLET_API_KEY}"
      }
    }
  }
}
```

[Current setup and full DICE guide](https://cotlet.dev/integrations/dice-api-mcp-server?utm_source=github&utm_medium=readme&utm_campaign=dice)

## Hosted operations

The live page documents these operations through `dice_read` and `dice_write`:

- `list_events`
- `get_event`
- `create_event`
- `submit_event`
- `update_event`
- `cancel_event`
- `add_ticket_type`
- `add_price_tier`
- `update_ticket_type`
- `get_sales_summary`
- `list_orders`
- `list_ticket_holders`
- `list_returns`
- `list_transfers`
- `message_attendees`

Creating an event saves a draft that fans cannot see. Submissions, event edits, prices, allocations, messages and cancellations ask for confirmation by default; you can change this per tool. DICE reviews submitted events before they can go live. Review each proposed change before approving it. Payouts, bank details, team members and account settings are outside these tools.

## Run the local stdio bridge

This repository includes a Python bridge to Cotlet.dev. It requires Python 3.10 or newer and uses the standard library.

```bash
export COTLET_API_KEY="your-key"
python3 dice_agent.py serve
```

The local bridge exposes seven browser helper tools: `dice_guide`, `dice_status`, `dice_open`, `dice_read`, `dice_click`, `dice_type` and `dice_close`. The hosted connector exposes the application operations listed above. Use the hosted connector for those operations.

```bash
docker build -t dice-mcp .
docker run -i --rm -e COTLET_API_KEY dice-mcp
```

Without `COTLET_API_KEY`, a tool call returns instructions for obtaining a key. Keep the key out of source control.

## Does DICE have an API or an official MCP server?

The live guide's check dated 27 October 2026 describes the official Ticket Holders API as a read-only GraphQL API for partners. It reports no official DICE MCP server. The guide also describes a third-party CLI and MCP server that reads through that API. Use the official API or DICE integrations first when they cover your task.

## Is this affiliated with DICE?

Cotlet.dev is independent and is not affiliated with, endorsed by or sponsored by DICE. DICE is a trademark of its owner. You use your own DICE account and its existing permissions.

[Get access](https://cotlet.dev/signup?app=dice)
