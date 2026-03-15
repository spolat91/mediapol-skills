---
name: log-analyzer
description: Analyze Docker container logs on the Mediapol VPS to diagnose errors, performance issues, and anomalies. Use when asked to check logs, investigate errors, find error patterns, or troubleshoot service problems.
---

# Log Analyzer

Analysiere Docker-Container-Logs auf dem Mediapol VPS.

## Analyse-Workflow

### 1. Log-Abruf
```bash
# Letzte N Zeilen eines Containers
docker logs --tail=100 [container-name]

# Logs seit einem Zeitpunkt
docker logs --since="2h" [container-name]

# Logs mit Zeitstempel
docker logs --timestamps --tail=50 [container-name]

# Alle Container eines Compose-Projekts
cd /docker/[service] && docker compose logs --tail=100
```

### 2. Fehler-Erkennung

Suche nach Mustern:
```bash
# Errors und Exceptions
docker logs [container] 2>&1 | grep -iE "error|exception|fatal|panic|traceback"

# HTTP-Fehler (4xx/5xx)
docker logs [container] 2>&1 | grep -E "HTTP/(1\.1|2) [45][0-9]{2}"

# OOM (Out of Memory)
dmesg | grep -i "oom\|killed"

# Container Restarts
docker inspect [container] --format='{{.RestartCount}}'
```

### 3. Analyse-Report

Erstelle einen strukturierten Report:
```
🔍 Log-Analyse: [Service]
Zeitraum: [von] — [bis]

❌ Fehler gefunden: [Anzahl]
├── [Fehlertyp 1]: [Anzahl] Vorkommen
│   └── Beispiel: [erste Zeile]
├── [Fehlertyp 2]: [Anzahl] Vorkommen
│   └── Beispiel: [erste Zeile]

⚠️ Warnungen: [Anzahl]
├── [Warnungstyp]: [Details]

📊 Statistik:
├── Requests gesamt: [Anzahl]
├── Fehlerrate: [%]
├── Avg Response Time: [ms] (falls verfügbar)

💡 Empfehlung:
├── [Aktion 1]
├── [Aktion 2]
```

## Container-Referenz

| Container | Log-Format | Typische Fehler |
|-----------|-----------|-----------------|
| openclaw-wfvq-openclaw-1 | JSON/Structured | Agent-Fehler, API-Timeouts |
| openclaw-mission-control-backend-1 | Python/uvicorn | FastAPI Errors, DB-Connection |
| openclaw-mission-control-frontend-1 | Next.js | Build Errors, SSR Failures |
| n8n-n8n-1 | JSON | Workflow Execution Errors |
| traefik-traefik-1 | Structured | Certificate Errors, Routing |
| postgresql | PostgreSQL | Connection Limits, Slow Queries |

## Verwendung

```
"Prüfe die Logs von Mission Control auf Fehler"
"Was ist in den letzten 2 Stunden auf dem VPS passiert?"
"Warum startet [Service] nicht?"
"Analysiere die n8n-Logs nach fehlgeschlagenen Workflows"
```
