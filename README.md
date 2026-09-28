# Introduction étape par étape au framework Vue.js

📖 **Lire le tutoriel : [https://stahe.github.io/vuejs-etape-par-etape-sept-2026/](https://stahe.github.io/vuejs-etape-par-etape-sept-2026/)**

Ce cours vous apprend à écrire une application web avec le framework [Vue.js](https://vuejs.org) 3 : une application **à page unique** (SPA), dont les pages sont fabriquées **dans le navigateur**, à partir des données JSON d'un serveur.

Il fait suite au cours [Introduction étape par étape au framework web NestJS](https://stahe.github.io/nestjs-html-sept-2026/), dont il change le point de vue :

| Cours NestJS | Cours Vue.js |
|---|---|
| le serveur fabrique les pages HTML (Handlebars) | le navigateur fabrique les pages (Vue.js) |
| le navigateur affiche ce qu'il reçoit | le serveur ne renvoie que du JSON |
| contrôleurs, vues, `res.render` | composants `.vue`, routeur, stores |
| dictionnaires lus par le serveur | dictionnaires dans le client (vue-i18n) ; le serveur ne renvoie que des clés |
| message flash dans un cookie | message flash dans un store Pinia |

Les pages, elles, ne changent pas : ce sont celles de l'application **RdvMedecins** déjà présentée avec les autres frameworks.

## L'approche : de nombreux petits exemples, puis une étude de cas

Le cours s'articule autour de **20 petits exemples**, chacun centré sur une notion. Ils partagent une seule commande `npm install` et un seul serveur de développement (Vite), qui affiche leur sommaire.

| Chapitre | Contenu | Exemples |
|---|---|---|
| Premiers pas | un projet Vite, `ref` / `reactive` / `computed` / `watch`, directives, événements, formulaires, validation | 01–06 |
| Les composants | props, événements, `v-model` sur un composant, slots, cycle de vie, composables, `provide` / `inject`, fenêtre de confirmation | 07–12 |
| Le routage | vue-router, paramètres, query, gardes de navigation, chargement différé | 13–14 |
| L'état partagé | les stores Pinia, `localStorage` | 15 |
| Internationalisation | vue-i18n : paramètres, pluriels, dates, nombres | 16 |
| Le serveur, une boîte noire | installation du serveur JSON, son API, 48 exemples `curl` | – |
| Dialoguer avec le serveur | `fetch`, proxy de Vite, cookie `httpOnly`, couche d'accès à l'API, erreurs du serveur | 17–20 |

Chaque exemple est présenté avec son code complet, commenté ligne par ligne, et une copie d'écran de son exécution.

## Le serveur : une boîte noire

Le serveur est le serveur NestJS du cours précédent, dont les contrôleurs renvoient maintenant du **JSON**. Le cours le traite comme une **boîte noire** : on l'installe, on étudie son API, on l'interroge avec `curl` — mais on n'a pas besoin de lire son code (fourni et commenté pour les curieux).

- toutes les erreurs ont la même forme : `{ "statusCode": 409, "cle": "ERRORS.LOGIN_TAKEN", "params": {...}, "champs": {...} }` — des **clés** de traduction, jamais de texte ;
- authentification par jeton JWT dans un cookie `httpOnly` / `sameSite=strict` : le code JavaScript du client ne voit jamais le jeton ;
- protection CSRF : cookie `sameSite`, et tout POST doit être en JSON ;
- un « mode test » du captcha pour pouvoir interroger l'API avec `curl`.

## L'étude de cas : le client Vue.js de RdvMedecins

Une application complète de **prise de rendez-vous dans un cabinet médical**, dont **tous** les fichiers (une quarantaine) sont listés et commentés.

- **Trois rôles** : `ADMIN` (gère les médecins et les clients), `DOCTOR` (prend et annule les rendez-vous), `USER` (le patient : réserve pour lui-même, gère son compte).
- **Confidentialité** : un patient ne reçoit jamais le nom des autres patients — le serveur ne l'envoie pas.
- **Tout l'état de la page dans l'URL** : `/agenda?idMedecin=1&jour=2026-10-05&reserver=7` rouvre la fenêtre de réservation après un F5 ; les boutons Précédent / Suivant fonctionnent.
- **Validation par le serveur** : les formulaires affichent sous chaque champ les erreurs renvoyées par l'API ; verrou optimiste, homonymes, login déjà pris...
- **Session** : rétablie après un F5 (`GET /api/auth/moi`), expiration gérée en un seul endroit (réponse 401).
- **Français / anglais**, fenêtre de confirmation accessible au clavier, Bootstrap 5.
- **Déploiement** : le client compilé est servi par le serveur JSON lui-même (même origine, pas de CORS).

## Technologies

Vue.js 3.5 (Composition API, `<script setup>`) · TypeScript 5.9 · Vite 7 · vue-router 4 · Pinia 3 · vue-i18n 11 · Bootstrap 5 · côté serveur : NestJS 10 · TypeORM · MySQL 8 / MariaDB · Passport JWT · svg-captcha

## Prérequis

- Des bases de JavaScript (ou TypeScript), de HTML et du protocole HTTP.
- Node.js 22 (ou 20.19 au moins), Visual Studio Code avec l'extension Vue (Official), un serveur MySQL (par exemple Laragon sous Windows) pour le serveur JSON. Les instructions d'installation sont données dans les annexes du cours.

## Auteur

Ce cours, ses exemples, le serveur JSON et l'étude de cas ont été rédigés par **Claude**, l'IA d'[Anthropic](https://www.anthropic.com) (septembre 2026) à la demande de **Serge Tahé**.
