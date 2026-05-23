# Blog

My personal blog, built with Hugo and served as a Docker container.

Live at: **https://blog.gcourtot.fr**

## Stack

| Component  | Technology |
|------------|------------|
| Framework  | Hugo |
| Server     | Apache HTTPd (Docker image `httpd:alpine`) |
| CI/CD      | GitHub Actions |
| Registry   | Docker Hub |
| Deployment | n8n (webhook → Watchtower) |

## Run locally

```bash
docker run --rm -v $(pwd):/src -w /src ghcr.io/gohugoio/hugo:latest server
# Open http://localhost:1313
```

## CI/CD

### Pull Request → `main`

1. Build the Hugo static site
2. Build the Docker image
3. Start the container
4. Verify that `/version.txt` contains the correct commit SHA

### Push to `main`

1. Tag the current `latest` image as `previous` (for rollback)
2. Build the Hugo static site
3. Build and push the new `latest` image to Docker Hub
4. Trigger deployment via n8n webhook
5. Verify in production that `/version.txt` matches the expected SHA
6. **Automatic rollback** if the production check fails: `previous` is re-tagged as `latest` and redeployed

### Required secrets

| Secret | Description |
|--------|-------------|
| `DOCKERHUB_USERNAME` | Docker Hub username |
| `DOCKERHUB_TOKEN`    | Docker Hub access token |
| `N8N_WEBHOOK_ID`     | n8n webhook ID triggering the redeployment |