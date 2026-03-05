# OfferFetcher Action

> **Note:** This action uses a **private Docker image** and requires authentication via Personal Access Token (PAT).

Fetch offers as part of your GitHub Actions workflows.

## Setup

## Inputs

| Input | Description | Required | Default |
|-------|-------------|----------|---------|
| `ghcr-token` | GitHub PAT with `read:packages` permission | ✅ Yes | - |
| `database-connection-string` | PostgreSQL connection string | ✅ Yes | - |
| `batch-size` | Number of offers per batch | ⚠️ No | `100` |
| `scan-interval-minutes` | Minutes between scans | ⚠️ No | `15` |
| `api-timeout` | Maximum runtime in seconds | ⚠️ No | `300` |
| `proxy-url` | Proxy server URL | ⚠️ No | - |
| `proxy-username` | Proxy username | ⚠️ No | - |
| `proxy-password` | Proxy password | ⚠️ No | - |

## Outputs

| Output | Description |
|--------|-------------|
| `status` | Operation status: `success` or `failure` |
| `message` | Detailed message about the operation |
