# AGENTS.md - GLPI Docker Deployment

## Project Overview

This repository contains a Docker Compose configuration for running GLPI (Gestionnaire Libre de Parc Informatique), an open-source IT asset management and helpdesk system. There is no custom source code - the application runs from the official `glpi/glpi:latest` Docker image.

## Quick Start

```bash
# Copy environment file and configure
cp .env.example .env
# Edit .env with your database credentials

# Start the stack
docker compose up -d

# View logs
docker compose logs -f

# Stop the stack
docker compose down
```

## Commands

### Running the Application

| Command | Description |
|---------|-------------|
| `docker compose up -d` | Start all services in detached mode |
| `docker compose down` | Stop and remove all containers |
| `docker compose restart` | Restart all services |
| `docker compose logs -f` | Follow logs in real-time |
| `docker compose logs -f glpi` | Follow logs for GLPI service only |
| `docker compose ps` | Show running containers |

### Database Operations

| Command | Description |
|---------|-------------|
| `docker compose exec db mysql -u glpi -p glpi` | Access MySQL CLI |

### Accessing the Application

- Web UI: http://localhost:8080
- Default credentials: `glpi` / `glpi` (change after first login)

## Environment Variables

Create a `.env` file based on `.env.example`:

```bash
GLPI_DB_HOST=db
GLPI_DB_PORT=3306
GLPI_DB_NAME=glpi
GLPI_DB_USER=glpi
GLPI_DB_PASSWORD=your_secure_password
```

## Data Persistence

- GLPI files: `/opt/glpi/glpi` (host)
- MySQL data: `/opt/glpi/mysql` (host)

## Single Test Commands

N/A - This is a Docker deployment project without testable source code.

## Code Style Guidelines

N/A - No custom source code in this repository.

## Project Structure

```
.
├── .env.example      # Environment template
├── .gitignore        # Git ignore patterns
├── AGENTS.md         # This file
├── README.md         # Basic readme
└── compose.yaml      # Docker Compose configuration
```

## Important Notes

1. This is a deployment-only repository using the official GLPI Docker image
2. No PHP, JavaScript, or other application code is present
3. Configuration changes should be made via environment variables or within the GLPI web UI
4. Back up the mounted volumes (`/opt/glpi/glpi` and `/opt/glpi/mysql`) regularly

## Troubleshooting

```bash
# Check container health
docker compose ps

# View specific service logs
docker compose logs db
docker compose logs glpi

# Rebuild and start fresh
docker compose down -v
docker compose up -d
```
