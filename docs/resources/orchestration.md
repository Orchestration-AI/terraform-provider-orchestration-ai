---
page_title: "oai_orchestration Resource - orchestration-ai"
description: An orchestration is a logical grouping of agents that work together toward a shared goal.
---

# oai_orchestration

An orchestration is a logical grouping of agents that work together toward a shared goal. It lives inside a workspace.

-> Changing `workspace_id` destroys and recreates the orchestration.

## Attribute Reference

| Attribute | Type | Required | Default | Description |
|---|---|---|---|---|
| `id` | string | computed | - | The orchestration ID |
| `workspace_id` | string | yes | - | ID of the workspace this orchestration belongs to. Forces replacement if changed |
| `orchestration_name` | string | yes | - | Display name for the orchestration |
| `orchestration_description` | string | yes | - | Description of what this orchestration does |

## Example Usage

```hcl
resource "oai_orchestration" "main" {
  workspace_id              = oai_workspace.main.id
  orchestration_name        = "customer-support"
  orchestration_description = "Handles inbound customer support requests"
}
```
