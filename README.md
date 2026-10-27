# CENG413 HW-2: Docker Compose with Redis

## Project Description

This project runs a Python Flask application and a Redis cache using Docker Compose. The application connects to Redis using the service name `cache` and stores a visit counter in a named Docker volume.

## How to Run

Open a terminal in the project folder and run:

```bash
docker compose up -d --build
docker compose ps
curl http://localhost:8000/visit
```

Both services should be running, and Redis should show a healthy status.

## Services

- **app:** Python Flask application, accessible on port 8000.
- **cache:** Redis service used to store the visit counter.
- **redisdata:** Named Docker volume that preserves Redis data.

The application connects to Redis through the hostname `cache`, not `localhost`.

## Application Endpoints

| Endpoint | Description |
|---|---|
| `/health` | Returns the application health status |
| `/greet?name=Ada` | Returns a greeting |
| `/visit` | Increments and displays the visit counter stored in Redis |
| `/whoami` | Returns the hostname of the application container |

## Data Persistence

The application container is stateless because the visit counter is stored in Redis.

The following tests were performed successfully:

1. Removing and recreating the `app` container preserved the counter.
2. Running `docker compose down` and restarting the services preserved the counter.
3. Running `docker compose down -v` removed the Redis volume and reset the counter.

## Configuration and Security

The application uses environment variables for configuration.

- `APP_GREETING`: Greeting text, default `Hello`.
- `REDIS_HOST`: Redis service hostname, set to `cache`.
- `REDIS_PORT`: Redis port, default `6379`.

The application runs as a non-root user inside its container. The Redis image uses a versioned tag rather than `latest`.

This local lab setup does not configure a Redis password. No passwords or other secrets are stored in the repository.

## Stop the Services

```bash
docker compose down
```

This stops and removes the containers while preserving the Redis data volume.