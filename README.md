# n8n
## _Docker Compose-based Installation_

This repository exists for exactly one purpose:
- Provide a clean, repeatable Docker-based install of n8n

That’s it. No workflows live here. No examples. No experiments. Workflows and shared automation live in a separate repository so this one can stay boring, stable, and dependable - like good infrastructure should be.

## What’s in this repo
- docker-compose.yml – the full n8n stack (n8n + Postgres)
- .env – all configuration lives here

You should not need to modify the compose file for normal use. If you feel the urge to do so, pause, hydrate, and re-read the .env first.

## Requirements
- Docker
- Docker Compose (plugin or standalone)
- A system that can keep secrets secret (this is on you)

## Quick start
1. Clone the repository
2. Copy and edit the environment file `cp .env.example .env`
3. Fill in the required values (details below)
4. Start n8n `docker compose up -d`

If everything worked, you now have a running n8n instance backed by Postgres. If it didn’t, Docker will tell you why – usually loudly.

## Required environment variables
All meaningful configuration happens in .env. These values are not optional unless you enjoy debugging containers at 2am.
### Core
```
N8N_RUNNERS_AUTH_TOKEN=change_me_to_a_long_random_alpha_numeric_string
ENCRYPTION_KEY=change_me_to_a_long_random_alpha_numeric_string
TZ=America/Detroit
N8N_HOST=changeHostName
```
- **N8N_RUNNERS_AUTH_TOKEN**
-- Used to authenticate task runners
-- Generate a long, random, alphanumeric value
- **ENCRYPTION_KEY**
--Protects credentials and sensitive data in the database
--If you lose this, encrypted data is gone. Permanently.
- **TZ**
-- Container timezone
-- Set this to match your environment unless you enjoy timestamp archaeology
- **N8N_HOST**
-- The hostname users will access n8n from
-- Example: n8n.example.com
### Postgres
```
POSTGRES_NON_ROOT_USER=changeUser
POSTGRES_NON_ROOT_PASSWORD=some-reasonable-alpha-numeric-password
POSTGRES_USER=changeUser
POSTGRES_PASSWORD=some-reasonable-alpha-numeric-password
POSTGRES_DB=n8n
```
- Use strong, unique passwords
- The database is not optional
- Yes, n8n can run without Postgres – this repo intentionally does not support that

## File permissions and bind mounts

This stack uses bind mounts for persistence.
Before starting the containers, ensure the directories used for:

- n8n data
- Postgres data

and are writable by Docker.

A safe baseline on Linux hosts:
```
sudo chown -R 1000:1000 ./n8n_storage
sudo chown -R 1000:1000 ./n8n-files
```

If your system uses a different UID/GID strategy, adjust accordingly. Containers failing to start due to permissions is not a Docker bug – it’s a rite of passage.

## Updating
To update n8n:
```
docker compose pull
docker compose up -d
```
## Final notes
1. Keep your .env file private
2. Back up your data
3. Document your changes

Infrastructure should be boring. This repo is doing its job if you forget it exists.

--

Visit the Lawrence Systems YouTube channel for educational videos and product reviews plus our live Thursday VLOG: https://youtube.com/@lawrencesystems.

