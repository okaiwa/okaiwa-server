# Règles de code

## TypeScript

- **Mode strict obligatoire** : `"strict": true` dans tous les `tsconfig.json`.
- **Zero `any`** : utiliser `unknown` si le type est inconnu, puis affiner avec des type guards.
- **Pas de `console.log` en production** : utiliser le logger AdonisJS.
- **Pas de `// @ts-ignore` ou `// @ts-expect-error`** sans justification documentee.
- **Imports explicites** : pas de `import *`, toujours des imports nommes.
- **Gestion d'erreurs** : toujours typer les erreurs, jamais de `catch` vide.

## AdonisJS

- Respecter la structure de repertoires standard AdonisJS.
- Utiliser les validators AdonisJS pour toute validation d'entree.
- Utiliser le conteneur IoC pour l'injection de dependances.
- Requetes base de donnees via Lucid ORM ou query builder — pas de SQL brut sauf necessite absolue.
