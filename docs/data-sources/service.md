---
page_title: "oai_service Data Source - orchestration-ai"
description: Looks up a single service by name and returns its ID.
---

# oai_service

Looks up a single service by name and returns its ID. Use this to populate `service_ids` on `oai_layer` without hardcoding IDs.

## Attribute Reference

| Attribute | Type | Required | Description |
|---|---|---|---|
| `service_name` | string | yes | The name of the service to look up (e.g. `messaging`, `mail`) |
| `id` | string | computed | The OAI-assigned ID for this service |

## Example Usage

```hcl
data "oai_service" "messaging" {
  service_name = "messaging"
}

resource "oai_layer" "main" {
  # ...
  service_ids = [data.oai_service.messaging.id]
}
```
