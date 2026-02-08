# OfferFetcher Action

## Inputs

| Input | Description | Required | Default |
|-------|-------------|----------|---------|
| `database-connection-string` | PostgreSQL database connection string | ✅ Yes | - |
| `timescaledb-connection-string` | TimescaleDB connection string | ✅ Yes | - |
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
