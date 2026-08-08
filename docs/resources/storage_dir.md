---
page_title: "oai_storage_dir Resource - orchestration-ai"
description: Creates a directory in OAI storage at a given scope.
---

# oai_storage_dir

Creates a directory in OAI storage at a given scope. Directories are immutable - changing any field destroys and recreates the resource.

## Attribute Reference

| Attribute | Type | Required | Default | Description |
|---|---|---|---|---|
| `id` | string | computed | - | Computed as `scope:path` |
| `scope` | string | yes | - | Storage scope. One of: `workspace`, `orchestration`, `agent`, `layer`. Forces replacement if changed |
| `workspace_id` | string | yes | - | ID of the workspace. Forces replacement if changed |
| `orchestration_id` | string | no | `""` | ID of the orchestration. Required when `scope` is `orchestration`, `agent`, or `layer`. Forces replacement if changed |
| `agent_id` | string | no | `""` | ID of the agent. Required when `scope` is `agent` or `layer`. Forces replacement if changed |
| `layer_id` | string | no | `""` | ID of the layer. Required when `scope` is `layer`. Forces replacement if changed |
| `path` | string | yes | - | The directory path to create (e.g. `documents/reports`). Forces replacement if changed |

## Example Usage

```hcl
resource "oai_storage_dir" "reports" {
  scope            = "agent"
  workspace_id     = oai_workspace.main.id
  orchestration_id = oai_orchestration.main.id
  agent_id         = oai_agent.support.id
  path             = "documents/reports"
}
```
