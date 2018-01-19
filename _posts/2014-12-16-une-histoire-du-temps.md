---
layout: post
title: "Une histoire de temps"
date: 2014-12-16 16:17:00 +0100
comments: false
categories: 
---
[![2010.06.05-montre m.jpg](https://blog-img.crafting-labs.fr/illustration/.2010.06.05-montre_m_s.jpg){: .left-image}
](https://blog-img.crafting-labs.fr/illustration/2010.06.05-montre_m.jpg)Lorsque je donne des formations ou des conférences, j'utilise tout un tas de petites anecdotes, des histoires qui me sont arrivées au cours de ma carrière.
Il y en a une en particulier que j'utilise lorsque je veux parler de la mauvaise notion du temps que l'on peut avoir parfois. On a pas le temps de faire des tests, on ne peut pas prendre le temps de faire de la qualité, car il faut avancer les fonctionnalité, corriger les bugs...


Il y a donc quelques temps, j'intervenais dans une équipe d'un très gros projet avec d'énormes problèmes de défauts, de qualité, et des temps de développement surréalistes.
Et pourtant, quand on écoutait les développeurs et qu'on les regardait faire, il était impossible de dire qu'ils glandouillaient joyeusement. Non, ça bossait dur. Et en plus, ils étaient techniquement très compétents.

Pour comprendre ce paradoxe, j'ai demandé à un développeur si je pouvais bosser avec lui pour la journée, que je vois comment ça se passe de l'intérieur. Pas de soucis.
Me voilà donc à suivre un développeur. Ce jour là, il s'attaquait à un défaut. Le développeur avait une bonne idée de l'endroit du problème.
Il n'y a aucun doute à avoir sur le fait qu'il maîtrisait son produit et ses outils.

Le voilà donc en quête de la zone, qu'il trouve rapidement et pour confirmer ses doutes, il rajoute quelques `print(toto)` et autres `print(on est passé par là)`[^1].


>-- donc maintenant, on compile, on exécute et on vérifie les logs ?

>-- yep. Sauf que, on a pas tout le nécessaire pour compiler sur nos machines, c'est trop long et compliqué, on envoie ça sur un serveur de compil.

>-- ok.

>-- vu la queue actuelle, y'en a pour 20 min[^2].

20 min plus tard, on récupère le package.


>-- donc là, on installe et on vérifie

>-- oui, mais toujours pas sur ma machine, on a des environnements pour ça, d'ici 20 min ça sera déployé.

20 min plus tard, on peut enfin utiliser l'application. On reproduit, le bug. On fouille les logs à la recherche des `toto`. Et drame... pas de `toto`.

On retourne sur le code, on rajoute plus de `print`. Partout. Puis on envoie en compile. 20 min. Puis on déploie. 20min. Puis on reproduit le bug, on fouille les logs. Ouf, ils sont là. Ils sont clairs, on sait maintenant quel est le problème.

On retourne sur le code, on corrige le défaut[^3]. Puis on envoie en compile. 20 min. Puis on déploie. 20min. Puis on reproduit le bug, et on constate qu'il n'y est plus. Youhou. Victoire. On a bien mérité un café.


>-- Ça serait plus pratique si vous pouviez compiler sur vos environnements non ?


>-- Oui, mais la chaîne de compil est trop lourde. Ça prendrait trop de temps à mettre en place.


>-- Et modulariser le système pour ne pas avoir à tout recompiler à chaque fois ?


>-- Oui, on a fait une étude, il y en a pour 15 jours de boulot, on n'a jamais trouvé le temps pour s'y attaquer.


>-- en 18 mois[^4], vous n'avez pas pu consacrer 15 jours à ça ?


>-- nop


>-- par contre, vous pouvez perdre 3h pour corriger un bug qui a réellement nécessité 15 min de travail ?


>-- Je... On... On l'avait jamais vu comme ça. Mince.[^5]


Ils s'y sont collé à 2 et en une semaine, ils ont complètement remis à plat leur système de build. Ils ont calculé que cela leur évitait de perdre 1h par jour chacun. Une équipe de 7 : 1 journée de gagnée tous les jours.


__Et si on prenait plus souvent le temps d'éviter d'en perdre ?__


[^1]: on ne se moque pas, le print(toto) est une arme de débuggage massive, plus efficace que la plupart des debuggers quand elle est bien utilisée (et si en plus on a des tests, c'est juste une tuerie)
[^2]: grosse appli en C/C++/C# (sisi, les trois d'un coup), mal modularisée et donc à recompiler intégralement à chaque fois
[^3]: une allocation mémoire foireuse
[^4]: dont 6 de retard
[^5]: un exemple de [la vision du lion](/?post/2014/02/22/La-vision-du-lion) ?
