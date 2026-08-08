---
page_title: "oai_application Resource - orchestration-ai"
description: An application is a deployed service that exposes tools agents can call.
---

# oai_application

An application is a deployed service that exposes tools agents can call. Once created, the application's ID can be added to a workspace's `applications` list to grant it access.

## Attribute Reference

| Attribute | Type | Required | Default | Description |
|---|---|---|---|---|
| `id` | string | computed | - | The application client ID |
| `application_name` | string | yes | - | Display name for the application |
| `application_description_md` | string | yes | - | Description of the application written in Markdown. Agents use this to understand what the app does |
| `application_url` | string | yes | - | The base URL where the application is deployed |
| `access_key` | string | yes | - | Secret key used to authenticate requests from your application to OAI |
| `private` | bool | no | `false` | When `true`, the application is only visible to workspaces it has been explicitly added to |
| `visible` | bool | no | `true` | When `true`, the application is public for other OAI orchestrators to use (Needs approval) |

## Example Usage

```hcl
resource "oai_application" "shared_services" {
  application_name           = "Shared Services"
  application_description_md = "Provides messaging, storage, and utility tools for all agents."
  application_url            = "https://make-oai.orchestration-ai.deno.net"
  access_key                 = var.oai_access_key
  private                    = false
  visible                    = true
}
```
