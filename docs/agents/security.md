# Securite — Regles fondamentales

> **La securite est la priorite absolue. Okaiwa est un messager zero-knowledge.**

- **JAMAIS logger le contenu des messages** : uniquement les metadonnees (timestamps, compteurs, codes d'erreur).
- **Relay : file transitoire uniquement** : blobs chiffres bout-en-bout opaques dans Redis, TTL 7 jours, purges a l'accuse de reception (`relay/app/services/message_queue_service.ts`) — pas de persistance durable cote serveur.
- **JAMAIS inclure de numeros de telephone en clair** : toujours utiliser des valeurs hashees.
- **JAMAIS de secrets dans le code** : tout passe par les variables d'environnement.
- **Valider toutes les entrees** : utiliser les validators AdonisJS sur chaque endpoint.
- **Zero tolerance** pour les failles connues : `pnpm audit --audit-level=high` comme en CI (job Security Audit).
