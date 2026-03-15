---
name: deployment-manager
description: Manage deployments on the Mediapol VPS (srv1281781.hstgr.cloud). Use when asked to deploy, update, restart, or rollback Docker services. Covers pre-deployment checks, container management, and rollback procedures for all hosted services.
---

# Deployment Manager

Standardisierter Deployment-Prozess für alle Mediapol-Services auf dem VPS.

## Infrastruktur

**VPS:** srv1281781.hstgr.cloud (Hostinger)
**Reverse Proxy:** Traefik (automatisches SSL via Let's Encrypt)
**Container Runtime:** Docker Compose

### Gehostete Services

| Service | Pfad | Domain |
|---------|------|--------|
| OpenClaw | /docker/openclaw-wfvq | oc.poljects.cloud |
| Mission Control | /docker/openclaw-mission-control | missioncontrol.poljects.cloud |
| n8n | /docker/n8n | n8n.poljects.cloud |
| Traefik | /docker/traefik | — |
| PostgreSQL | /docker/postgresql | — |
| CloudBeaver | /docker/cloudbeaver | — |
| Poljects Landing | /docker/poljects-landing | poljects.cloud |

## Deployment-Workflow

### Pre-Deployment Checklist
```
1. ☐ Backup der aktuellen Konfiguration
2. ☐ Docker Images pullen / builden
3. ☐ .env Datei prüfen (keine Secrets geändert?)
4. ☐ Disk Space prüfen (>20% frei)
5. ☐ Aktive User/Connections prüfen
```

### Deploy-Befehle
```bash
# Standard-Update (Pull + Restart)
cd /docker/[service]
docker compose pull
docker compose up -d

# Build + Deploy (wenn Dockerfile geändert)
docker compose build --no-cache [service]
docker compose up -d [service]

# Einzelnen Container neustarten
docker compose restart [container-name]
```

### Post-Deployment Checks
```bash
# Container-Status prüfen
docker compose ps

# Logs auf Fehler prüfen (letzte 50 Zeilen)
docker compose logs --tail=50 [service]

# Health-Check via HTTP
curl -s -o /dev/null -w "%{http_code}" https://[domain]/
```

### Rollback
```bash
# Zurück zur vorherigen Version
docker compose down
docker compose up -d --force-recreate

# Oder: Specific Image Version
docker compose pull [service]@[previous-tag]
docker compose up -d
```

## Sicherheitsregeln

- **Nie** `.env` Dateien überschreiben ohne Backup
- **Nie** `docker system prune` ohne Rückfrage ausführen
- **Immer** Logs nach Deploy prüfen
- **Immer** SSL-Zertifikat nach Domain-Änderungen verifizieren
- Bei Problemen: Rollback > Debug

## Verwendung

```
"Deploye die neueste Version von [Service]"
"Starte Mission Control neu"
"Prüfe ob alle Services laufen"
"Rollback [Service] auf die vorherige Version"
```
