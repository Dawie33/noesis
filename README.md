# Noesis

Encyclopédie personnelle générée par IA : tape un sujet, obtiens une fiche complète (explication, images, vidéos, quiz).

## L'idée

Une encyclopédie de poche qui se construit au fil de ta curiosité. Tape n'importe quel sujet — *"comment se forme un tsunami"*, *"pourquoi Rome est tombée"* — et l'application génère une fiche de connaissance complète :

- Une **explication claire**, structurée en étapes ou en sections
- De **vraies sources** trouvées sur le web (vidéos, articles, livres)
- Un **quiz** pour vérifier ce qui est resté
- Des **sujets connexes** pour continuer à creuser

Chaque fiche explorée s'ajoute à un historique personnel.

## Stack technique

- **Framework** : [Nuxt 3](https://nuxt.com) (Vue 3 + serveur Nitro intégré, tout en JavaScript)
- **IA** : API Claude (Anthropic)
- **Recherche web/images** : API de recherche externe (Tavily / Serper — à trancher)
- **Base de données** : SQLite + [Drizzle ORM](https://orm.drizzle.team)

## Structure du projet

```
noesis/
├── pages/
│   └── index.vue           # page principale : formulaire + fiche
├── components/
│   ├── FicheCard.vue
│   └── QuizWidget.vue
├── server/
│   ├── api/
│   │   └── fiche.post.js   # reçoit un sujet, orchestre Claude + recherche, renvoie la fiche
│   └── utils/
│       ├── claude.js       # client Anthropic
│       └── search.js       # client API de recherche
├── db/
│   └── schema.js           # schéma Drizzle (fiches, quiz, historique)
├── nuxt.config.js
└── package.json
```

## Installation

```bash
git clone <repo>
cd noesis
npm install
```

Créer un fichier `.env` à la racine :

```
ANTHROPIC_API_KEY=sk-ant-...
SEARCH_API_KEY=...
```

Lancer le serveur de dev :

```bash
npm run dev
```

L'app est disponible sur `http://localhost:3000`.

## Roadmap

- [ ] V1 — génération de fiche texte (explication + quiz), stockage en base
- [ ] V2 — recherche web réelle (images, vidéos, sources)
- [ ] V3 — historique visuel des sujets explorés + suggestions de sujets connexes
- [ ] V4 — quiz à répétition espacée (rappel automatique quelques jours après)

## Licence

Projet personnel — pas de licence définie pour l'instant.