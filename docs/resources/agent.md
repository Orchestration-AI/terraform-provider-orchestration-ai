---
page_title: "oai_agent Resource - orchestration-ai"
description: An agent is an AI unit within an orchestration.
---

# oai_agent

An agent is an AI unit within an orchestration. It has a name, a description, and optionally a VM for running custom JavaScript.

-> Changing `workspace_id` or `orchestration_id` destroys and recreates the agent.

## Attribute Reference

| Attribute | Type | Required | Default | Description |
|---|---|---|---|---|
| `id` | string | computed | - | The agent ID |
| `workspace_id` | string | yes | - | ID of the workspace. Forces replacement if changed |
| `orchestration_id` | string | yes | - | ID of the orchestration. Forces replacement if changed |
| `agent_name` | string | yes | - | Display name for the agent |
| `agent_description` | string | yes | - | Description of what this agent does. This is what the LLM uses to understand the agent's role |
| `vm_enabled` | bool | no | `false` | Whether to enable the JavaScript VM for this agent |
| `script_source` | string | no | `""` | JavaScript source code to run in the agent VM. Only used when `vm_enabled` is `true` |
| `script_package_json` | string | no | `""` | `package.json` content for the agent VM script. Only used when `vm_enabled` is `true` |

## Example Usage

Basic agent:

```hcl
resource "oai_agent" "support" {
  workspace_id      = oai_workspace.main.id
  orchestration_id  = oai_orchestration.main.id
  agent_name        = "Support Agent"
  agent_description = "Handles inbound customer support tickets and routes them to the right team"
}
```

Agent with a VM script:

```hcl
resource "oai_agent" "processor" {
  workspace_id        = oai_workspace.main.id
  orchestration_id    = oai_orchestration.main.id
  agent_name          = "Data Processor"
  agent_description   = "Processes and transforms incoming data payloads"
  vm_enabled          = true
  script_source       = file("${path.module}/scripts/processor.js")
  script_package_json = file("${path.module}/scripts/package.json")
}
```
