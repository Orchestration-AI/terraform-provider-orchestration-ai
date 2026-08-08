---
page_title: "oai_setting Resource - orchestration-ai"
description: A setting is a named configuration value scoped to an agent.
---

# oai_setting

A setting is a named configuration value scoped to an agent. Agent services and scripts can read settings at runtime, making it easy to inject environment-specific values without changing the agent's code or context.

-> Changing `workspace_id`, `orchestration_id`, or `agent_id` destroys and recreates the setting.

## Attribute Reference

| Attribute | Type | Required | Default | Description |
|---|---|---|---|---|
| `id` | string | computed | - | The setting ID |
| `workspace_id` | string | yes | - | ID of the workspace. Forces replacement if changed |
| `orchestration_id` | string | yes | - | ID of the orchestration. Forces replacement if changed |
| `agent_id` | string | yes | - | ID of the agent this setting belongs to. Forces replacement if changed |
| `setting_name` | string | yes | - | The name/key of the setting |
| `setting_description` | string | yes | - | Description of what this setting controls |
| `setting_type` | string | yes | - | The type of the setting value. Typically `Text`, `Secret` or `Boolean` |
| `text_value` | string | no | `""` | The string value of the setting. Used when `setting_type` is `Text` or `Secret` |
| `boolean_value` | bool | no | `false` | The boolean value of the setting. Used when `setting_type` is `Boolean` |

## Example Usage

```hcl
resource "oai_setting" "escalation_email" {
  workspace_id        = oai_workspace.main.id
  orchestration_id    = oai_orchestration.main.id
  agent_id            = oai_agent.support.id
  setting_name        = "escalation_email"
  setting_description = "Email address to escalate unresolved tickets to"
  setting_type        = "Text"
  text_value          = "support-escalations@example.com"
}

resource "oai_setting" "auto_close" {
  workspace_id        = oai_workspace.main.id
  orchestration_id    = oai_orchestration.main.id
  agent_id            = oai_agent.support.id
  setting_name        = "auto_close_resolved"
  setting_description = "Automatically close tickets marked as resolved"
  setting_type        = "Boolean"
  boolean_value       = true
}
```
