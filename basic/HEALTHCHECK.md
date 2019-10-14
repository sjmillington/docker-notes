## Healthchecks

It expects a `0` (Good) or `1` (Error)

3 states:

- Starting
- Healthy
- Unhealthy

Not a replacement for monitoring

Status shows up with `docker container ls`

We can view the last 5 healthchecks with `docker container inspect`

### Healthcheck from Command Line

```
docker run \
  --health-cmd="curl -f localhost:9200/_cluster/health || false" \
  --health-interval=5s \
  --health-retries=3 \
  --health-timeout=2s \
  --health-start-period=15s \
  elasticsearch:2

```

### Healthcheck in Nginx Dockerfile

```

FROM nginx:1.13

HEALTHCHECK --interval=30s --timeout=3s \
  CMD curl -f http://localhost/ || exit 1 #same as false

```

### Healthcheck in Compose/Stack files

```
services:
  web:
    image: nginx
    healthcheck:
      test: ["CMD", "curl", "-f" "http://localhost"]
      interval: 1m30s
      timeout: 10s
      retries:3
      start_period: 1m #version: '3.4' needed

```