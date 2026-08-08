---
page_title: "oai_llm Data Source - orchestration-ai"
description: Looks up a single LLM by name and returns its OAI-assigned ID.
---

# oai_llm

Looks up a single LLM by name and returns its OAI-assigned ID. Use this to populate `llm_id` on `oai_layer` without hardcoding IDs that differ per account.

-> LLMs become available after an `oai_llm_key` is created. Allow up to 1 minute for discovery before referencing this data source.

## Attribute Reference

| Attribute | Type | Required | Description |
|---|---|---|---|
| `llm_name` | string | yes | The name of the LLM to look up (e.g. `gpt-4o`, `gemini-2.0-flash`) |
| `id` | string | computed | The OAI-assigned ID for this LLM |

## Example Usage

```hcl
data "oai_llm" "gpt4o" {
  llm_name = "gpt-4o"
}

resource "oai_layer" "main" {
  # ...
  llm_id = data.oai_llm.gpt4o.id
}
```
