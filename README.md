# OfferFetcher Action

> **Note:** This action uses a private Docker image. It can only be used by repositories under the `kaspioffers` account.

Fetch offers from Kaspi marketplace as part of your GitHub Actions workflows.

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
        uses: kaspioffers/OfferFetcher-action@v1
        with:
          database-connection-string: ${{ secrets.DATABASE_CONNECTION_STRING }}
          batch-size: '100'
          scan-interval-minutes: '15'
```

## Inputs

| Input | Description | Required | Default |
|-------|-------------|----------|---------|
| `database-connection-string` | PostgreSQL database connection string | ✅ Yes | - |
| `timescaledb-connection-string` | TimescaleDB connection string | ⚠️ No | - |
| `batch-size` | Number of offers to fetch per batch | ⚠️ No | `100` |
| `scan-interval-minutes` | Minutes between scan intervals | ⚠️ No | `15` |
| `api-timeout` | Maximum runtime in seconds | ⚠️ No | `300` |
| `proxy-url` | Proxy server URL | ⚠️ No | - |
| `proxy-username` | Proxy username | ⚠️ No | - |
| `proxy-password` | Proxy password | ⚠️ No | - |

## Outputs

| Output | Description |
|--------|-------------|
| `status` | Operation status: `success` or `failure` |
| `message` | Detailed message about the operation |

## Requirements

- PostgreSQL database accessible from GitHub Actions
- Repository must be under the `kaspioffers` account (private Docker image)

## Example with All Options

```yaml
- name: Fetch Offers
  uses: kaspioffers/OfferFetcher-action@v1
  with:
    database-connection-string: ${{ secrets.DATABASE_CONNECTION_STRING }}
    timescaledb-connection-string: ${{ secrets.TIMESCALEDB_CONNECTION_STRING }}
    proxy-url: ${{ secrets.PROXY_URL }}
    proxy-username: ${{ secrets.PROXY_USERNAME }}
    proxy-password: ${{ secrets.PROXY_PASSWORD }}
    batch-size: '200'
    scan-interval-minutes: '30'
    api-timeout: '600'
```

## License

See LICENSE file.
