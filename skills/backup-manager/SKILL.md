---
name: backup-manager
description: Manage backups for all Mediapol services including databases, configurations, and Docker volumes. Use when asked to create backups, verify backup integrity, restore data, or check backup status.
---

# Backup Manager

Erstelle und verwalte Backups für alle Mediapol-Services.

## Backup-Strategie

### Was wird gesichert?

| Komponente | Methode | Frequenz | Aufbewahrung |
|-----------|---------|----------|--------------|
| PostgreSQL DB | pg_dump | Täglich | 7 Tage |
| Docker Volumes | tar/gzip | Wöchentlich | 4 Wochen |
| .env Dateien | Kopie | Bei Änderung | Permanent |
| Traefik Certs | Kopie | Wöchentlich | 2 Wochen |
| n8n Workflows | API Export | Bei Änderung | Permanent |

### Backup-Verzeichnis
\`\`\`
/backups/
├── daily/
│   ├── postgres_YYYY-MM-DD.sql.gz
│   └── ...
├── weekly/
│   ├── volumes_YYYY-MM-DD.tar.gz
│   └── traefik_YYYY-MM-DD.tar.gz
├── config/
│   ├── openclaw-mc.env
│   ├── n8n.env
│   └── traefik.env
└── n8n/
    └── workflows_YYYY-MM-DD.json
\`\`\`

## Backup-Skripte

### PostgreSQL Backup
\`\`\`bash
# Erstellen
docker exec postgresql pg_dumpall -U postgres | gzip > /backups/daily/postgres_$(date +%F).sql.gz

# Verifizieren (Größe prüfen)
ls -lh /backups/daily/postgres_$(date +%F).sql.gz

# Alte Backups aufräumen (>7 Tage)
find /backups/daily -name "postgres_*.sql.gz" -mtime +7 -delete
\`\`\`

### Docker Volume Backup
\`\`\`bash
# Alle Volumes eines Services sichern
cd /docker/[service]
docker compose stop
tar czf /backups/weekly/[service]_$(date +%F).tar.gz -C /var/lib/docker/volumes .
docker compose start
\`\`\`

### Konfiguration Backup
\`\`\`bash
# Alle .env Dateien sichern
for dir in /docker/*/; do
  [ -f "$dir/.env" ] && cp "$dir/.env" "/backups/config/$(basename $dir).env"
done
\`\`\`

### n8n Workflow Export
\`\`\`bash
curl -s "https://n8n.poljects.cloud/api/v1/workflows" \
  -H "X-N8N-API-KEY: [key]" > /backups/n8n/workflows_$(date +%F).json
\`\`\`

## Restore-Prozeduren

### PostgreSQL Restore
\`\`\`bash
gunzip < /backups/daily/postgres_YYYY-MM-DD.sql.gz | docker exec -i postgresql psql -U postgres
\`\`\`

### Volume Restore
\`\`\`bash
cd /docker/[service]
docker compose stop
tar xzf /backups/weekly/[service]_YYYY-MM-DD.tar.gz -C /var/lib/docker/volumes
docker compose start
\`\`\`

## Verwendung

\`\`\`
"Erstelle ein Backup der Datenbank"
"Wann war das letzte Backup?"
"Stelle die PostgreSQL-DB von gestern wieder her"
"Sichere alle Konfigurationen"
"Exportiere die n8n-Workflows"
\`\`\`
