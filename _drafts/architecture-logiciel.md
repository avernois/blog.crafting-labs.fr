---
layout: post
title: "architecture logicielle"
categories: 
- "agilité"
- "architecture logicielle"
---
![2010.03.16_m.jpg](https://blog.crafting-labs.fr/images/illustration/.2010.03.16_m_s.jpg){: .left-image}

Sur la liste de diffusion d'un JUG, au détour d'une conversation animée sur langage statique ''vs'' langage dynamique, je tombe sur cette petite phrase :

> Personnellement en tant qu'architecte logiciel je préfère toujours partir du postulat les développeurs sont mauvais, entre 2 choix ils prendront toujours le moins bon... ca me permet d'avoir de bonnes surprises par moments et dans la plupart des cas d'avoir anticipé les problèmes.

Ma réponse immédiate commençait par un 

> argh... sic... au secours...

Et devant mes cris d'orfraie effrayé, après une appréciable tentative de médiation[^1] rappelant l'importance des architectures simples et faciles à comprendre, ce monsieur de renchérir :

> Si je peux me permettre l'adjectif ''simple'' n'est pas assez explicite à mon gout : moi je dis ''privilégions les environnements qui cadrent l'activité de développement''.
>
> J'entends par ''environnement'' : les outils, les frameworks et l'architecture logicielle du projet.__''}}


Et de nouveau 

> argh... sic... au secours...

C'est là, à mon avis, une déviance assez grave.
L'idée, c'est de restreindre les possibilités des développeurs et de les empêcher de faire leur métier et d'exprimer leurs compétences... et ça dans l'idée que ça les empêchera de faire de potentielles erreurs. Donc c'est contraindre, rigidifier plutôt que d'expliquer et d'éduquer. Faites ceci, parce que ceci est bon, c'est moi qui vous le dis.

Personnellement, j'ai tendance à prendre l'approche totalement inverse. Accompagner l'équipe dans sa conception de l'archi, et leur expliquer le pourquoi des bonnes pratiques, des choses à faire et à ne pas faire. En bref, partager plutôt que contraindre.

À mon sens, c'est ce qui assurera l'autonomie et permettra de réaliser proprement des fonctionnalités qui n'étaient pas prévues initialement.


Alors, non, je ne vais pas jeter des pierres sur ce monsieur. Déjà, ça n'est pas mon genre et surtout, il n'est qu'un exemple parmi tant d'autre, digne représentant du ''mythe'' de l'Architecte Logiciel. L'homme ultime qui sait prévoir la structure d'un logiciel alors même qu'on ne sait pas encore réellement ce qu'il va faire. Je connais même des sociétés dans lesquels il y a des groupes complets d'architectes, qui ne voient jamais une ligne de code d'une application réelle. 


Cette petite histoire m'a donné l'occasion de relire l'article de Mike Fowler [Who needs an architect ?](http://martinfowler.com/ieeeSoftware/whoNeedsArchitect.pdf) qui date déjà de 2003. Il revient sur la notion d'architecture et sur les architectes. Ils les classent en deux espèces :

###Symptômes :

* intervient uniquement en début ne projet. 
* vous prescrit trois couches dès que vous dites JEE sans avoir entendu la finalité de votre appli. 
* fait tous les choix au début du projet
* répond à vos ''pourquoi ?'' par des ''Parce que c'est la bonne pratique
* s'en va dès que les dev ont commencé, mais reste joignable par téléphone
* vous n'avez toujours pas compris ce qu'il fallait mettre dans la couche application

Diagnostique : vous êtes en présence d'un ''Architectus Reloadus''

Prescription : fuyez...

###Symptomes :

* fait partie de l'équipe de dév
* guide l'équipe vers des choix
* apprend et explique pourquoi des pratiques sont bonnes
* écrit du code

Diagnostique : vous êtes en présence d'un ''Architectus Oryzus'', ou plus simplement d'un guide.

Prescription : c'est un animal rare et précieux. Reconnaissez sa valeur, chouchoutez le :)


[^1]: merci Bruno
