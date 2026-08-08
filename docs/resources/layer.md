---
page_title: "oai_layer Resource - orchestration-ai"
description: A layer is the configuration block attached to an agent, defining the system prompt, LLM, temperature, and services.
---

# oai_layer

A layer is the configuration block attached to an agent. It defines the system prompt (`context_md`), the LLM to use, the temperature, and which services the agent has access to. An agent can have multiple layers.

-> Changing `workspace_id`, `orchestration_id`, or `agent_id` destroys and recreates the layer.

## Attribute Reference

| Attribute | Type | Required | Default | Description |
|---|---|---|---|---|
| `id` | string | computed | - | The layer ID |
| `workspace_id` | string | yes | - | ID of the workspace. Forces replacement if changed |
| `orchestration_id` | string | yes | - | ID of the orchestration. Forces replacement if changed |
| `agent_id` | string | yes | - | ID of the agent this layer belongs to. Forces replacement if changed |
| `layer_name` | string | yes | - | Display name for the layer |
| `context_md` | string | no | `""` | System prompt / context for the agent written in Markdown |
| `temperature` | number | no | `0.7` | LLM sampling temperature (0.0–2.0). Lower = more deterministic |
| `llm_id` | string | no | `""` | ID of the LLM to use. Look up the ID by name using `data.oai_llm`. LLMs become available after an `oai_llm_key` is created - allow up to 1 minute for discovery |
| `service_ids` | set(string) | no | - | IDs of services to attach to this layer. Agents can call these services as tools |

## Example Usage

```hcl
resource "oai_layer" "main" {
  workspace_id     = oai_workspace.main.id
  orchestration_id = oai_orchestration.main.id
  agent_id         = oai_agent.support.id
  layer_name       = "Main Layer"
  context_md       = <<-EOT
    You are a helpful customer support agent.
    Always be polite and concise.
    Escalate to a human if the issue cannot be resolved in 3 messages.
  EOT
  temperature      = 0.5
  llm_id           = data.oai_llm.gemini.id
  service_ids      = [data.oai_service.messaging.id]
}
```
