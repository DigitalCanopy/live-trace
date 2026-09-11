# CLAUDE.md

Règles de comportement pour ce repo. Complète-les avec les commandes, conventions et zones sensibles du projet au fur et à mesure.

**Compromis :** ces règles favorisent la prudence sur la vitesse. Pour une tâche triviale (typo, renommage local), applique-les sans cérémonie.

## 1. Hypothèses explicites, puis avance

- Si plusieurs interprétations sont plausibles et mènent à un travail différent, présente-les avant de coder.
- Sinon, énonce ton hypothèse en une ligne et continue. Ne bloque pas sur une question dont la réponse ne changerait pas le résultat.
- Si une approche plus simple existe, dis-le. Pousse en retour quand c'est justifié.
- Ne cache pas une confusion : nomme-la, propose un choix, avance.
- Quand un skill mattpocock est actif (par exemple `grilling` ou `tdd`), ses règles de questionnement priment sur celle-ci : elles sont volontairement bloquantes.

## 2. Simplicité d'abord

- Le minimum de code qui résout le problème. Rien de spéculatif.
- Pas de fonctionnalité au-delà de la demande.
- Pas d'abstraction pour du code à usage unique.
- Pas de "flexibilité" ou de "configurabilité" non demandée.
- Pas de gestion d'erreur pour des cas impossibles.
- Si tu écris 200 lignes et que 50 suffiraient, réécris.

Test : "Un ingénieur senior dirait-il que c'est surcompliqué ?" Si oui, simplifie.

## 3. Changements chirurgicaux

- Code mort préexistant : signale-le, ne le supprime pas.
- Supprime les imports, variables et fonctions que TES changements ont rendus inutilisés.

## 4. Vérification : les skills mattpocock sont le workflow

Ne réinvente pas un workflow. Les skills du plugin `mattpocock-skills` s'enchaînent entre eux (par exemple `implement` pilote `tdd` puis `code-review` ; les interviews lancent toujours `grilling` avec `domain-modeling`). Laisse cet enchaînement se faire, ne le raccourcis pas.

- Si tu hésites sur le skill ou le flux adapté, lance `ask-matt` : c'est le routeur officiel, pas ce fichier.
- Le flux principal pour une fonctionnalité part de `grill-with-docs`, pas de `tdd` directement.
- Lis `CONTEXT.md` et les ADR s'ils existent avant de toucher un module.

Hors skill, un critère de succès vérifiable reste obligatoire : quelle commande, quel test ou quelle observation prouve que c'est fini. "Ça marche" n'est pas un critère.

## Projet

<!-- À compléter : commandes de build/test/lint, conventions, fichiers ou dossiers à ne pas toucher. -->

---

**Ces règles fonctionnent si :** les diffs sont plus petits, il y a moins de réécritures pour surcomplication, et les questions arrivent avant l'implémentation plutôt qu'après une erreur.

## Agent skills

### Issue tracker

Issues are tracked as GitHub Issues on `DigitalCanopy/live-trace`, via the `gh` CLI. See `docs/agents/issue-tracker.md`.

### Triage labels

Default vocabulary: `needs-triage`, `needs-info`, `ready-for-agent`, `ready-for-human`, `wontfix`. See `docs/agents/triage-labels.md`.

### Domain docs

Single-context: one `CONTEXT.md` and `docs/adr/` at the repo root. See `docs/agents/domain.md`.
