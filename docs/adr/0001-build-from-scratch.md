---
status: accepted
date: 2026-09-11
---

# Construire Live Trace from scratch plutôt que d'héberger Sentry ou GlitchTip

Sentry et GlitchTip self-hosted couvrent déjà le crash reporting MAUI (SDK `Sentry.Maui`, regroupement, dashboard, alerting) et gardent les données on-prem. Nous les écartons tout de même : la règle interne est de ne pas dépendre d'un projet externe pour cet outil, et non seulement de garder les données chez nous. Live Trace est donc développé de zéro : SDK MAUI, API d'ingestion et dashboard.

## Conséquences

- Tout ce que Sentry offre gratuitement (symbolication, crashs natifs, alerting riche) doit être justifié et construit séparément, ou renoncé.
- Le périmètre reste volontairement réduit : exceptions managées uniquement, pas de performance monitoring.
