---
layout: post
title: "La dictature des chiffres"
date: 2013-05-02 16:09:00 +0100
comments: false
categories: 
- "agilité"
- "chiffre"
- "indicateur"
- "sens"
---
[![Cluj, panneau](https://blog-img.crafting-labs.fr/illustration/.2007.09-ICCP-313_m.jpg){: .left-image}
](https://blog-img.crafting-labs.fr/illustration/2007.09-ICCP-313.jpg)

Entendu sur des projets :

> -- dev 1 : rahh, le taux de couverture est en dessous du seuil.

> -- dev 2 : ok, je vais voir où je peux rajouter des tests pour le faire remonter.

> -- dev 1 : t'embarques pas trop dans ce bout de code, il est tordu. Tiens, t'as qu'à couvrir les getter/setter, ça devrait suffire.

> -- dev 2 : bien vu !

> -- dev 1 : checkstyle râle parce que les attributs ne sont pas déclaré ''transient''. C'est quoi ''transient''[^1] ?

> -- dev 2 : je sais pas, fait ce qu'il te dit ça fera baisser le nombre d'erreur.


Je n'en cite que deux, et uniquement lié au développement logiciel mais je pourrai probablement tenir une nuit à vous en raconter des comme ça[^2]. Toutes rigoureusement véridiques.

Le travers ici n'est pas d'écrire des tests ou de suivre les conseils de checkstyle, mais bien de le faire dans le seul et unique but d'atteindre un quota, sans vraiment chercher à comprendre ce qu'on fait : l'objectif, est devenu le chiffre et non ce qu'il représente. Et donc, tous les moyens sont bons pour atteindre le chiffre au détriment de ce qu'il devait représenter au départ.
La tentation première est de rajouter encore plus d'indicateurs, plus de chiffres, contraindre encore plus la mesure pour qu'elle ne puisse être contournée. Plus de règles, plus de lois. Ce n'est pas une solution viable. Car pire qu'un objectif, le chiffre devient répression, et là, c'en est fini de son sens.

Une information utile meurt à chaque fois qu'un contrat spécifie le niveau de couverture de tests ou qu'un testeur est objectivé sur le nombre de bugs qu'il ouvre[^3]. Parce que l'objectif, ce n'est pas que le taux de couverture atteigne 95%, ou que le nombre d'erreurs remontées par checkstyle soit nul.

L'objectif, le vrai, c'est que le code soit de qualité, et qu'il y ait ce qu'il faut de tests pour que je puisse mettre les mains dedans, le compléter, l'améliorer sans risque de faire exploser l'application sans m'en rendre compte.
Un taux de couverture élevé, des valeurs sympas pour les indicateurs de qualité seront une conséquence de ça[^4].

Un code de qualité impliquera de bons indicateurs [^5]. La réciproque est fausse. Toujours.

# Donc on jette tous les chiffres et le sonar avec l'eau du bain ?
Bien sûr que non[^6] ! Mais on les utilise pour ce qu'ils sont : des indicateurs, qui donnent globalement une direction et pas un gps qui vous dit exactement où vous êtes.

Ce qui est intéressant n'est pas le chiffre, mais la réalité qu'il est censé refléter. Et c'est cette réalité qui doit être le centre premier de l'attention.

Il ne faut pas jeter les chiffres pour autant. Je me sers presque tout le temps de tout un tas de métriques. Mais bien souvent je n'en utilise vraiment qu'une à la fois.
![2012.03.16 - Agile Open Sud - Banyuls.0216.jpg](https://blog-img.crafting-labs.fr/illustration/.2012.03.16_-_Agile_Open_Sud_-_Banyuls.0216_m.jpg){: .right-image}

## Concrètement
Imaginons qu'une équipe décide d'augmenter sa pratique des tests unitaires. Le taux de couverture ou le nombre de tests sont des indicateurs pertinents. On va donc les afficher bien en vue de tous en les mettant à jour régulièrement[^7], éventuellement avec un petit graphique d'historique pour voir la progression.

L'équipe se concentre alors sur les tests unitaires. Cela se traduira par une augmentation de leur nombre et de la couverture de code. 
Si ce n'est pas le cas, c'est soit notre mise en oeuvre des tests qui n'est pas correcte, soit ce que l'on mesure, ou notre façon de mesurer, qui ne convient pas.
Dans un cas comme dans l'autre, c'est un signe pour l'équipe de se poser des questions sur la pratique et sa mesure.

Lorsque l'on arrive au niveau de pratique que l'on souhaitait, on note la valeur de l'indicateur qui servira de référence.
On continue à évaluer l'indicateur[^8] et on passe à une autre pratique à améliorer. Et donc un autre indicateur en premier plan.

Ainsi, petit à petit, l'équipe se construit les indicateurs qui lui sont utiles pour suivre la réalité de ses pratiques. 
Si par force de routine, de fatigue, ou de pression externe, l'équipe venait à ralentir une de ses pratiques, l'indicateur concerné le montrerait permettant à l'équipe de réagir au plus vite.

#Conclusion
Les indicateurs doivent être des conséquences de vos actions et des déclencheurs de remise en question de vos pratiques. 
Un indicateur ne peut pas être vu comme un objectif en soi.

-- un grand merci à [Ludo](https://twitter.com/ludopradel) et [Nicolas](https://twitter.com/ndeverge) pour les relectures attentives


[^1]: ''transient'', en java signifie que l'attribut ne sera pas présent lors de la sérialisation. Par conséquent, à la désérialisation, il prendra la valeur ''null''.
[^2]: bon peut être pas la nuit, mais au moins jusqu'à la fermeture du bar
[^3]: oui, ça aussi je l'ai vu en vrai
[^4]: et si ce n'est pas le cas, c'est probablement que l'indicateur n'est pas bon
[^5]: à condition que ceux-ci soient pertinents :)
[^6]: quoique pour sonar ... :)
[^7]: une fois par jour ou plus
[^8]: automatiquement cela va de soi
