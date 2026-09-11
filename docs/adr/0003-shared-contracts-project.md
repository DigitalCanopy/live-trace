---
status: accepted
date: 2026-09-11
---

# Le serveur référence un projet de contrats partagés, jamais le SDK

Le SDK `LiveTrace.Maui` est multi-ciblé (`net10.0-android`, `net10.0-windows`) : un serveur qui le référencerait pour partager les objets du payload ne pourrait plus se construire sous Linux sans installer les workloads MAUI, ce qui casse la production de l'image de conteneur. Dupliquer ces objets des deux côtés, l'autre option évidente, les fait dériver dès la première évolution du contrat.

Nous ajoutons donc un projet `LiveTrace.Contracts` en `net10.0` pur, sans aucune dépendance, qui porte les objets du contrat d'ingestion, la version de schéma et les constantes partagées, et rien d'autre. Le SDK et le serveur le référencent tous les deux ; le serveur ne référence jamais le SDK.

## Conséquences

- `LiveTrace.Contracts` doit rester sans aucune dépendance. Une seule référence de package ajoutée là se propagerait au build du serveur et rouvrirait le problème.
- Une évolution du payload se fait dans un seul projet, donc dans une seule pull request, pour les deux côtés à la fois.
- Le projet existe dès le squelette alors qu'il est encore vide : c'est sa place dans le graphe de références qui compte, et c'est elle qui coûte cher à corriger après coup.
