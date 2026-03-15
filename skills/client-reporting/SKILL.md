---
name: client-reporting
description: Generate structured client reports for Mediapol projects. Use when asked to create status reports, monthly summaries, project updates, or progress overviews for clients. Pulls data from Jira, Mission Control, and Git to compile comprehensive reports.
---

# Client Reporting

Erstelle strukturierte Kundenberichte für Mediapol-Projekte.

## Report-Typen

### 1. Wöchentlicher Status-Report

```markdown
# Status-Report: [Projekt] — KW [XX]

## Zusammenfassung
[2-3 Sätze zum Gesamtstatus]

## Ampel-Status
| Bereich | Status |
|---------|--------|
| Timeline | 🟢 / 🟡 / 🔴 |
| Budget | 🟢 / 🟡 / 🔴 |
| Qualität | 🟢 / 🟡 / 🔴 |
| Scope | 🟢 / 🟡 / 🔴 |

## Diese Woche erledigt
- [Task 1] ✅
- [Task 2] ✅
- [Task 3] ✅

## Nächste Woche geplant
- [Task 4]
- [Task 5]

## Risiken / Blocker
- [Risiko 1]: [Maßnahme]

## Entscheidungsbedarf
- [Frage die der Kunde beantworten muss]
```

### 2. Monatlicher Projektbericht

Umfassenderer Report mit:
- Sprint-Velocity und Burndown
- Feature-Completion Rate
- Stunden-Aufwand vs. Schätzung
- Nächste Meilensteine
- Budget-Verbrauch

### 3. Abschluss-Report

- Projektübersicht und Zielerreichung
- Deliverables und Dokumentation
- Lessons Learned
- Empfehlungen für nächste Schritte

## Datenquellen

| Quelle | Was | Wie |
|--------|-----|-----|
| Jira | Issues, Sprints, Velocity | JQL-Abfrage über API |
| Mission Control | Agent-Tasks, Board-Status | MC API |
| Git | Commits, PRs, Releases | Git Log / GitHub API |
| Zeiterfassung | Stunden pro Task | Jira Worklogs |

## Automatisierung

Der Report kann als Cron-Job konfiguriert werden:
- **Wöchentlich**: Freitag 16:00 Uhr
- **Monatlich**: Letzter Arbeitstag des Monats
- **Delivery**: Discord-Kanal oder direkt per E-Mail

## Verwendung

```
"Erstelle einen Status-Report für [Projekt]"
"Monatsbericht für [Kunde] zusammenstellen"
"Was haben wir diese Woche für [Kunde] erledigt?"
"Abschluss-Report für [Projekt] erstellen"
```
