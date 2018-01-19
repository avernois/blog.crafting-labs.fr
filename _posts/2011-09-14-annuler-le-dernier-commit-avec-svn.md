---
layout: post
title: "annuler un commit avec svn"
date: 2011-09-14 10:15:00 +0100
comments: false
categories: 
---
![subversion logo.png](https://blog-img.crafting-labs.fr/logo/.subversion_logo_s.jpg){: .left-image}
Si c'est trivial avec git, avec svn annuler les modifs du dernier commit n'est pas forcement évident.
C'est même impossible, svn ne donne pas le droit à l'erreur et n'a aucun moyen d'oublier un commit.

Par contre, ce qui est tout a fait possible et assez simplement, c'est de remettre le code de sa copie locale dans l'état précédent le commit malheureux et committer cet état.


{% highlight bash %}
svn merge -r [révision_erreur]:[révision_correcte] [url]
{% endhighlight %}

où :

* `révision_erreur` est la révision qui pose problème
* `révision_correcte` est la révision précédent le commit foireux (généralement révision_erreur -1, mais on pourrait imaginer revenir en arrière de plusieurs commit)
* `url` le chemin de l'arbre concerné par l'annulation

Cette manipulation va retirer toutes les changements réalisés entre `révision_correcte` et `révision_erreur`.
On peut donc de cette manière annuler un commit même si d'autres ont été fait depuis[^1]

Pour annuler juste le dernier commit, on peut utiliser les alias de révion :

{% highlight bash %}
svn merge -r COMMITED:PREV [url]
{% endhighlight %}

Et pour annuler tous les commits effectués depuis une `révision` [^2]: 

{% highlight bash %}
svn merge -c -[révision]
{% endhighlight %}

Bien sur, il ne faudra pas oublier de commiter ce retour arrière :

{% highlight bash %}
svn commit -m "On annule le dernier commit et on revient à la version [révision_courante]"
{% endhighlight %}


[^1]: évidement, si vous avez fait des commits sur la partie impactée par le problème, ça risque de mal se passer
[^2]: il ne faut pas oublier le __-__ devant le numéro de révision
