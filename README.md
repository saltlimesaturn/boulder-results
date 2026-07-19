# boulder-results

## Migrate local result publishing to a cloud JSON endpoint

To keep your existing Python pipeline and satisfy Reddit security checks, publish your JSON to an approved cloud host and post using that hosted URL.

### 1) Use an approved host

Use a major cloud provider endpoint (for example: AWS S3 + CloudFront, Google Cloud Storage, Azure Blob Storage, or Cloudflare R2) instead of a local or personal URL.

### 2) Configure the endpoint URL in Python

Store the hosted JSON URL in an environment variable so your current code needs minimal changes:

```python
import os

RESULTS_JSON_URL = os.environ["RESULTS_JSON_URL"]  # e.g. https://cdn.example.com/results/latest.json
```

### 3) Keep your existing push flow

Generate JSON exactly as you do now, upload it to the cloud location, then push `RESULTS_JSON_URL` to the app/integration that consumes it.