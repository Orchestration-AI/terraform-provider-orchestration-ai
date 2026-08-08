---
page_title: "oai_task Resource - orchestration-ai"
description: A task is a message sent to an agent on a schedule or as a one-off instruction.
---

# oai_task

A task is a message sent to an agent on a schedule or as a one-off instruction. Tasks are immutable after creation - changing `message` or `cron_expression` requires destroying and recreating the resource.

-> Changing `workspace_id`, `orchestration_id`, or `agent_id` destroys and recreates the task.

## Attribute Reference

| Attribute | Type | Required | Default | Description |
|---|---|---|---|---|
| `id` | string | computed | - | The task ID |
| `workspace_id` | string | yes | - | ID of the workspace. Forces replacement if changed |
| `orchestration_id` | string | yes | - | ID of the orchestration. Forces replacement if changed |
| `agent_id` | string | yes | - | ID of the agent to send the task to. Forces replacement if changed |
| `message` | string | yes | - | The message/instruction to send to the agent |
| `cron_expression` | string | no | `""` | A cron expression for scheduling the task (e.g. `0 9 * * 1-5` for weekdays at 9am UTC). Leave empty for a one-off task |

## Example Usage

One-off task:

```hcl
resource "oai_task" "onboarding" {
  workspace_id     = oai_workspace.main.id
  orchestration_id = oai_orchestration.main.id
  agent_id         = oai_agent.support.id
  message          = "Review the open support tickets and send a daily summary to the team."
}
```

Scheduled task:

```hcl
resource "oai_task" "daily_summary" {
  workspace_id     = oai_workspace.main.id
  orchestration_id = oai_orchestration.main.id
  agent_id         = oai_agent.support.id
  message          = "Generate and send the daily support metrics report."
  cron_expression  = "0 9 * * 1-5"
}
```
