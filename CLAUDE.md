# Okaiwa Server

Monorepo backend Okaiwa : messager securise avec portefeuille crypto integre. Quatre micro-services AdonisJS (relay, identity, push, blockchain). Depot public AGPLv3 (`LICENSE`). Remote : `okaiwa/okaiwa-server`.

## Stack

AdonisJS 6.x, TypeScript strict 5.x, Lucid ; PostgreSQL 15+, Redis 7+ ; pnpm >=9 (`packageManager` pnpm@9.15.4) + Turborepo 2.x ; Node 20 (`.nvmrc`, CI `NODE_VERSION` 20). Detail : `docs/agents/stack.md`.

## Emplacements

```
okaiwa-server/
├── relay/          # WebSocket, relais ephemere
├── identity/       # Identite et cles
├── push/           # APNs, FCM
├── blockchain/     # Chaine et portefeuille
├── turbo.json
├── pnpm-workspace.yaml
└── commitlint.config.mjs
```

## Regles absolues

Securite zero-knowledge : ne jamais logger le contenu des messages ; relay : blobs E2E opaques dans Redis, TTL 7 j, purges a l'accuse (`relay/app/services/message_queue_service.ts`) ; numeros de telephone uniquement hashes ; pas de secrets dans le code (variables d'environnement) ; valider chaque entree (validators AdonisJS) ; `pnpm audit --audit-level=high` comme en CI. Detail : `docs/agents/security.md`.

Code : `"strict": true` dans chaque `tsconfig.json` ; pas de `any` (`unknown` + type guards) ni de `catch` vide (erreurs typees) ; pas de `// @ts-ignore` ni `// @ts-expect-error` sans justification ; pas de `console.log` en production (logger AdonisJS) ; imports nommes ; IoC AdonisJS ; Lucid plutot que SQL brut. Detail : `docs/agents/code-style.md`.

Langue : PR/issues/reviews en francais ; code et commits en anglais (`docs/agents/language.md`).

## Commandes

```bash
pnpm install              # Installation des dependances
HOST=127.0.0.1 pnpm run dev  # Demarrer tous les services (HOST requis par service, sans defaut ; identity : code SMS dev via DEV_SMS_BYPASS_CODE)
pnpm run build            # Build complet
pnpm run lint             # Verification ESLint
pnpm run lint:fix         # Correction automatique ESLint
pnpm run prettier         # Verification du formatage
pnpm run prettier:fix     # Correction automatique du formatage
pnpm run typecheck        # Verification des types TypeScript
pnpm run test             # Execution des tests
```

CI PR vers `dev` (`.github/workflows/pr-checks.yml`) : Git Conflicts, Banned Keywords, Lockfile, Prettier, Lint, Type Check, Security Audit (`pnpm audit --audit-level=high`, sans `pnpm install` dans ce job), Tests ; `commitlint` via `.husky/commit-msg` seulement (pas en CI).

## Docs detaillees

- `docs/agents/code-style.md` : avant de modifier du TypeScript ou du code AdonisJS.
- `docs/agents/security.md` : avant tout endpoint ou donnee sensible.
- `docs/agents/commits.md` : avant de committer (Conventional Commits / commitlint).
- `docs/agents/git-workflow.md` : avant d'ouvrir ou cibler une PR.
- `docs/agents/language.md` : en cas de doute sur la langue d'un livrable.
- `docs/agents/stack.md` : pour les versions et technologies attendues.
