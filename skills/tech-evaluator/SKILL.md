---
name: tech-evaluator
description: Evaluate and compare technologies, frameworks, and tools for Mediapol projects. Use when asked to compare technologies, choose a tech stack, evaluate a framework, assess a SaaS tool, or make build-vs-buy decisions. Provides structured evaluation with scoring and recommendations.
---

# Tech Evaluator

Bewerte und vergleiche Technologien, Frameworks und Tools fuer Mediapol-Projekte.

## Evaluations-Framework

### 1. Anforderungen definieren

Bevor evaluiert wird, klaere:
- **Projekttyp**: Web-App, Mobile App, API, SaaS, etc.
- **Team-Kompetenz**: Welche Technologien kennt das Team?
- **Budget**: Open Source vs. Commercial
- **Timeline**: Schneller Start vs. langfristige Skalierbarkeit
- **Spezielle Anforderungen**: DSGVO, Performance, Offline-faehig, etc.

### 2. Kandidaten identifizieren

Recherchiere 3-5 Kandidaten und erfasse:

```
[Technologie/Tool]
- Typ: [Framework / Library / SaaS / Self-Hosted]
- Lizenz: [MIT / Apache / Commercial / Freemium]
- Sprache: [JS / Python / Go / etc.]
- Maintainer: [Firma / Community]
- GitHub Stars: [Anzahl] | Last Commit: [Datum]
- Dokumentation: [Qualitaet 1-5]
- Community: [Groesse und Aktivitaet]
```

### 3. Bewertungsmatrix

| Kriterium | Gewicht | Kandidat A | Kandidat B | Kandidat C |
|-----------|---------|-----------|-----------|-----------|
| Funktionsumfang | 25% | 4/5 | 3/5 | 5/5 |
| Lernkurve | 15% | 3/5 | 5/5 | 2/5 |
| Performance | 20% | 4/5 | 3/5 | 4/5 |
| Community/Support | 15% | 5/5 | 3/5 | 4/5 |
| Kosten | 10% | 5/5 | 4/5 | 2/5 |
| Zukunftssicherheit | 15% | 4/5 | 3/5 | 5/5 |
| **Gesamt** | 100% | **X.X** | **X.X** | **X.X** |

### 4. Empfehlung

```
Empfehlung: [Kandidat X]

Begruendung:
- [Hauptgrund 1]
- [Hauptgrund 2]
- [Hauptgrund 3]

Risiken:
- [Risiko 1] -> Mitigation: [Massnahme]

Alternative: [Kandidat Y] falls [Bedingung]
```

## Haeufige Evaluierungen bei Mediapol

| Bereich | Typische Kandidaten |
|---------|-------------------|
| Frontend | Next.js, Nuxt, Remix, Astro |
| Backend | Node/Express, Python/FastAPI, Go/Gin |
| CMS | Strapi, Sanity, Contentful, Payload |
| Database | PostgreSQL, MongoDB, Supabase, PlanetScale |
| Hosting | Vercel, Hetzner, AWS, DigitalOcean |
| Auth | Clerk, Auth0, NextAuth, Supabase Auth |
| Payments | Stripe, Mollie, PayPal |

## Verwendung

```
"Vergleiche Next.js vs. Nuxt fuer [Projekt]"
"Welches CMS passt fuer [Anforderungen]?"
"Build vs. Buy Analyse fuer [Feature]"
"Bewerte [Tool] fuer unseren Use Case"
"Welche Datenbank fuer [Projekttyp]?"
```
