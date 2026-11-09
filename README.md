# GitHub Actions — Cours Liora

Ce dépôt regroupe les exercices du module **GitHub Actions (CI/CD)** du bootcamp **Développeur Full Stack de Liora** (ex-DataScientest).

Son but est d'apprendre à automatiser des tâches avec des **workflows** GitHub, qui se lancent tout seuls à chaque `push` ou `pull request`.

## Workflows

Les workflows se trouvent dans le dossier `.github/workflows`.

| Fichier | Déclencheur | Ce qu'il fait |
|---|---|---|
| `my_first_workflow.yml` | Chaque `push` | Lance le même job sur **2 versions d'Ubuntu** en parallèle grâce à une **matrice** : affiche « Hello world », la version de Python, crée un fichier et liste le dossier. |
| `multiple_shells.yaml` | `push` sur `main` et `pull request` | Exécute du **Python** sur Ubuntu, puis, grâce à `needs`, un job **Windows** en PowerShell et en Bash qui affiche les variables d'environnement par défaut de GitHub. |

## Notions abordées

- La structure d'un workflow : `name`, `on`, `jobs`, `runs-on`, `steps`, `run`
- La **matrice** (`strategy.matrix`) pour tester plusieurs systèmes en même temps
- Le choix du **shell** : `bash`, `pwsh`, `python`…
- L'exécution **séquentielle** des jobs avec `needs`
- Les **déclencheurs** : `push` sur une branche, types de `pull_request`
- Le **mode debug** avec les secrets `ACTIONS_RUNNER_DEBUG` et `ACTIONS_STEP_DEBUG`
- La lecture et le téléchargement des **journaux** dans l'onglet Actions
- Les **variables d'environnement** par défaut : `GITHUB_ACTOR`, `GITHUB_REPOSITORY`, `GITHUB_EVENT_NAME`, `GITHUB_WORKSPACE`…

## Voir les résultats

Onglet **Actions** du dépôt, puis clic sur une exécution pour voir le détail de chaque job et de chaque step.



Charlotte Queijo