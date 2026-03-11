<<<<<<< HEAD
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
=======
# AGENTS.md - Development Guide for GLPI Docker Setup

## Project Overview

This repository contains a Docker Compose configuration for running GLPI (Gestionnaire Libre de Parc Informatique), an IT Asset Management software. The actual GLPI application runs from the official `glpi/glpi` Docker image.

**Repository:** https://github.com/pmsbs/glpi
**Live URL:** http://localhost:8080

---

## Build, Run, and Test Commands

### Starting Services

```bash
# Start all services in detached mode
docker compose up -d

# Start with verbose output
docker compose up

# Rebuild and start (if Dockerfile or compose changes)
docker compose up --build
```

### Stopping Services

```bash
# Stop all services
docker compose down

# Stop and remove volumes (WARNING: deletes database data)
docker compose down -v

# Stop and remove images
docker compose down --rmi all
```

### Viewing Logs

```bash
# View all logs
docker compose logs

# Follow logs in real-time
docker compose logs -f

# View logs for specific service
docker compose logs -f glpi
docker compose logs -f db
```

### Database Commands

```bash
# Access MySQL CLI
docker exec -it glpi-db mysql -u glpi -p

# Backup database
docker exec glpi-db mysqldump -u glpi -p glpi > backup.sql

# Restore database
docker exec -i glpi-db mysql -u glpi -p glpi < backup.sql
```

### Health Checks

```bash
# Check service status
docker compose ps

# Verify database is ready
docker compose logs db | grep "ready for connections"
```

### Testing

There are no unit tests for this Docker configuration. To verify the setup works:
1. Run `docker compose up -d`
2. Wait ~30 seconds for initialization
3. Visit http://localhost:8080
4. Complete the GLPI installation wizard

---

## Code Style Guidelines

This project contains only Docker configuration files (compose.yaml, .env). There is no PHP/JavaScript code to style.

### Configuration Files

- **compose.yaml**: Uses Docker Compose v2 syntax
- **.env**: Environment variables for local development
- Follow existing indentation (2 spaces)

### File Patterns

- Always use the `.env` file for sensitive configuration (never commit to git)
- The `.env.example` file documents required variables
- Keep `.gitignore` minimal - only exclude `.env`

---

## Development Workflow

### Initial Setup

1. Copy `.env.example` to `.env`
2. Edit `.env` with your desired database credentials
3. Run `docker compose up -d`
4. Access GLPI at http://localhost:8080
5. Complete installation wizard with database credentials from `.env`

### Database Configuration (Installation Wizard)

- **Database host:** `db`
- **Database name:** Value of `GLPI_DB_NAME` (default: glpi)
- **Database user:** Value of `GLPI_DB_USER` (default: glpi)
- **Database password:** Value of `GLPI_DB_PASSWORD`

### Common Tasks

#### Reset Everything

```bash
docker compose down -v
docker compose up -d
```

#### Update GLPI Version

```bash
# Change image tag in compose.yaml, e.g., glpi/glpi:10.0.6
docker compose up -d
```

#### Access Container Shell

```bash
docker exec -it glpi-glpi sh
```

#### View GLPI Logs

```bash
docker exec glpi-glpi tail -f /var/log/glpi/php.log
```

---

## Important Notes

1. **No Source Code**: This is not the GLPI project source code. It's a deployment configuration.
2. **Data Persistence**: Database and files are stored in Docker volumes (`/opt/glpi/glpi`, `/opt/glpi/mysql`)
3. **Production Use**: This setup is suitable for development/testing only. Production deployments require additional security configuration.
4. **Updates**: To update GLPI, simply change the image tag in `compose.yaml` and recreate containers.

---

## Troubleshooting

### Database Connection Failed

- Wait longer for MySQL to initialize (can take 30-60 seconds)
- Verify credentials in `.env` match installation wizard input
- Check logs: `docker compose logs db`

### Port 8080 Already in Use

Edit `compose.yaml` and change the port mapping:
```yaml
ports:
  - "8090:80"  # Use 8090 instead
```

### Permission Issues

```bash
sudo chown -R 1000:1000 /opt/glpi/glpi /opt/glpi/mysql
```

---

## File Reference

| File | Purpose |
|------|---------|
| `compose.yaml` | Docker services configuration |
| `.env.example` | Environment variable template |
| `.env` | Local environment variables (gitignored) |
| `.gitignore` | Git ignore rules |
>>>>>>> edc49d1 (Update to GLPI 11 and add AGENTS.md documentation)
