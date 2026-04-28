# GLPI

Open source IT Asset Management software.

## Quick Start

```bash
cp .env.example .env
docker compose up -d
```

Access at http://localhost (port 80)

## Commands

| Command | Action |
|---------|--------|
| `docker compose up -d` | Start services |
| `docker compose down` | Stop (keep data) |
| `docker compose down -v` | Stop and delete data |
| `docker compose logs -f` | Follow logs |
| `docker compose logs -f glpi` | GLPI logs only |
| `docker compose logs -f db` | Database logs only |

## Service Names

- Container names: `glpi-glpi-1`, `glpi-db-1`
- Use `glpi` and `db` in docker compose commands
- Access MySQL: `docker exec -it glpi-db-1 mysql -u glpi -p`

## Gotchas

- Port maps to **80**, not 8080 (use `http://localhost`)
- Named volumes: `glpi_data`, `glpi_mysql_data`
- DB container needs ~30s to initialize before GLPI connects
- Image: `glpi/glpi:11`