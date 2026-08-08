# terraform-provider-orchestration-ai

A Terraform provider for managing [Orchestration AI](https://orchestration-ai.com) resources as infrastructure-as-code.

## Resources supported

| Resource | Description |
|----------|-------------|
| `oai_workspace` | Workspaces |
| `oai_orchestration` | Orchestrations |
| `oai_agent` | Agents |
| `oai_application` | Applications |
| `oai_endpoint` | Agent endpoints |
| `oai_link` | Agent links |
| `oai_setting` | Agent settings |
| `oai_llm_key` | LLM API keys |
| `oai_access` | Access control |
| `oai_ticker_config` | Ticker (cron) configuration |
| `oai_storage_file` | Storage files |
| `oai_storage_dir` | Storage directories |
| `oai_task` | Tasks |

## Data sources

- `oai_llm` - look up a single LLM
- `oai_llms` - list available LLMs
- `oai_service` - look up a service

## Prerequisites

- [Go](https://go.dev) 1.21+
- [Terraform](https://www.terraform.io) 1.5+

## Local development

```bash
# Build
make build

# Install locally (~/.terraform.d/plugins/...)
make install

# Unit tests
make test

# Acceptance tests (requires live credentials)
ORCHESTRATION_AI_CLIENT_ID=<id> ORCHESTRATION_AI_CLIENT_SECRET=<secret> make testacc
```

## Usage example

```hcl
terraform {
  required_providers {
    orchestration_ai = {
      source  = "orchestration-ai/orchestration-ai"
      version = "~> 0.1"
    }
  }
}

provider "oai" {
  # Or set ORCHESTRATION_AI_CLIENT_ID / ORCHESTRATION_AI_CLIENT_SECRET env vars
  client_id     = var.oai_client_id
  client_secret = var.oai_client_secret
}

resource "oai_workspace" "main" {
  workspace_name = "my-workspace"
}

resource "oai_agent" "main" {
  workspace_id      = oai_workspace.main.id
  orchestration_id  = oai_orchestration.main.id
  agent_name        = "my-agent"
  agent_description = "Handles the thing"
}
```

See [`examples/main.tf`](examples/main.tf) for a full example.

## Contributing

1. Fork the repo and create a branch off `qa`
2. Make your changes
3. Open a pull request targeting `qa`
4. Once reviewed and merged, changes deploy to staging automatically
5. Promotion to `main` deploys to production

Please make sure there are no secrets, credentials, or PII in your commits.

## License

MIT
