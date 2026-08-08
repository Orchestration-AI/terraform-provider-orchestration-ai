---
page_title: "oai_llms Data Source - orchestration-ai"
description: Fetches the full list of LLMs available to your account.
---

# oai_llms

Fetches the full list of LLMs available to your account. Useful for inspecting what models are available after creating an `oai_llm_key`.

## Attribute Reference

| Attribute | Type | Description |
|---|---|---|
| `llms` | list(object) | List of available LLMs, each with `id` and `llm_name` |

## Example Usage

```hcl
data "oai_llms" "all" {}

output "available_llms" {
  value = data.oai_llms.all.llms
}
```
