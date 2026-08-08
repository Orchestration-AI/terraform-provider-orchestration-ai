---
page_title: "oai_workspace Resource - orchestration-ai"
description: A workspace is the top-level container for all your orchestrations and access control. Everything else lives inside a workspace.
---

# oai_workspace

A workspace is the top-level container for all your orchestrations and access control. Everything else lives inside a workspace.

## Attribute Reference

| Attribute | Type | Required | Default | Description |
|---|---|---|---|---|
| `id` | string | computed | - | The workspace ID |
| `workspace_name` | string | yes | - | Display name for the workspace |
| `applications` | set(string) | no | - | Set of application client IDs that have access to this workspace |

## Example Usage

```hcl
resource "oai_workspace" "main" {
  workspace_name = "my-workspace"
}
```

With applications:

```hcl
resource "oai_application" "app" {
  application_name           = "my-app"
  application_description_md = "My application"
  application_url            = "https://my-app.example.com"
  access_key                 = "my-secret-key"
}

resource "oai_workspace" "main" {
  workspace_name = "my-workspace"
  applications   = [oai_application.app.id]
}
```
