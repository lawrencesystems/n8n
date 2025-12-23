# n8n
## _Docker Compose-based Installation_

This repository exists for exactly one purpose:
- Provide a clean, repeatable Docker-based install of n8n

That’s it. No workflows live here. No examples. No experiments. Workflows and shared automation live in a separate repository so this one can stay boring, stable, and dependable - like good infrastructure should be.

## What’s in this repo
- docker-compose.yml – the full n8n stack (n8n + Postgres)
- .env – for password configuration


## Requirements
- Docker
- Docker Compose (plugin or standalone)
- A system that can keep secrets secret (this is on you)

## Quick start
1. Clone the repository
2. Copy and edit the environment file
3. Fill in the required values (details below)
4. Start n8n `docker compose up -d`

If everything worked, you now have a running n8n instance backed by Postgres. If it didn’t, Docker will tell you why – usually loudly.

## Required environment variables
Password configuration happens in .env. 

## File permissions and bind mounts

This stack uses bind mounts for persistence.
Before starting the containers, ensure the directories are created and are writable by Docker. if you create them ahead of time using

`mkdir -p data/n8n local-files`

With a user that has proper permisions they should be fine, if not you will have to set those permissions.

Start the service

```
docker compose pull
docker compose up -d
```
## Final notes
1. Keep your .env file private
2. Back up your data
3. Document your changes



