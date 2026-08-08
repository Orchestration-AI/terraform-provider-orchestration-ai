---
page_title: "oai_llm_key Resource - orchestration-ai"
description: Registers OAuth credentials for an LLM provider.
---

# oai_llm_key

Registers OAuth credentials for an LLM provider. After creation, OAI asynchronously discovers the available models for that provider - allow up to 1 minute before referencing an `llm_id` in `oai_layer`.

-> There is no delete endpoint for LLM keys. Removing this resource from your config will remove it from Terraform state but will not delete it from OAI.

## Attribute Reference

| Attribute | Type | Required | Default | Description |
|---|---|---|---|---|
| `id` | string | computed | - | The LLM key ID |
| `client_id` | string | yes | - | OAuth client ID for the LLM provider |
| `client_secret` | string | yes | - | OAuth client secret. Marked sensitive - never stored in plain text in state |
| `llm_provider` | string | yes | - | The LLM provider. One of: `Google`, `GoogleOAI`, `OpenAI`, `Anthropic` |

## Example Usage

```hcl
resource "oai_llm_key" "openai" {
  client_id     = var.openai_client_id
  client_secret = var.openai_client_secret
  llm_provider  = "OpenAI"
}

resource "oai_llm_key" "google" {
  client_id     = var.google_client_id
  client_secret = var.google_client_secret
  llm_provider  = "Google"
}
```
