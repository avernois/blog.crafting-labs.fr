---
layout: post
title: "Mythe : un code de qualité est largement commenté"
date: 2012-08-06 22:14:00 +0100
comments: false
categories: 
- "code"
- "commentaire"
- "craftsmanship"
- "mythe"
---
![useless comment2.jpg](https://blog.crafting-labs.fr/images/illustration/useless_comment2.jpg){: .left-image}
Quand j'aborde le sujet de la qualité du code avec un nouveau groupe, dans un coding dojo ou en établissant la signification de fini par exemple, il arrive toujours un moment comme ça :

> __dev__ : et il faut que tout soit largement commenté et que la javadoc soit à jour<br>
> __le groupe__ : ah ouais ! c'est vrai, c'est important<br>
> __moi__ : les commentaires, ça sert à rien<br>
> __le groupe__ : huh !?



Ok, je reconnais, c'est une approche un peu brutale, mais c'est volontaire. 
Car c'est vrai : la plupart des commentaires sont au mieux un bruit inutile dans le code, au pire un symptôme d'un code trop complexe et mal maîtrisé.

En fait, un commentaire peut servir à décrire trois types d'informations :

* quoi : ce que fait le code
* comment : comment il le réalise
* pourquoi : pourquoi il le fait comme ça et pas d'une autre façon

# Ce que fait le code
[![useless comment1.jpg](https://blog.crafting-labs.fr/images/illustration/.useless_comment1_s.jpg){: .right-image}
](/images/illustration/useless_comment1.jpg)La plupart du temps, on trouve ça dans un petit commentaire au-dessus de chaque classe et méthode. Les fameux commentaires javadoc[^1].

Bien souvent, la trame de ces commentaires est auto générée par l'IDE, et trop souvent laissé telle quelle.

Si vraiment, un besoin d'expliquer ce que fait la méthode/classe, c'est probablement qu'il faut changer son nom pour être plus explicite.
Et si trouver un nom est trop compliqué, c'est soit que l'élément concerné fait trop de trucs, soit qu'on ne sait pas vraiment ce qu'il fait.
Dans les deux cas, le commentaire ne sera au mieux qu'un pavé difficilement compréhensible par quelqu'un d'autre que son auteur[^2].

L'idée, c'est de ce dire que si on a besoin d'expliquer ce que fait le code, c'est qu'il faut le retravailler.

Parce que là est le problème des commentaires, c'est que très vite, ils deviennent obsolètes. Le code a changé, mais pas le commentaire qui va avec...
Donc quand on se base sur un commentaire d'un code qui a un peu vécu, la probabilité est assez élevé pour que le commentaire soit foireux. Et ne fasse que faire perdre du temps.

Alors que le code, lui, il fait ce qu'il fait. Et celui qui modifie une méthode, s'en sert, renomme la méthode si sa responsabilité a changé est dans l'ordre naturelle des choses (ou devrait l'être :).


Souvent, à ça on me rétorque un truc du genre :

> ouais, mais même si la responsabilité de ma méthode est bien définie, son nom ne peut pas forcément refléter les différents comportements qu'elle peut avoir.

C'est vrai. Le nom ne dira pas comment se comporte la méthode en cas d'erreur ou de cas particulier.
Le nom, non. Le code oui. Les cas particuliers, et les détails, c'est intéressant pour celui qui va se servir réellement de la méthode ou qui va devoir la modifier.

Encore plus fiable que le code, les tests unitaires seront votre meilleure documentation sur le fonctionnement d'une méthode. 

Contrairement à un commentaire, si un jour votre code ne fait plus ce qu'il faisait avant, les tests devront être corrigés pour passer et refléteront toujours la réalité. Si celui qui l'écrit est honnête, un test unitaire ne peut pas mentir.

Bon, encore faut-il faire des tests unitaires. J'en parlerai dans un prochain billet.

Note : pour ce qui est du commentaire qui parle du quoi, je fais une exception : il s'agit des API publiques. Je reviens dessus plus bas.

# Comment il le fait
[![useless comment.jpg](https://blog.crafting-labs.fr/images/illustration/.useless_comment_s.jpg){: .left-image}
](/images/illustration/useless_comment.jpg)Ces commentaires, on les retrouve directement dans le code. Il explique que là on démarre un bloc conditionnel, ou une boucle et qu'à tel autre endroit on le fini. Il dit que que c'est là qu'on gère les erreurs et ce qu'on fait dans ce cas là.

Waaah... En fait, ces commentaires servent juste à expliquer ce que le code nous raconte de lui même. 
Nan sérieux les gens, à moins que ce soit dans un contexte didactique, ce genre de commentaires n'a aucun intérêt : si vous ne savez pas lire du code, vous ne devriez probablement pas en écrire !

Plutôt que d'écrire un commentaire, prenez le temps d'écrire un code lisible et compréhensible pour ceux qui passeront après vous. Si ça se trouve, ça pourrait être vous :)[^3].

# Pourquoi il le fait comme ça

Voilà les rares commentaires qui trouvent grâce à mes yeux. Le pourquoi.

Je ne parle pas là du besoin, pourquoi on a écrit ce code, mais du pourquoi il est écrit comme ça.

Parce que des fois, souvent, on fait des choix sur la façon d'écrire les choses. Parfois de façon arbitraire, par goût. D'autres parce qu'il y a des contraintes extérieures pas forcément visible immédiatement.

Cela peut être l'utilisation d'une bibliothèque particulière parce que l'on va tourner sur un OS exotique, une contrainte métier bizaroïde, un cas particulier à gérer pour combler le défaut d'une bibliothèque externe, ...

Bref, ça c'est un commentaire très utile parce qu'il donne une information qui n'est pas déjà présente dans le code.

# le cas de l'API publique
Voilà un cas bien différent. Par nature, une api publique est un moyen d'intéragir avec votre code depuis l'extérieur de celui-ci.
L'utilisateur d'une api est extérieur au projet, il n'a probablement accès qu'à l'interface et pas au code, encore moins aux tests unitaires.

Il est donc indispensable que cette api soit bien documentée : que font les méthodes, quelles sont les entrées, les sorties, comment sont gérés les erreurs.

Dans le cas d'une api rendue publique, le problème de l'obsolescence est moins courant, tout simplement parce que l'api elle-même ne doit bouger que peu : une fois rendu publique, on ne peut pas changer sans arrêt cette api, ça serait un cauchemar pour ceux qui ont choisi de s'en servir.

Le commentaire complet prend donc tout son sens.

#Conclusion
Les commentaires sont utiles, mais ils ne doivent pas être redondants avec l'information que doit délivrer le code et ses tests.
Et donc : faites des tests unitaires ! :)

#TL;DR

> les tests me disent quoi, le code me dit comment, les commentaires me disent pourquoi.[^4]


[^1]: pour java, mais tous les langages ont plus ou moins l'équivalent
[^2]: voire son auteur lui même dès qu'un peu de temps aura passé
[^3]: ça pourrait aussi être un psychopathe, alors autant ne pas lui donner de raison de s'en prendre à vous :p
[^4]: je crois que c'est de [@jeromeavoustin](https://twitter.com/JeromeAvoustin)
