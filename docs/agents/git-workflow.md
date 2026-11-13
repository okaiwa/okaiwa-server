# Workflow Git

## Branches (convention d'equipe)

| Branche | Environnement | Attendu                          |
| ------- | ------------- | -------------------------------- |
| `main`  | Production    | PR depuis `rec`, accord de Kevin |
| `rec`   | Staging       | PR depuis `dev`, accord de Kevin |
| `dev`   | Developpement | PR feature, CI verte avant merge |

GitHub n'applique pas de protection de branche (`gh api repos/okaiwa/okaiwa-server/branches/{main,dev,rec}/protection` : non protege ; rulesets vides). Le tableau ci-dessus est une convention, pas un verrou technique.

`.github/workflows/pr-checks.yml` ne s'execute que sur les pull requests vers `dev`. Un push sur `rec` ou `main` declenche `.github/workflows/deploy.yml` (deploiement ; job identity : `node ace migration:run --force`).

Les PR vers `rec` doivent provenir de `dev` ; les PR vers `main` de `rec` (`.github/workflows/branch-protection.yml`, controle documentaire non bloquant cote GitHub).

## Processus

1. Creer une branche depuis `dev`
2. Developper avec des commits atomiques
3. PR vers `dev` avec CI verte
4. `dev` -> `rec` -> `main`

## Merge d'une PR vers `dev`

Ne merger que si tous les checks sont `pass` ou `skipping` :

```bash
gh pr checks <N> --json bucket --jq 'any(.[]; .bucket == "pass") and all(.[]; .bucket == "pass" or .bucket == "skipping")'
```

Les promotions vers `rec` et `main` restent soumises a la confirmation de Kevin.

## Controles CI (PR vers `dev`)

Jobs dans `.github/workflows/pr-checks.yml` : Git Conflicts, Banned Keywords, Lockfile, Prettier, Lint, Type Check, Security Audit (`pnpm audit --audit-level=high`, sans etape `pnpm install` dans ce job), puis Tests. `commitlint` : `.husky/commit-msg` uniquement, pas en CI.
