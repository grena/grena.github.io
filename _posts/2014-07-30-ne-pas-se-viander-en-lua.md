---
title: [FR] Ne pas se viander en Lua
author: grena
layout: post
permalink: /ne-pas-se-viander-en-lua
disqus: http://www.grena.fr/ne-pas-se-viander-en-lua
path: 2014-07-30-ne-pas-se-viander-en-lua.md
---

Suite à [cet article](http://www.grena.fr/lua-et-middleclass-attention-a-initialize/) où je rage contre un comportement étrange de Middleclass, je me devais de créer un autre article pour expliquer où était mon erreur dans mon code (la vraie erreur, hein).

**TL;DR** : _L'appel avec un `.` fait appel à la méthode de classe et nécessite donc le passage du contexte explicitement (self), l'appel avec `:` se sert de l'appelant comme contexte implicite._

Quand j'ai débarqué en Lua, je ne comprenais pas forcément pourquoi on appelait certaines méthodes d'un objet avec `.` et d'autres avec `:` . Et bien c'est une histoire de contexte.

### Mettons nous en situation

Mettons en place de quoi nous amuser, une simple classe position

{% highlight lua %}
local Position = class('Position')

function Position:initialize(x, y)
    self:set(x, y)
end

function Position:set(x, y)
    self.x = x
    self.y = y
end

function Position:__tostring()
    return 'Position: [x:' .. tostring(self.x) .. ', y:' .. tostring(self.y) .. ']'
end
{% endhighlight %}

Puis une classe et sa fille

{% highlight lua %}
local Entity = class('Entity')

function Entity:initialize()
    self.position = Position:new(0, 0)
end

local MovingEntity = class('MovingEntity', Entity)

function MovingEntity:initialize()
    Entity:initialize(self)
end
{% endhighlight %}

Maintenant si on les trifouille un peu :

{% highlight lua %}
local paul = MovingEntity:new()
local jack = MovingEntity:new()

print(paul.position)    -- Position: [x:0, y:0]
print(jack.position)    -- Position: [x:0, y:0]

paul.position:set(50, 50)

print(paul.position)    -- Position: [x:50, y:50]
print(jack.position)    -- Position: [x:50, y:50] !
{% endhighlight %}

**BIM !** Jack a aussi la position de Paul maintenant.

{% highlight lua %}
function MovingEntity:initialize()
    Entity:initialize(self)
end
{% endhighlight %}

### Le self

En Lua, chaque méthode d'un objet a besoin d'un contexte, le fameux `self`. Lorsque je fais :

{% highlight lua %}
monObjet:maMethode()
{% endhighlight %}

Le `self` est implicitement passé en premier argument ! Ainsi à l'intérieur de la méthode, le `self` sera bien `monObjet`, l'appelant.

Maintenant si je fais :

{% highlight lua %}
monObject.maMethode()
{% endhighlight %}

Je fais en fait appel à la méthode de manière "brute", en passant par la classe, il faut à ma méthode **un contexte**, elle a besoin de son `self` nom de Zeus !

Note :

{% highlight lua %}
-- Si l'on a monObjet instance de maClass :
monObjet:maMethode()

-- Revient à faire...
maClass.maMethode( monObjet )
{% endhighlight %}

### Bilan et correction du code

Rectifions maintenant le tir avec ce qu'on sait, et voyons donc ce que ça implique, correction de la classe donc :

{% highlight lua %}
function MovingEntity:initialize()
    Entity.initialize(self)
end
{% endhighlight %}

Voilà, maintenant avec notre jeu d'essai :

{% highlight lua %}
local paul = MovingEntity:new()
local jack = MovingEntity:new()

print(paul.position)    -- Position: [x:0, y:0]
print(jack.position)    -- Position: [x:0, y:0]

paul.position:set(50, 50)

print(paul.position)    -- Position: [x:50, y:50]
print(jack.position)    -- Position: [x:0, y:0]
{% endhighlight %}

Niquel.

### Caveats

Bon alors vous l'aurez compris je suis pas hyper fan de ce système... ça peut laisser place (_dans le sens, "autoriser"_) à des choses ultra tricky, genre :

{% highlight lua %}
local paul = MovingEntity:new()
local jack = MovingEntity:new()

print(paul.position)    -- Position: [x:0, y:0]
print(jack.position)    -- Position: [x:0, y:0]

paul.position.set(jack.position, 50, 50)   -- Bien noter le '.set' et pas ':set'

print(paul.position)    -- Position: [x:0, y:0]
print(jack.position)    -- Position: [x:50, y:50]
{% endhighlight %}

Ici je change la position de jack avec paul. `paul.position` me sert juste à accéder à l'instance de la classe `Position`. Maintenant j'appel `.set()`, à savoir la manière "brute", en attaquant directement la classe de `paul.position` , soit `Position`, ainsi la signature devient : `.set(context, x, y)`

M'voyez. Alors, ça reste logique puisque ça respecte ce qu'on a évoqué plus haut, mais je trouve ça juste bof de pouvoir faire un appel de classe en passant par une instance, mais c'est une question de goût !
