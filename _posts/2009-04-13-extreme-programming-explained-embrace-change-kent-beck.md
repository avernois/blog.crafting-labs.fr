---
layout: post
title: "Extreme Programming Explained: Embrace Change -- Kent Beck"
date: 2009-04-13 22:52:00 +0100
comments: false
categories: 
- "agilité"
- "chronique"
- "lecture"
- "xp"
---
[![beck-XP eplained.jpg](https://blog-img.crafting-labs.fr/couverture/.beck_-_XP_eplained_s.jpg){: .left-image}](
http://www.amazon.fr/gp/product/0321278658?ie=UTF8&tag=monbloamoique-21&linkCode=as2&camp=1642&creative=19458&creativeASIN=0321278658)
Quatrième de couverture :

> Software development projects can be fun, productive, and even daring. Yet they can consistently value to a business and remain under control.
Extreme Programming (XP) was conceived and developed to address the specific needs of software development conducted by small teams in the face of vague and changing requirements. This new lightweight methodology challenges many conventional tenets, including the long-held assumption that the cost of changing a piece of software necessarily rises dramatically over the course of time. XP recognizes that projects have to work to achieve this reduction in cost and exploit the savings once they have been earned. \\[...\\]


Dans [Extreme Programming Explained: Embrace Change](http://www.amazon.fr/gp/product/0321278658?ie=UTF8&tag=monbloamoique-21&linkCode=as2&camp=1642&creative=19458&creativeASIN=0321278658), Kent Beck décrit en détail ce qu'est ''eXtreme Programming (XP)'', méthode de développement logiciel dont il est à l'origine.

Le livre est classiquement décomposé en trois sections : 1/le problème, 2/La solution, 3/La mise en pratique.
Beck s'adresse directement à son lecteur, et celui-ci est clairement un développeur ou quelqu'un ayant directement les mains du coté technique des choses. 
Mêlant théorie, pratique, retour d'utilisateurs et expérience personnelle, Beck explique tous les détails de la méthode et en justifie ses force et son intérêt. Il ne néglige pas non plus de faire le tour des faiblesses : XP n'est pas la panacée du dev, il y a des cas où ça ne marchera pas et cela implique une réelle volonté de changer les choses.

Ce livre est vraiment une mine d'info, même si certains points[^1] nécessitent d'avantage d'éléments pour aller au bout des choses.

Si, je pense, le ton de ce bouquin peut vraiment parler à quelqu'un qui à un rapport direct avec du code, il peut avoir l'effet inverse sur des managers qui n'ont plus les mains dedans. Ce livre ne leur est pas destiné et peut même probablement leur faire peur (par son côté technique et la remise en cause d'une partie de leur job).

Dans les grandes lignes, XP se base sur quatre valeurs :

* __communication__
* __simplicité__
* __feedback__
* __courage__

Les trois premières sont assez classiques, la dernière est plus surprenante, et pourtant, elle est tout à fait justifiée. Pour faire un code simple, accepter de remettre son travail en cause régulièrement et que les autres le remettent aussi en cause, prendre le recul nécessaire, ..., ça demande du courage.

À ces valeurs s'ajoutent des bonnes pratiques :

* __planning game__
* __de petites livraisons__ : livrer peu mais souvent
* __métaphore__ 
* __design simple__ : KISS[^2] et YAGNI[^3]
* __tests__
* __refactoring__
* __programmation en binôme__ : binôme qui changent régulièrement, crée selon les besoins
* __propriété collective__ : tout le monde peut intervenir sur toute partie du code
* __intégration continue__ : 
* __40 heures par semaine__[^4]
* __client sur site__ : pour rester au plus près de ses attentes
* __coding standards__ : avoir un socle commun de règles valable pour tout le monde

L'idée est que si, prises séparément, ces bonnes pratiques ont des avantages et des inconvénients, prises toutes ensemble, elles se renforcent et s'auto entretiennent si bien qu'on en oublie les inconvénient pour ne garder que les avantages.
Toutes ces pratiques forment une cadre complet qui couvre l'intégralité du cycle de vie d'un logiciel : de la collecte des besoins de l'utilisateur, à la mise en production en passant par l'analyse, la planification et le développement bien sur :)

Après avoir lu ce livre, j'ai l'impression que Scrum en est essentiellement une réécriture destinée aux décideurs, avec un vocabulaire et un cadre qui leur parle et en cachant tous les détails trop techniques qui peuvent faire peur.

Achetez le sur amazon : [Extreme Programming Explained: Embrace Change](http://www.amazon.fr/gp/product/0321278658?ie=UTF8&tag=monbloamoique-21&linkCode=as2&camp=1642&creative=19458&creativeASIN=0321278658) de Kent Beck


[^1]: le planning par exemple, qui fait l'objet d'un livre pour lui tout seul: [Planning Extreme Programming](http://www.amazon.fr/gp/product/0201710919?ie=UTF8&tag=monbloamoique-21&linkCode=as2&camp=1642&creative=19458&creativeASIN=0201710919)
[^2]: Keep It Stupidly Simple
[^3]: You Ain't Gonna Need It
[^4]: bon, en France, ça serait plutôt 35h :)
