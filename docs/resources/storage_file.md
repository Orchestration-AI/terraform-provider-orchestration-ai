---
page_title: "oai_storage_file Resource - orchestration-ai"
description: Uploads a file to OAI storage.
---

# oai_storage_file

Uploads a file to OAI storage. Supports both inline text content and binary file uploads from the local filesystem. Exactly one of `content` or `source_path` must be set.

Files are uploaded via a GCS signed URL - the provider requests the signed URL from OAI, then uploads directly to GCS. The `source_hash` attribute tracks the SHA-256 of the uploaded content and triggers a re-upload when it changes.

-> All scope and path fields force replacement if changed.

## Attribute Reference

| Attribute | Type | Required | Default | Description |
|---|---|---|---|---|
| `id` | string | computed | - | Computed as `scope:path` |
| `scope` | string | yes | - | Storage scope. One of: `workspace`, `orchestration`, `agent`, `layer`. Forces replacement if changed |
| `workspace_id` | string | yes | - | ID of the workspace. Forces replacement if changed |
| `orchestration_id` | string | no | `""` | ID of the orchestration. Required when `scope` is `orchestration`, `agent`, or `layer`. Forces replacement if changed |
| `agent_id` | string | no | `""` | ID of the agent. Required when `scope` is `agent` or `layer`. Forces replacement if changed |
| `layer_id` | string | no | `""` | ID of the layer. Required when `scope` is `layer`. Forces replacement if changed |
| `path` | string | yes | - | The destination file path in storage (e.g. `documents/report.txt`). Forces replacement if changed |
| `content` | string | no | - | Inline text content to upload. Mutually exclusive with `source_path` |
| `source_path` | string | no | - | Path to a local file to upload. Supports binary files (`.pdf`, `.docx`, etc). Mutually exclusive with `content` |
| `source_hash` | string | computed | - | SHA-256 hash of the uploaded content. Automatically tracked - changes trigger a re-upload |

## Example Usage

Inline text file:

```hcl
resource "oai_storage_file" "prompt" {
  scope            = "agent"
  workspace_id     = oai_workspace.main.id
  orchestration_id = oai_orchestration.main.id
  agent_id         = oai_agent.support.id
  path             = "prompts/system.txt"
  content          = "You are a helpful support agent. Always be concise."
}
```

Binary file upload from local disk:

```hcl
resource "oai_storage_file" "handbook" {
  scope        = "workspace"
  workspace_id = oai_workspace.main.id
  path         = "docs/employee-handbook.pdf"
  source_path  = "${path.module}/assets/employee-handbook.pdf"
}
```
