---
name: whatsapp-business
description: Use when the user asks to do anything with their WhatsApp Business account through WA Smart Sender — reading or replying to customer conversations, contacts and tags, message templates, broadcast campaigns, AI agents, flows, orders or messaging analytics.
---

# Working in a WA Smart Sender workspace

WA Smart Sender runs a business's official WhatsApp Business (Meta Cloud API) account. The `wasmartsender` MCP server gives you its tools. The first time you use them, the person is sent to sign in and approve the connection in their browser.

## Start every session the same way

1. Call `get_my_access` to see the workspace, the person's role, and whether the plan allows changes (MCP access can be full, read-only or off).
2. Call `list_connections`. Almost every other tool needs a `connectionId` (a WhatsApp number). If there are several, ask which one, unless the request already makes it clear.
3. When you are unsure how something works (how flows trigger, how agents and Quick Rules share messages, what a template category means), call `get_system_guide` before guessing.
4. Only the everyday tools are listed at first. To do something else, call `search_tools` with what you want to do (for example "pause a sequence") and then call the tool it returns.

## Rules that protect the business

- **Anything a customer will see needs a clear yes from the person first.** That covers `send_message`, `start_campaign`, `resend_failed_campaign_messages` and `start_flow_for_contact`. Show exactly what will be sent and to whom, plus the cost estimate for campaigns (`get_campaign_cost_estimate`), then wait for approval.
- **WhatsApp's 24-hour window.** Free-form text only reaches a customer who wrote in during the last 24 hours. Outside that window, use an approved template (`list_templates`, look for status APPROVED). If a send fails for this reason, say so plainly and offer a template.
- **Tools marked confirm** (deletes, publishing, merges) are refused unless the call carries `confirm: true`. Only pass it after the person has agreed to that specific action.
- **Never invent ids.** Get them from list or get tools.
- **Errors explain themselves.** A failed tool returns a code and a message. Read it and tell the person what to do: upgrade, pick another number, use a template, or ask the workspace owner.

## Common jobs

| The person asks                           | Do this                                                                                                                                                                       |
| ----------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| "What needs my attention?"                | `list_unanswered_messages`, then `list_conversations` with status open. Summarise by urgency.                                                                                 |
| "Reply to Ahmed"                          | `list_conversations` / `get_conversation_transcript` → draft → confirm → `send_message`.                                                                                      |
| "Send the Ramadan offer to VIP customers" | `list_templates` → `list_campaign_audiences` or `list_segments` → `create_campaign` → `upload_campaign_contacts` → `get_campaign_cost_estimate` → confirm → `start_campaign`. |
| "How did last week go?"                   | `get_analytics_overview`, `get_message_analytics`, `get_campaign_analytics`.                                                                                                  |
| "Make the bot answer delivery questions"  | `list_agents` → `get_agent` → add knowledge (`create_kb_entry`) → test with `test_agent_turn` before anything goes live.                                                      |

Reply in the language the person writes in. Many WA Smart Sender customers write in Arabic.
