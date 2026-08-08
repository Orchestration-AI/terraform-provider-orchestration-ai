---
page_title: "oai_access Resource - orchestration-ai"
description: Grants a principal access to a resource at a specific role.
---

# oai_access

Grants a principal (a user or service account) access to a resource at a specific role. Access grants are immutable - changing any field requires destroying and recreating the resource.

-> `principal_id`, `principal_name`, `principal_email`, and `resource_id` all force replacement if changed.

## Attribute Reference

| Attribute | Type | Required | Default | Description |
|---|---|---|---|---|
| `id` | string | computed | - | The access grant ID |
| `principal_id` | string | yes | - | The ID of the principal being granted access. Forces replacement if changed |
| `principal_name` | string | yes | - | Display name of the principal. Forces replacement if changed |
| `principal_email` | string | yes | - | Email address of the principal. Forces replacement if changed |
| `resource_id` | string | yes | - | ID of the resource to grant access to (e.g. a workspace ID). Forces replacement if changed |
| `role` | string | yes | - | The role to grant. Refer to the OAI roles documentation for available values |

## Example Usage

```hcl
resource "oai_access" "team_member" {
  principal_id    = var.team_member_id
  principal_name  = "Jane Smith"
  principal_email = "jane@example.com"
  resource_id     = oai_workspace.main.id
  role            = "workspace_editor"
}
```
