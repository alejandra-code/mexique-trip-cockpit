# 🌊 Cockpit Mexique 2026 — Trip Planner

Tableau de bord de pilotage d'un voyage de ~5 semaines à Puerto Escondido (Oaxaca),
mobile-first, synchronisé cloud, conçu pour évoluer en vrai *trip planner + AI assistant*.

## Ce que c'est

Un cockpit HTML autonome (un seul fichier) qui pilote toute la logistique d'un voyage :
statuts des chantiers, trame du séjour, vols, pipeline d'annonces de logement avec
historique de messages, budget estimé/réel, checklist pré-départ, journal de décisions.

- **Mobile-first** : optimisé iPhone (plein écran, safe-area, ajout à l'écran d'accueil).
- **Offline-first** : fonctionne sans réseau (cache local) et resynchronise dès que ça revient — pensé pour la connexion capricieuse de Puerto.
- **Synchronisé** : la donnée vit dans Supabase (Postgres), pas dans le navigateur → iPhone ↔ Mac cohérents, et l'assistant peut écrire dedans.

## Architecture

```
index.html            ← le cockpit (UI + logique + config Supabase inline)
app/calendrier.html   ← vue calendrier live (⚠️ tourne uniquement dans Claude/Cowork,
                          via le connecteur Google Calendar — pas sur GitHub Pages)
```

- **Backend** : Supabase, projet dédié `voyage-mexique-2026`.
  Tables `voyage_kv` (statuts, checklist, budget, journal), `voyage_listings`,
  `voyage_messages`. RLS activée.
- **Clé** : le fichier embarque une *publishable key* Supabase. Elle n'ouvre l'accès
  qu'aux tables `voyage_*` (rôle anon) — les autres données du projet sont fermées par RLS.

## Déploiement (GitHub Pages)

1. Pousser ce dépôt sur GitHub (voir `push-to-github.sh`).
2. Repo → **Settings → Pages** → Source : branche `main`, dossier `/ (root)`.
3. Ouvrir l'URL `https://<user>.github.io/<repo>/` dans Safari → « Ajouter à l'écran d'accueil ».

## ⚠️ Note de sécurité

La publishable key est publique par nature. Combinée à une URL publique (Pages), n'importe qui
connaissant l'URL peut lire/écrire les données `voyage_*` (données de voyage, faible sensibilité).
Les données KPC du même projet Supabase restent protégées (rôle anon bloqué par RLS — vérifié).
Pour durcir : repo privé, ou passer les données perso dans un projet Supabase séparé, ou
ajouter une passphrase côté client.

## Réutilisation (template)

Le code est générique : seule la config Supabase (URL + clé, en haut du `<script>` de
`index.html`) est spécifique à une instance. Pour en faire un template partageable :
créer un projet Supabase vierge, appliquer le schéma `voyage_*`, remplacer la config.

## Roadmap (vers l'AI assistant)

- [ ] Agent négociation Airbnb : parsing d'annonces + réponses espagnol calibré + scoring
- [ ] Brief quotidien proactif (tâche planifiée)
- [ ] Calendrier embarqué via iCal public (pour marcher sur Pages)
- [ ] PWA offline complète (service worker)
- [ ] Réconciliation dépenses Pro/Perso au retour

---
Généré avec Alejandra (assistante exécutive de Seb) · Life OS.
