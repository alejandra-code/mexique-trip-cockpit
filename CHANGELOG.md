# Changelog

Toutes les versions notables du Cockpit Mexique 2026.

## [1.0.0] — 2026-07-04
Première version versionnée, prête à déployer.

### Ajouté
- Cockpit HTML mobile-first : statut mission control, compte à rebours, avancement.
- Trame du séjour en 5 phases (arrivée, solo, bascule famille, escapades, retour).
- Vols confirmés (réf. XMR2QG) + vols internes MEX↔PXM à réserver.
- Module **Annonces & messages** : pipeline de logements avec fils de discussion
  (1er message espagnol calibré déjà en place), ajout/suppression, statut cyclable.
- Les 3 missions cumulatives (KPC télétravail, talents IA offshore, Nidos) en checklists.
- Budget consolidé estimé/réel avec recalcul auto.
- Checklist pré-départ + décisions à trancher + journal.
- **Backend Supabase** : sync multi-appareils, offline-first (cache local + resync).
- Vue calendrier live connectée Google Calendar (via Claude/Cowork).

### Sécurité
- RLS : le rôle anon n'accède qu'aux tables `voyage_*`. Données KPC du projet
  Supabase vérifiées inaccessibles (event_signups = 0 ligne en anon).

## [0.2.0] — 2026-07-04 (interne)
### Modifié
- Retrait du chantier « Impôts » (hors périmètre voyage).
- Correction route Puerto→Oaxaca : autoroute 135D ~3h-3h30 (au lieu de 6-7h).
- Escapades datées (Oaxaca 18-19/08, Mazunte 25-26/08) d'après l'agenda réel.

## [0.1.0] — 2026-07-04 (interne)
### Ajouté
- Première maquette cockpit statique (persistance localStorage).
