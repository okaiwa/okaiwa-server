# Conventions de commits

Format **Conventional Commits** obligatoire, verifie par commitlint :

```
<type>(<scope>): <description>
```

## Types autorises

| Type       | Usage                                    |
| ---------- | ---------------------------------------- |
| `feat`     | Nouvelle fonctionnalite                  |
| `fix`      | Correction de bug                        |
| `docs`     | Documentation uniquement                 |
| `style`    | Formatage (pas de changement de logique) |
| `refactor` | Refactoring sans changement fonctionnel  |
| `perf`     | Amelioration de performance              |
| `test`     | Ajout ou modification de tests           |
| `build`    | Systeme de build, dependances            |
| `ci`       | Configuration CI/CD                      |
| `chore`    | Taches de maintenance                    |
| `revert`   | Annulation d'un commit precedent         |
| `security` | Correctif ou amelioration de securite    |

## Scopes autorises

`relay`, `identity`, `push`, `blockchain`, `ci`, `deps`
