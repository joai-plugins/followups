---
name: use-followups
description: Use the Followups JoAi app plugin when the task needs Followups tools or workflows.
---

# Followups

Connect Followups to Claude, Cursor, and ChatGPT through JoAi's hosted MCP app server.

If a specific task was given, identify the relevant MCP tool and call it immediately — no preamble.

If invoked with no task, call the authenticate tool first (if present), then list the available actions concisely so the user can pick one.

Never ask "what would you like to do?" — either act on the task or show the menu.

## Example Prompts

- List the Followups tools available in this app.
- Explain what setup or authentication Followups needs before I run an action.
- Use Followups to help me with the task I describe next.

## Action Inventory

- `followups-birthday` (collect, prompt, collect) — Send a birthday greeting to a customer, optionally with a special offer.
- `followups-birthday-scan` (collect) — Automatically identify customers with birthdays in the next 7 days.
- `followups-check-in` (collect, prompt, collect) — Send a friendly check-in message to a customer you haven't heard from recently.
- `followups-dashboard` (collect, collect, collect) — View and manage your follow-up pipeline. See enrolled contacts, their current sequence step, and reply status in one overview.
- `followups-enroll` (collect, collect, collect) — Enroll a CRM contact into a follow-up sequence by setting the sequence name and step. The host system schedules execution of the appropriate template.
- `followups-execute-step` (collect, collect, prompt, collect, collect) — Execute one step of a follow-up sequence for a contact: fetch the contact and matching template, personalize the message, send or log it depending on channel, then advance the contact to the next step.
- `followups-handle-reply` (collect, inline) — Record that a contact replied to a follow-up message. Tags the contact as 'followups-replied' so the sequence can be stopped and the response handled appropriately.
- `followups-inactive-scan` (collect, prompt) — Automatically identify customers who haven't visited in 30+ days and suggest follow-up actions.
- `followups-post-treatment` (collect, prompt, collect) — Send aftercare tips and instructions to a customer following their treatment.
- `followups-reorder-reminder` (collect, prompt, collect) — Remind a customer that it's time to reorder a product they purchased previously.
- `followups-sequence-remove` (collect, collect, collect, inline) — Remove a contact from a follow-up sequence. Clears the sequence properties, removes the enrolled tag, and logs the removal as an activity. Use this when a contact opts out or was enrolled by mistake.
- `followups-template-create` (collect) — Create a reusable follow-up message template with structured metadata like channel, sequence step, and delay. Pre-fills type=template and app=followups, then chains to the generic document-create warp so the actual storage logic stays in one place.
- ...and 4 more actions exposed by the hosted MCP app server.

## Usage Notes

- Every listed action becomes an MCP tool when the app server is connected.
- Prefer the generated provider plugin when one is available, and fall back to the raw MCP URL otherwise.

## Auth Notes

- Some actions require provider credentials or OAuth on first use.
