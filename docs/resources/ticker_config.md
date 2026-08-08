---
page_title: "oai_ticker_config Resource - orchestration-ai"
description: Configures the ticker for a workspace, orchestration, or agent.
---

# oai_ticker_config

Configures the ticker for a workspace, orchestration, or agent. The ticker restricts tasks to fire at a set cadence and can be restricted to specific working hours per day of the week.

The API is upsert-based - create and update both call the same `PUT` endpoint. There is no delete endpoint, so removing this resource from your config removes it from Terraform state only.

## Attribute Reference

| Attribute | Type | Required | Default | Description |
|---|---|---|---|---|
| `id` | string | computed | - | The ticker config ID |
| `scope` | string | yes | - | The scope this ticker applies to. One of: `workspace`, `orchestration`, `agent`. Forces replacement if changed |
| `workspace_id` | string | yes | - | ID of the workspace. Forces replacement if changed |
| `orchestration_id` | string | no | `""` | ID of the orchestration. Required when `scope` is `orchestration` or `agent` |
| `agent_id` | string | no | `""` | ID of the agent. Required when `scope` is `agent` |
| `enabled` | bool | no | `true` | Whether the ticker is active |
| `cadence_minutes` | number | yes | - | How often the ticker fires, in minutes |
| `inherit` | bool | no | `false` | When `true`, inherits ticker config from the parent scope instead of using its own |
| `work_hours` | object | no | - | Optional working hours schedule. Omit entirely to run the ticker at all hours |

### `work_hours` nested block

Each day of the week is an optional nested block. Omitting a day disables the ticker on that day entirely.

| Attribute | Type | Required | Description |
|---|---|---|---|
| `sunday` | object | no | Working hours for Sunday |
| `monday` | object | no | Working hours for Monday |
| `tuesday` | object | no | Working hours for Tuesday |
| `wednesday` | object | no | Working hours for Wednesday |
| `thursday` | object | no | Working hours for Thursday |
| `friday` | object | no | Working hours for Friday |
| `saturday` | object | no | Working hours for Saturday |

Each day object has:

| Attribute | Type | Required | Description |
|---|---|---|---|
| `start` | number | yes | Start hour in UTC (0–23) |
| `end` | number | yes | End hour in UTC (0–23) |

## Example Usage

Workspace-scoped ticker, runs every 5 minutes:

```hcl
resource "oai_ticker_config" "workspace" {
  scope           = "workspace"
  workspace_id    = oai_workspace.main.id
  enabled         = true
  cadence_minutes = 5
}
```

Agent-scoped ticker, runs every 30 minutes, weekdays only, 9am–5pm UTC:

```hcl
resource "oai_ticker_config" "agent_weekdays" {
  scope            = "agent"
  workspace_id     = oai_workspace.main.id
  orchestration_id = oai_orchestration.main.id
  agent_id         = oai_agent.support.id
  enabled          = true
  cadence_minutes  = 30

  work_hours = {
    monday    = { start = 9, end = 17 }
    tuesday   = { start = 9, end = 17 }
    wednesday = { start = 9, end = 17 }
    thursday  = { start = 9, end = 17 }
    friday    = { start = 9, end = 17 }
  }
}
```
