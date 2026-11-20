# Okaiwa Server — project status

## Product
Self-hostable backend of Okaiwa, a secure messenger with an embedded crypto wallet: zero-knowledge relay, Signal Protocol end-to-end encryption, messages relayed ephemerally and never stored.
Four AdonisJS 6 microservices: `relay` (encrypted blobs over WebSocket/REST), `identity` (pseudonyms, phone hashes, pre-keys), `push` (silent APNs/FCM pushes with no content), `blockchain` (anonymised RPC proxy). Public repository, AGPLv3.

## Environments and state
| Environment | Branch | Where | State |
|---|---|---|---|
| dev | `dev` | — | Last feature work 2026-04-13 (Kyber pre-keys, sender envelope, auth fixes on identity). 31 commits ahead of `main`. |
| rec | `rec` | — | Not used yet. |
| prod | `main` | — | Initial project structure only (2026-04-11). |
| Development server | `dev` | https://okaiwa-api.globodai.group (Globodai server) | Running (`/health` 200 on 2026-11-20); admin panel from `okaiwa/okaiwa-admin`. |

- Target production: AWS (ECS/Fargate, RDS, ElastiCache, ALB), not built yet.
- Mobile clients live in separate repos (`okaiwa/okaiwa-ios`, `okaiwa/okaiwa-android`).

## Open blockers
| Blocker | Owner | Since |
|---|---|---|
| No `pnpm-lock.yaml` committed while CI installs with `--frozen-lockfile`; install currently needs a plain `pnpm install`. | Dev | 2026-04-13 |
| Build workaround: each service's `ace.js` must point at `bin/console.ts` (ts loader does not map `.js` to `.ts`). | Dev | 2026-04-13 |
| Push service needs real APNs and FCM credentials. | Product | 2026-04-13 |
| AWS production environment not provisioned. | DevOps | 2026-04-13 |

## Decisions
| Date | Who | Decision |
|---|---|---|
| 2026-04-13 | Product | Repository is public under AGPLv3; the server never stores, reads or logs message content. |
| 2026-04-13 | DevOps | GitHub organisation moved from `globodai-group` to `okaiwa`. |
| 2026-04-13 | Dev | The API strips client IP forwarding headers for privacy. |

## Contacts (roles)
- Product owner: Okaiwa.
- Development, CI, hosting: Globodai team.

Last updated: 2026-11-20 (source: DevOps memory + git history).
