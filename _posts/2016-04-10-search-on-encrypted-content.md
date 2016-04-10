---
title: "[EN] Search on encrypted content"
author: grena
layout: post
permalink: /search-on-encrypted-content
disqus: http://www.grena.fr/search-on-encrypted-content
path: 2016-04-10-search-on-encrypted-content.md
---

Yesterday I was working on Gruik, especially on note encryption & UI integration.

> Ok so, I don't have to forget the search bar.. I'm gonna put the search bar here. Wait. How do we search in encrypted content?

Depression & fetal position.
Notes on Gruik are meant to be **encrypted client side**, for example: "_Hello World!_" will be saved in database with something like "*dkj8__//=ioa748z-*". The database only saves the encrypted content.

<div class="img-legend">
    <img src="/assets/img/posts/gruik-encryption1.png" class="img-thumbnail ">
</div>

So as a user, if I want to search every notes containing "Hello", I'm a bit stuck:

<div class="img-legend">
    <img src="/assets/img/posts/gruik-encryption2.png" class="img-thumbnail ">
</div>

As you can see, the server will gently respond "No sir, no note with 'Hello' inside, sorry."
After googling this subject, I found an interesting topic on StackExchange: http://crypto.stackexchange.com/questions/3446/is-it-possible-to-match-encrypted-documents-using-user-defined-search-terms
There are some kind of solutions, but it's hard to setup, at least, **with my current knowledge**. Plus I want Gruik to have a simple setup.

## An alternative search?
I can't really drop the search feature, neither **load all notes in client memory** in order to search on decrypted content...
So I came to this solution to continue the development:
- Text search won't be possible on private note (*encrypted ones*), but available on public ones
- We'll still be able to search notes with tags & maybe some kind of categories

If anyone has a nice solution to this, please let me know about it :)
