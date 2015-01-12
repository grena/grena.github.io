---
title: "git : bien choisir ce que l'on veut commit"
author: grena
layout: post
permalink: /git-bien-choisir-ce-que-lon-veut-commit
disqus: http://www.grena.fr/git-bien-choisir-ce-que-lon-veut-commit
path: 2015-01-12-git-bien-choisir-ce-que-lon-veut-commit.md
---

J'ai intégré une nouvelle entreprise en ce début d'année, l'occaz de faire de nouvelles rencontres et d'apprendre plein de nouveaux trucs \o/
Bon alors je sais, on trouve des milliards de trucs pour **git**, mais je mets ça ici, comme ça je l'aurai sous le coude.

Prenons un simple fichier **A.txt** :
{% highlight javascript %}
function print(text) {
    console.log(text);
}
{% endhighlight %}

Tac, je commence à trifouiller, j'ouvre **A.txt**, et j'écris un peu.
Voici le nouveau fichier **A.txt** :
{% highlight javascript %}
function print(text) {
    console.log(text);
}

function fire() {
    print('BOOM !');
}

function water() {
    print('PLOUF !');
}
{% endhighlight %}

Un petit `git diff` nous donne :
{% highlight diff %}
diff --git a/A.txt b/A.txt
index 9431404..2c137ce 100644
--- a/A.txt
+++ b/A.txt
@@ -1,3 +1,12 @@
 function print(text) {
    console.log(text);
 }
+
+function fire() {
+    print('BOOM !');
+}
+
+function water() {
+    print('PLOUF !');
+}
+
(END)
{% endhighlight %}

### Vraiment choisir ce qu'on veut commit

C'est un cas relativement courant.
On ouvre le même fichier, pour ajouter plusieurs trucs qui n'ont pas forcément rapport.

Il est possible de **scinder les commits, même si les changements sont sur un seul fichier**.
Mettons que l'on veuille faire un commit pour chaque nouvelle fonction ajoutée, on va utiliser la commande

```plain
git add -p
```

Cette commande va nous ouvrir notre éditeur pour afficher **bloc par bloc** les diff que nous avions précédemment, avec une ligne supplémentaire en bas :

```plain
Stage this hunk [y,n,q,a,d,/,e,?]?
```

> "hunk" veut dire "bloc" en anglais, ce sont les parties que git estime comme **une seule modification**

On peut évidemment afficher l'aide en entrant `?` pour voir ce que toutes ces options font :

```plain
y - stage this hunk
n - do not stage this hunk
q - quit; do not stage this hunk or any of the remaining ones
a - stage this hunk and all later hunks in the file
d - do not stage this hunk or any of the later hunks in the file
g - select a hunk to go to
/ - search for a hunk matching the given regex
j - leave this hunk undecided, see next undecided hunk
J - leave this hunk undecided, see next hunk
k - leave this hunk undecided, see previous undecided hunk
K - leave this hunk undecided, see previous hunk
s - split the current hunk into smaller hunks
e - manually edit the current hunk
? - print help
```

Comme on peut le voir au diff ci-dessus, les modifications que l'on a effectuées sont dans le "même bloc", elles se suivent.
On peut éditer un bloc pour indiquer manuellement à git ce qu'il y a à retirer / garder.

On va pour cela utiliser l'option `e` : **manually edit the current hunk**.
L'éditeur s'ouvre :

{% highlight diff %}
# Manual hunk edit mode -- see bottom for a quick guide
@@ -1,3 +1,12 @@
 function print(text) {
    console.log(text);
 }
+
+function fire() {
+    print('BOOM !');
+}
+
+function water() {
+    print('PLOUF !');
+}
+
# ---
# To remove '-' lines, make them ' ' lines (context).
# To remove '+' lines, delete them.
# Lines starting with # will be removed.
#
# If the patch applies cleanly, the edited hunk will immediately be
# marked for staging. If it does not apply cleanly, you will be given
# an opportunity to edit again. If all lines of the hunk are removed,
# then the edit is aborted and the hunk is left unchanged.
{% endhighlight %}

Tout est très bien expliqué ici. Dans le cas d'ajout (_on n'a que ça dans ce bloc_), on peut les retirer en supprimant simplement les lignes.
Moi je veux faire **un premier commit** pour la **première fonction**, puis **un deuxième** pour l'autre :
Donc j'édite pour finalement me retrouver avec :

{% highlight diff %}
# Manual hunk edit mode -- see bottom for a quick guide
@@ -1,3 +1,12 @@
 function print(text) {
    console.log(text);
 }
+
+function fire() {
+    print('BOOM !');
+}
+
# ---
# To remove '-' lines, make them ' ' lines (context).
# To remove '+' lines, delete them.
# Lines starting with # will be removed.
#
# If the patch applies cleanly, the edited hunk will immediately be
# marked for staging. If it does not apply cleanly, you will be given
# an opportunity to edit again. If all lines of the hunk are removed,
# then the edit is aborted and the hunk is left unchanged.
{% endhighlight %}

Je sauvegarde, et voilà !

{% highlight sh %}
➜  test git:(master) ✗ git status
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

    modified:   A.txt

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

    modified:   A.txt
{% endhighlight %}

Ce que l'on va commit, c'est ce que j'ai laissé plus haut, la fonction `print()`.
D'ailleurs, si je regarde ce qui n'a pas été "staged" dans le commit actuel avec un `git diff` :

{% highlight diff %}
diff --git a/A.txt b/A.txt
index 62a96cc..2c137ce 100644
--- a/A.txt
+++ b/A.txt
@@ -6,3 +6,7 @@ function fire() {
     print('BOOM !');
 }

+function water() {
+    print('PLOUF !');
+}
+
(END)
{% endhighlight %}

Il reste bien la function `water()`, que l'on pourra commit plus tard ;)

### Les hunks

Pour bien capter la notion de hunk, on va reprendre notre exemple du dessus, sauf que je vais modifier différemment le fichier **A.txt** :

{% highlight diff %}
diff --git a/A.txt b/A.txt
index 9431404..cb56ec4 100644
--- a/A.txt
+++ b/A.txt
@@ -1,3 +1,12 @@
+function fire() {
+    print('BOOM !');
+}
+
 function print(text) {
    console.log(text);
 }
+
+function water() {
+    print('PLOUF !');
+}
+
(END)
{% endhighlight %}

J'ai juste mis la function `fire()` au dessus cette fois.
On remarque bien qu'il y a 2 hunks éventuels dans ce diff.

Une fois `git add -p` lancé, on va pouvoir choisir l'option `s` : **split the current hunk into smaller hunks**

{% highlight diff %}
--- a/A.txt
+++ b/A.txt
@@ -1,3 +1,12 @@
+function fire() {
+    print('BOOM !');
+}
+
 function print(text) {
    console.log(text);
 }
+
+function water() {
+    print('PLOUF !');
+}
+
{% endhighlight %}

Je choisi de spliter les hunks avec `s` :

```
Stage this hunk [y,n,q,a,d,/,s,e,?]? s
```

Il m'informe donc du nombre de bloc qu'il a automatiquement trouvé :

```
Split into 2 hunks.
```

Et là, il va commencer à faire défiler **un à un** les blocs qu'il a trouvé pour me demander ce que je veux en faire, avec toutes les options que l'on connait.

{% highlight diff %}
@@ -1,3 +1,7 @@
+function fire() {
+    print('BOOM !');
+}
+
 function print(text) {
    console.log(text);
 }
Stage this hunk [y,n,q,a,d,/,j,J,g,e,?]?
{% endhighlight %}

On va donc pouvoir choisir d'ajouter ou non chaque bloc (_hunk_) dans notre commit via `y` ou `n`, ou encore de spliter ces blocs etc..
Très puissant donc !







