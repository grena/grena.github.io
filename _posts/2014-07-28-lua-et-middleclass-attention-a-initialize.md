---
title: "[FR] Lua et Middleclass, attention à initialize() (Obsolète)"
author: grena
layout: post
permalink: /lua-et-middleclass-attention-a-initialize
disqus: http://www.grena.fr/lua-et-middleclass-attention-a-initialize
path: 2014-07-28-lua-et-middleclass-attention-a-initialize.md
---

> Edit : Comme me l'a signalé un [excellent ami](https://github.com/socketubs), l'`initialize()` fonctionne très bien, il s'agissait **d'une erreur dans mon code**. Le code donné en exemple dans cet article fonctionne bien, et je vous invite à lire l'article pour ne pas se viander comme je l'ai fait ! Note : pour le coup, le facepalm, c'est pour moi \o/

---------

Si en Lua vous utilisez [Middleclass](https://github.com/kikito/middleclass) - _librairie vous offrant une interface pour implémenter l'OOP dans votre projet_ -, alors il va falloir faire attention à un truc lors de l'`initialize()`.

Le cas est le suivant :

{% highlight lua %}
local class = require 'middleclass'

local Position = class('Position')

function Position:initialize(x, y)
    self:set(x, y)
end

function Position:set(x, y)
    self.x = x
    self.y = y
end

local Entity = class('Entity')

function Entity:initialize()
    self.position = Position:new(0, 0)
end
{% endhighlight %}

Rien de bien compliqué ici, j'ai une classe `Position` qui représente une coordonnée {x,y} et une classe `Entity` qui possède une `Position`.

Maintenant jouons un peu avec ces classes pour voir où ça coince :

{% highlight lua %}
dog = Entity:new()
cat = Entity:new()

dog.position:set( 10, 50 )
cat.position:set( 30, 30 )
{% endhighlight %}

Niquel, c'est esthétique, le clébard et le matou sont bien à leur place.

**ET BIEN NON.**

### Le problème

`dog` sera à la même position que `cat` dans cet exemple ! N'importe qui venant du monde OOP pourrait penser (à juste titre) que lors de l'appel de l'`initialize()` de chaque `Entity`, soit :

{% highlight lua %}
function Entity:initialize()
    self.position = Position:new(0, 0)
end
{% endhighlight %}

... chaque entity créerait une nouvelle `Position` (d'où le `new`) ! Que neni. Alors, bug dans la matrice ? Bug de la lib ? En tout cas soyez prudents, c'est un coup à tourner en rond pour le debug...

Voici donc comment il faut procéder :

{% highlight lua %}
dog = Entity:new()
cat = Entity:new()

dog.position = Position:new( 10, 50)
cat.position = Position:new( 30, 30)
{% endhighlight %}

A partir de là, un objet `Position` a bien été instancié pour chaque `Entity` avec la bonne adresse mémoire !

**NOTEZ** qu'ici, il s'agit de référence d'une autre classe, mais ce problème **est aussi présent si vous faites référence à une fonction**, par exemple pour générer de l'aléatoire sur un attribut de votre classe, ainsi :

{% highlight lua %}
local Entity = class('Entity')

function Entity:initialize()
    self.size = math.random( 15, 80 )
end
{% endhighlight %}

Vous générera un seul aléatoire et toutes vos Entity auront le même...
