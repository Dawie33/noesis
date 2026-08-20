# CLAUDE.md

Ce fichier donne le contexte du projet **Noesis** pour travailler efficacement dessus.

## Le projet

Noesis est une encyclopédie personnelle générée par IA. L'utilisateur tape un sujet, l'app génère une fiche de connaissance : explication structurée, sources réelles (web), quiz, sujets connexes. Voir `README.md` pour la description complète.

## Stack

- **Nuxt 3**, en **JavaScript pur** (pas de TypeScript — merci de ne pas introduire de fichiers `.ts` sauf demande explicite)
- **Vue 3** (Composition API, `<script setup>`) pour les composants
- **Nitro** (routes serveur natives Nuxt, dans `server/api/`) pour le backend
- **SQLite** + **Drizzle ORM** pour la persistance
- **API Claude** (Anthropic) pour la génération de contenu
- **API de recherche web** (Tavily ou Serper) pour images/vidéos/sources — le choix final n'est pas encore figé, vérifier `server/utils/search.js` avant de supposer un provider

## Conventions de code

- Composants Vue : `<script setup>`, pas d'Options API
- Nommage des fichiers composants : PascalCase (`FicheCard.vue`)
- Nommage des routes API : `server/api/<ressource>.<methode>.js` (ex: `fiche.post.js`)
- Pas de framework CSS lourd imposé — rester simple (CSS scoped dans les composants, ou variables CSS globales)
- Les appels à l'API Anthropic et à l'API de recherche passent toujours par `server/utils/`, jamais directement depuis un composant Vue (le frontend ne doit jamais voir les clés API)

## Commandes utiles

```bash
npm run dev          # serveur de dev sur localhost:3000
npm run build         # build de production
npx drizzle-kit generate   # générer une migration après modif du schéma
npx drizzle-kit migrate    # appliquer les migrations
```

## Variables d'environnement attendues

```
ANTHROPIC_API_KEY=
SEARCH_API_KEY=
```

Ne jamais committer le fichier `.env`.

## Points d'attention

- Le format de sortie attendu du modèle Claude pour une fiche est un **JSON structuré** (titre, sections d'explication, liste de questions de quiz, mots-clés pour la recherche de sources). Si tu modifies le prompt de génération, garde ce contrat JSON stable pour ne pas casser le frontend.
- Le projet est encore en V1 : privilégier la simplicité et la lisibilité du code plutôt que l'optimisation prématurée.
- Toujours garder l'app mono-utilisateur en tête pour l'instant (pas d'authentification prévue à ce stade).