# GitHub Actions — Cours Liora

Ce dépôt regroupe les exercices du module **GitHub Actions (CI/CD)** du bootcamp **Développeur Full Stack de Liora** (ex-DataScientest).

Son but est d'apprendre à automatiser des tâches avec des **workflows** GitHub, qui se lancent tout seuls à chaque `push` ou `pull request`.

## Contenu du dépôt

```
github_actions/
├── .github/
│   └── workflows/
│       ├── my_first_workflow.yml
│       ├── multiple_shells.yml
│       └── control_tests.yml
├── file_test.py
└── README.md
```

## Workflows

| Fichier | Déclencheur | Ce qu'il fait |
|---|---|---|
| `my_first_workflow.yml` | Chaque `push` | Lance le même job sur **2 versions d'Ubuntu** en parallèle grâce à une **matrice** : affiche « Hello world », la version de Python, crée un fichier et liste le dossier. |
| `multiple_shells.yml` | `push` sur `main` et `pull request` | Exécute du **Python** sur Ubuntu, puis, grâce à `needs`, un job **Windows** en PowerShell et en Bash qui affiche les variables d'environnement par défaut de GitHub. |
| `control_tests.yml` | Chaque `push` | **Contrôle qualité** du code : récupère le dépôt, installe Python, lance les tests avec **pytest**, puis vérifie le style du code avec **flake8** (norme PEP 8). |

## Tests et qualité du code

Le fichier `file_test.py` contient 4 tests simples : une addition, une soustraction, une multiplication et une comparaison de texte.

- **pytest** exécute automatiquement toutes les fonctions dont le nom commence par `test_` et vérifie leurs `assert`.
- **flake8** vérifie que le code respecte la norme **PEP 8** : imports inutilisés, espaces autour des opérateurs, deux lignes vides entre les fonctions, indentation des commentaires…

Lors du premier push, les tests passaient mais flake8 échouait. Le code a ensuite été corrigé pour respecter PEP 8, et le workflow passe au vert.

## Notions abordées

**Les bases d'un workflow**
- La structure : `name`, `on`, `jobs`, `runs-on`, `steps`, `run`
- La **matrice** (`strategy.matrix`) pour tester plusieurs systèmes en même temps
- Le choix du **shell** : `bash`, `pwsh`, `python`…
- L'exécution **séquentielle** des jobs avec `needs`
- Les **déclencheurs** : `push`, `push` sur une branche, types de `pull_request`, `workflow_dispatch` (lancement manuel)

**Les actions du Marketplace**
- Le mot-clé `uses` pour réutiliser une action existante :
  - `actions/checkout` copie le dépôt sur la machine qui exécute le workflow
  - `actions/setup-python` installe Python, avec sa version choisie dans `with`
  - `py-actions/flake8` lance flake8

**Les variables et les secrets**
- Les **variables d'environnement** par défaut : `GITHUB_ACTOR`, `GITHUB_REPOSITORY`, `GITHUB_EVENT_NAME`, `GITHUB_WORKSPACE`, `GITHUB_SHA`…
- Les **variables personnalisées** avec `env`, définies à 3 niveaux : pour tout le workflow, pour un job ou pour un seul step
- Les **secrets** (`${{ secrets.NOM }}`), pour cacher les informations sensibles comme les identifiants d'API ou de base de données
- Le jeton **`GITHUB_TOKEN`**, qui permet à un workflow de faire un `push` sur le dépôt (avec `permissions: contents: write`)

**Le débogage**
- Le **mode debug** avec les secrets `ACTIONS_RUNNER_DEBUG` et `ACTIONS_STEP_DEBUG`
- La lecture et le téléchargement des **journaux** dans l'onglet Actions

## Voir les résultats

Onglet **Actions** du dépôt, puis clic sur une exécution pour voir le détail de chaque job et de chaque step.



Charlotte Queijo