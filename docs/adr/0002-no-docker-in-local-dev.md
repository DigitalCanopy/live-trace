---
status: accepted
date: 2026-09-11
---

# Pas de Docker en développement local, image produite par le SDK .NET

Le poste de développement n'a pas de droits administrateur et n'en aura pas : Docker Desktop, WSL 2 et Hyper-V y sont inaccessibles. Plutôt que `docker compose`, le serveur démarre lui-même ses dépendances en Development : PostgreSQL embarqué (binaires téléchargés dans le profil utilisateur, sans installation) et serveur Vite du dashboard via SpaProxy. `dotnet run` lance tout ; `dotnet test` utilise le même Postgres embarqué, sans Docker, en local comme en CI.

Le déploiement reste conteneurisé : l'image est produite par `dotnet publish /t:PublishContainer`, qui n'a besoin ni de `Dockerfile` ni de démon Docker, et poussée vers le registre Azure. Le repo ne contient donc ni `Dockerfile` ni `docker-compose.yml`.

## Options écartées

- **.NET Aspire** : sa ressource PostgreSQL est un conteneur, il n'enlève donc rien au travail ci-dessus, et il n'y a qu'un seul service à orchestrer. À reconsidérer si un second service apparaît (worker d'agrégation en P2).
- **SQLite en dev, PostgreSQL en prod** : les requêtes d'agrégation du dashboard finiraient par diverger entre moteurs.
- **GitHub Codespaces** : Docker dans le cloud, mais le SDK MAUI et l'émulateur restent sur le poste ; deux environnements à jongler.
