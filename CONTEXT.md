# Live Trace

Solution interne de crash reporting et d'analytics d'usage pour les applications MAUI de l'entreprise, construite from scratch : un SDK embarqué dans les apps, une API d'ingestion et un dashboard de lecture.

## Language

### Applications suivies

**Application** :
Une app MAUI suivie par Live Trace, identifiée par sa propre clé d'API. Plusieurs Applications coexistent dans une même instance.
_Avoid_ : projet, app, tenant, produit

**Device** :
Une installation physique de l'Application, identifiée par un identifiant d'installation généré par le SDK.
_Avoid_ : appareil, téléphone, installation, client

**User** :
La personne connectée à l'Application, identifiée par son identifiant d'annuaire, avec son e-mail et son rôle métier. Une même personne sur deux Devices compte pour un seul User. Inconnu tant que le login n'a pas eu lieu.
_Avoid_ : utilisateur anonyme, compte, visiteur

**Session** :
La période entre l'ouverture de l'Application et sa mise en arrière-plan ou sa fermeture.
_Avoid_ : visite, connexion

### Erreurs

**Crash** :
Une exception non gérée qui termine l'Application.
_Avoid_ : plantage, erreur fatale, exception non gérée

**Error** :
Une exception gérée que le code de l'Application remonte volontairement à Live Trace.
_Avoid_ : exception, erreur gérée, warning

**Occurrence** :
Une instance individuelle de Crash ou d'Error, avec sa stack trace, son Device, son User et son contexte au moment des faits.
_Avoid_ : événement d'erreur, rapport, log

**Issue** :
Le regroupement des Occurrences qui partagent la même signature (type d'exception et frame d'origine). C'est l'unité affichée et comptée dans le dashboard.
_Avoid_ : bug, groupe, problème, erreur

**Breadcrumb** :
Le fil des Events et Screen views de la Session qui précèdent une Occurrence.
_Avoid_ : historique, trace, log

### Usage

**Event** :
Une action utilisateur nommée, remontée par le code de l'Application (clic sur un bouton, utilisation d'une feature).
_Avoid_ : action, événement custom, log, tracking

**Screen view** :
L'affichage d'une page de l'Application.
_Avoid_ : page view, navigation, écran

### Contexte d'exécution

**Environment** :
Le contexte de déploiement de l'Application d'où provient un envoi (développement, recette, production). Filtre transversal du dashboard.
_Avoid_ : env, stage, tenant

**Version** :
Le numéro de version et de build de l'Application au moment d'un envoi. Sert à dater les Issues et à détecter les régressions.
_Avoid_ : release, build seul

### Dashboard

**Account** :
Une personne qui se connecte au dashboard Live Trace. Distinct du User, qui utilise l'Application suivie.
_Avoid_ : utilisateur, user, compte dashboard, opérateur

**Admin** :
Le rôle d'Account qui administre les Applications, leurs clés d'API et les autres Accounts.
_Avoid_ : administrateur, superuser, owner

**Viewer** :
Le rôle d'Account qui consulte les Applications pour lesquelles il a un Access et change le statut de leurs Issues, sans administrer.
_Avoid_ : user, lecteur, membre

**Access** :
Le droit d'un Account Viewer de consulter une Application donnée, accordé par un Admin. Un Admin accède à toutes les Applications sans Access.
_Avoid_ : permission, droit, autorisation, accès
