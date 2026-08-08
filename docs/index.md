---
page_title: "Provider: Orchestration AI"
description: The Orchestration AI provider lets you manage your entire OAI infrastructure as code - workspaces, orchestrations, agents, layers, storage, access control, and more.
---

# Orchestration AI Provider

The Orchestration AI provider lets you manage your entire OAI infrastructure as code - workspaces, orchestrations, agents, layers, storage, access control, and more.

## Provider Configuration

```hcl
terraform {
  required_providers {
    oai = {
      source  = "orchestration-ai/orchestration-ai"
      version = "~> 0.1"
    }
  }
}

provider "oai" {
  client_id     = var.oai_client_id
  client_secret = var.oai_client_secret
}
```

You can also use environment variables instead of hardcoding credentials:

```bash
export ORCHESTRATION_AI_CLIENT_ID=your-client-id
export ORCHESTRATION_AI_CLIENT_SECRET=your-client-secret
```

## Argument Reference

| Argument | Required | Description |
|---|---|---|
| `client_id` | Yes | Your OAI client ID. Can be set via `ORCHESTRATION_AI_CLIENT_ID` |
| `client_secret` | Yes | Your OAI client secret. Can be set via `ORCHESTRATION_AI_CLIENT_SECRET` |
