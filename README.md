# Openrelik worker for VirusTotal
## Description
Worker for fetching threat intel from VirusTotal.

## Deploy
Add the below configuration to the OpenRelik docker-compose.yml file.

```
openrelik-worker-virustotal:
    container_name: openrelik-worker-virustotal
    image: ghcr.io/openrelik/openrelik-worker-virustotal:latest
    restart: always
    environment:
      - REDIS_URL=redis://openrelik-redis:6379
      - OPENRELIK_PYDEBUG=0
    volumes:
      - ./data:/usr/share/openrelik/data
    command: "celery --app=src.app worker --task-events --concurrency=4 --loglevel=INFO -Q openrelik-worker-virustotal"
    # ports:
      # - 5678:5678 # For debugging purposes.
```

## Test
```
uv sync --group test
uv run pytest -s --cov=.
```
