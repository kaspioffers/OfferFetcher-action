# OfferFetcher Action

> **Note:** This action uses a **private Docker image** and requires authentication via Personal Access Token (PAT).

Fetch offers from Kaspi marketplace as part of your GitHub Actions workflows.

## Setup

### 1. Create a Personal Access Token

1. Go to https://github.com/settings/tokens
2. Click **"Generate new token"** → **"Generate new token (classic)"**
3. Give it a name: `OfferFetcher GHCR Access`
4. Select expiration (recommend: 90 days or No expiration)
5. Select scopes:
   - ✅ `read:packages` (required)
6. Click **"Generate token"**
7. **Copy the token immediately** (you won't see it again!)

### 2. Add Token as Repository Secret

1. Go to your repository settings → Secrets → Actions
2. Click **"New repository secret"**
3. Name: `GHCR_TOKEN`
4. Value: Paste your PAT
5. Click **"Add secret"**

## Usage

```yaml
name: Fetch Offers

on:
  schedule:
    - cron: '0 * * * *'  # Run every hour
  workflow_dispatch:

jobs:
  fetch-offers:
    runs-on: ubuntu-latest
    steps:
      - name: Fetch Kaspi Offers
        uses: kaspioffers/OfferFetcher-action@main
        with:
          ghcr-token: ${{ secrets.GHCR_TOKEN }}
          database-connection-string: ${{ secrets.DATABASE_CONNECTION_STRING }}
          timescaledb-connection-string: ${{ secrets.TIMESCALEDB_CONNECTION_STRING }}
          proxy-url: ${{ secrets.PROXY_URL }}
          proxy-username: ${{ secrets.PROXY_USERNAME }}
          proxy-password: ${{ secrets.PROXY_PASSWORD }}
          batch-size: '100'
          scan-interval-minutes: '15'
```

## Inputs

| Input | Description | Required | Default |
|-------|-------------|----------|---------|
| `ghcr-token` | GitHub PAT with `read:packages` permission | ✅ Yes | - |
| `database-connection-string` | PostgreSQL connection string | ✅ Yes | - |
| `timescaledb-connection-string` | TimescaleDB connection string | ⚠️ No | - |
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

## Security Notes

- ✅ PAT is never exposed in logs
- ✅ Docker logout happens automatically after run
- ✅ Token only needs `read:packages` permission
- ⚠️ Rotate your PAT periodically
- ⚠️ Set an expiration date on your PAT

## Troubleshooting

### "Error: Invalid credentials"
- Verify the PAT has `read:packages` scope
- Check the token hasn't expired
- Ensure the secret name is exactly `GHCR_TOKEN`

### "Error: unauthorized"
- Verify the Docker image exists
- Check the package visibility settings

## License

See LICENSE file.
