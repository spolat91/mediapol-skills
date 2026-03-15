---
name: sales-pipeline
description: Track and manage the Mediapol sales pipeline. Use when asked about deals, pipeline status, lead conversion, revenue forecast, or sales metrics. Provides pipeline overview, deal stage tracking, and win/loss analysis.
---

# Sales Pipeline Manager

Verwalte die Mediapol Sales-Pipeline — von Lead bis Abschluss.

## Kernfunktionen

### 1. Pipeline-Übersicht
Erstelle eine strukturierte Übersicht aller aktiven Deals:

```
Pipeline-Status:
├── 🆕 Neue Leads (Anzahl, Gesamtwert)
├── 📞 Kontaktiert (Erstgespräch geführt)
├── 📋 Angebot gesendet (Wert, Deadline)
├── 🤝 Verhandlung (offene Punkte)
└── ✅ Gewonnen / ❌ Verloren (diesen Monat)
```

### 2. Deal-Tracking
Für jeden Deal erfasse:
- **Unternehmen** und Ansprechpartner
- **Projekttitel** und kurze Beschreibung
- **Geschätzter Wert** (einmalig + monatlich)
- **Stage** (Lead → Kontaktiert → Angebot → Verhandlung → Gewonnen/Verloren)
- **Nächste Aktion** und Deadline
- **Wahrscheinlichkeit** (0-100%)

### 3. Forecast
Berechne den gewichteten Pipeline-Forecast:
```
Gewichteter Wert = Dealwert × Wahrscheinlichkeit
Forecast = Summe aller gewichteten Werte
```

### 4. Aktionsplan
Generiere wöchentliche Prioritätenliste:
- Deals die diese Woche Follow-up brauchen
- Angebote die ablaufen
- Leads die zu lange ohne Kontakt sind (>7 Tage)

## Datenquellen

- **Mission Control Tasks**: Board "Poljects" für aktive Kundenprojekte
- **Jira POL-Projekt**: Verknüpfte Issues für Projektfortschritt
- **lemlist**: Outreach-Kampagnen und Response-Tracking (falls MCP verfügbar)

## Output-Format

Berichte als strukturierte Discord-Nachricht mit:
- Emoji-Indikatoren für Deal-Status
- Tabellen für Übersicht
- Klare Handlungsempfehlungen

## Verwendung

```
"Zeig mir die aktuelle Pipeline"
"Wie steht es um den Deal mit [Firma]?"
"Erstelle einen Forecast für diesen Monat"
"Welche Deals brauchen diese Woche Aufmerksamkeit?"
```
