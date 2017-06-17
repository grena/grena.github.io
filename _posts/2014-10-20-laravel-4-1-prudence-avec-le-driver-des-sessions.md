---
title: "[FR] Laravel >= 4.1 : prudence avec le driver des sessions"
author: grena
layout: post
permalink: /laravel-4-1-prudence-avec-le-driver-des-sessions
disqus: http://www.grena.fr/laravel-4-1-prudence-avec-le-driver-des-sessions
path: 2014-10-20-laravel-4-1-prudence-avec-le-driver-des-sessions.md
---

> **TL;DR** : Pour éviter les ennuis, n'utilisez pas le driver par défaut pour les sessions, à savoir `native`, préférez quelque chose comme `redis` par exemple.

Avec Laravel 4.1 est venue une **refonte du système des sessions**, ils ont abandonnés le système qui fonctionnait très bien de Symfony pour... faire un truc à leur sauce, plus "maintenable" apparemment. Soit. Sauf qu'en cherchant bien un peu partout sur le web on tombe assez rapidement sur ce genre de résultats :

<img src="/assets/img/posts/google-laravel-sessions.png" class="align-center img-thumbnail">

Cela peut causer énormément de problèmes, comme les fameuses `TokenMismatchException` : le serveur, **aléatoirement**, ne détecte pas correctement la session, génère un nouveau token et invalide la requête avec un code d'erreur 500 et c'est très chiant dans le cas de requêtes concurrentes :

<img src="/assets/img/posts/laravel-sessions-mismatch.png" class="align-center img-thumbnail">

> A gauche, les `Session::token()` du serveur, à droite, le CSRF envoyé dans les headers de la requête

Comme l'explique [la documentation](http://laravel.com/docs/4.2/session#session-drivers) :

- `file` - sessions will be stored in app/storage/sessions.
- `cookie` - sessions will be stored in secure, encrypted cookies.
- `database` - sessions will be stored in a database used by your application.
- `memcached` / `redis` - sessions will be stored in one of these fast, cached based stores.
- `array` - sessions will be stored in a simple PHP array and will not be persisted across requests.

La configuration par défaut est mise à `native`, qui correspond en fait à `file`.

Et à moins que vous ne vouliez vous amuser à configurer entièrement le bousin qu'est PHP et à surcharger des configs à droite à gauche, vous allez vous retrouver avec des sessions branlantes gérées par les routines de base de PHP. Donc utilisez un driver plus sûr, tel que `redis` par exemple.
