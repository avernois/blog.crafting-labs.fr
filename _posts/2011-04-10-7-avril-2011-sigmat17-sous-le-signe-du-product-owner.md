---
layout: post
title: "7 avril 2011 -- SigmaT17 sous le signe du Product Owner"
date: 2011-04-10 21:52:00 +0100
comments: false
categories: 
- "agilité"
- "chronique"
- "conférence"
- "product owner"
- "scrum"
- "sigmat"
---
![sigmat.PNG](https://blog-img.crafting-labs.fr/logo/.sigmat_s.jpg){: .left-image}
 Jeudi dernier, c'est SigmaT17, le SigmaT nouvelle formule. À la Cantine, une trentaine de personnes s'était réunie pour écouter Olivier Béarn et Frédéric Duffau nous parler du rôle de Product Owner. Et continuer les débats autour de l'apéro :)


![DSC 6061 r.JPG](https://blog-img.crafting-labs.fr/2011.04.07_-_SigmaT17/.DSC_6061_r_s.jpg){: .right-image}
C'est Olivier Béarn qui ouvre la session avec une présentation du rôle du Product Owner. Je ne vais pas revenir en détail sur cette présentation au contenu théorique et pédagogique, d'autres l'on déjà fait bien mieux. Si vous souhaitez découvrir ce rôle et ce qu'il implique, faites donc un tour sur le blog de [Claude Aubry](http://www.aubryconseil.com/?q=product+owner) ou son [livre sur Scrum](http://rcm-fr.amazon.fr/e/cm?lt1=_blank&bc1=000000&IS2=1&bg1=FFFFFF&fc1=000000&lc1=0000FF&t=monbloamoique-21&o=8&p=8&l=as4&m=amazon&f=ifr&ref=ss_til&asins=2100540181), les traductions de [Fabrice Aimetti](http://www.fabrice-aimetti.fr/index.php?q=product+owner+traduction) ou encore [Google](http://www.google.fr/#q=product+owner).

Ensuite, Frédéric Duffau prend la parole pour un retour d'expérience sur un projet qu'il a accompagné. Il s'agit d'un projet au forfait[^1] réalisé par sa SSII pour le CNES.
Dans ce projet, le Product Owner était un membre du CNES mais l'importance de son rôle avait été sous estimée par lui et/ou son organisation, ce qu'il fait qu'il n'était pas en mesure de s'occuper correctement de son backlog.
![DSC 6066 r.JPG](https://blog-img.crafting-labs.fr/2011.04.07_-_SigmaT17/.DSC_6066_r_s.jpg){: .left-image}
Le Scrum Master de l'équipe s'est alors transformé en proxy du product owner. Son rôle premier de Scrum Master a alors été transféré à une autre personne[^2].
L'objectif de ce proxy était de remplacer le Product Owner dans les contacts au quotidien avec l'équipe de développement et de l'aider à écrire le product backlog le temps qu'il se forme aux exigences du rôle de PO et qu'il se libère suffisamment de temps pour le remplir correctement.
Et c'est là que le retour de Frédéric est très intéressant, c'est qu'ils ont réussi à impliquer le client et convaincre son organisation qu'il devait être sur le projet à plein temps. Aujourd'hui, le proxy est redevenu le Scrum Master de l'équipe et le Product Owner joue son rôle naturellement. La preuve qu'il est possible de faire bouger, au moins localement, une grosse organisation pas spécialement agile.

Un petit débat s'est ensuite organisé sur ce mode de fonctionnement qui semble assez courant dans l'implémentation de l'agilité dans des projets réalisés par des sous-traitants.
Merci à Claude d'avoir rappelé à l'assemblée qu'avec l'apparition du product owner proxy, c'est le triste spectre du découplage MOA/MOE que l'on voit essayer de revenir par la petite porte. Je partage l'opinion de Claude pour dire que ce modèle à fait beaucoup de dégâts sur le développement logiciel et qu'il faut l'éviter à tout prix. Il faut donc être très prudent si l'on met en place ce type de proxy, cela doit répondre à un besoin ponctuel et tout doit être mis en oeuvre pour sortir de ce mode au plus vite.

Maintenant, je dois aussi être honnête et admettre que malheureusement, dans le projet où je suis actuellement, nous avons aussi implémenté cette solution de proxy... 
__Pourquoi ?__ parce que nous aussi nous sommes dans une très grande société française pas spécialement agile[^3], qui fonctionne encore largement sous le principe MOA/MOE... D'ailleurs, officiellement, notre Product Owner est la MOA du projet. En pratique, nous avons cassé ce modèle et notre PO est au contact quasi quotidien de l'équipe, avance avec elle et est fortement impliqué. Le vrai problème c'est qu'il n'est pas à plein temps sur le projet et qu'en plus du notre, il doit gérer d'autres projets[^4], en mode old school qui plus est...
Et comme si cette non disponibilité permanente ne suffisait pas, nous avons aussi le problème de la distance, puisque nous sommes à Toulouse[^5] et que lui est à Lyon[^6].

__Alors, en pratique, comment ça marche chez nous ?__
Notre Product Owner est donc à Lyon et bien sûr, le proxy est avec l'équipe. Notre application a un périmètre fonctionnel assez vaste et recouvre plusieurs métiers différents (mais complémentaire), donc notre PO est assisté par des représentants des différents métiers concernés (2 à 3 personnes, de Bordeaux, Toulouse et Rennes). Avec leur aide, il est en mesure de définir les fonctionnalités du produit et par extension, le backlog.
C'est là qu'intervient notre proxy. Il participe à toutes les réunions[^7] de cette équipe et il aide le PO à écrire son backlog. En gros, le PO définit les user story. Le proxy s'occupe de poser les différentes règles métiers, ce que le PO n'aurait pas le temps de faire vu ses autres activités.
Ces user stories sont présentées régulièrement[^8] par le duo PO/proxy à l'équipe pour les estimer ou les retravailler si nécessaire.
Le PO s'implique au plus qu'il le peut et il y a une très grande communication entre lui et le proxy, et sont très régulièrement au téléphone ensemble[^9].

Le proxy est à proximité de l'équipe, c'est donc lui qui assiste au meeting quotidien avec l'équipe. C'est aussi lui qui répond aux questions/suggestions/demandes de précisions/... de l'équipe. Si il est dans l'incapacité de répondre directement, une réunion téléphonique a lieu au plus tôt avec le PO (en général, dans la demi journée). Mais même si les réponses arrivent vite, c'est une latence toujours trop importante par rapport à une communication directe.

Un système de déploiement automatique toutes les nuits permet au PO de suivre au quotidien l'avancement et de faire du feedback rapidement.

Un point important à noter, c'est que l'équipe a parfaitement[^10] conscience ce cette façon de fonctionner. Nous savons qui est le PO et quel est le rôle que tient le proxy.

Pour nous, cette méthode fonctionne à peu près, parce que le projet est réellement le bébé du PO qui s'investit au maximum de ses possibilités, mais elle a tout de même montré ses limites à plusieurs reprises, et provoque une duplication du travail[^11]. 

Il est clair que les choses seraient plus faciles et plus agréables si nous pouvions avoir le PO à plein temps. Et si en plus il était sur place, ça serait le bonheur.

Bref, __ce rôle de Product Owner Proxy n'est absolument pas une chose à généraliser__, rien ne remplacera jamais un Product Owner dédié, conscient de son rôle et entièrement impliqué dans le projet avec l'équipe. Les sociétés qui veulent de l'agilité doivent arrêter de croire que ça ne concerne que le fonctionnement des développeurs. Elles doivent se donner les moyens de bien faire, dans leur propre intérêt.


Pour finir ce billet, je reprends le format rétrospective que j'utilise depuis quelques temps.

##Ce qui s'est bien passé

* une trentaine de personnes présentes
* j'ai enfin pris le temps de savourer l'apéro
* le chef de projet de mon projet et un des membres de l'équipe sont venus
* quelques irréductibles[^12] ont fini la soirée à discuter sur le développement logiciel et l'agilité devant une bière au [Breughel](http://www.breughel.fr/).

##Ce qui aurait pu être mieux

* beaucoup d'inscrits ne sont pas venus sans prévenir (plus de 25%, ça fait beaucoup)
* les présentations manquaient un peu de punch
* peu de nouvelles têtes

##Leçons (ré-)apprises

* le Product Owner est un rôle essentiel.
* le PO peut être assisté de spécialistes, mais il reste le seul décideur.
* le proxy PO est une chose à laquelle il faut faire extrêmement attention, ne pas le faire c'est encore mieux.


##Puzzles

* j'ai une idée de présentation Artistes / Développeurs : tous des créatifs
* j'espère que l'intervention de Claude aura fait mouche
* mais où ai je mis le chargeur de mon P5000 ?

##Remerciements

* Olivier et Frédéric pour leurs présentations
* Claude pour sa sagesse
* les membres de la SigmaT qui ont permis cet événement
* La Cantine pour l'accueil et l'apéro


##Feedback

* rien pour l'instant chez [Claude](http://www.aubryconseil.com)


##À venir

* des personnes avisées m'ont dit qu'il se raconte qu'un apéroweb serait en préparation pour la fin du mois
* le prochain rendez vous du Toulouse JUG se tiendra le 21 avril 2011


[^1]: il part avec un handicap
[^2]: par Frédéric, qui à l'origine devait faire de l'accompagnement et du coaching
[^3]: je tairais le discours officiel qu'elle tient sur l'intérêt de l'agilité, un public non averti pourrait être choqué...
[^4]: au moins 2 à ma connaissance
[^5]: Blagnac en fait
[^6]: si je tenais celui qui a eu cette brillante idée...
[^7]: qui se font par téléphone vu les distances
[^8]: une fois par semaine
[^9]: à vue de nez, maintenant, c'est un minimum d'une heure par jour
[^10]: je crois
[^11]: le proxy est obligé de mettre beaucoup de choses à l'écrit pour les soumettre au PO qui les valide ensuite,
[^12]: [@oaz](http://twitter.com/#!/oaz), [@DirtyF](http://twitter.com/#!/DirtyF), [@yann_madeleine](http://twitter.com/#!/yann_madeleine) et [moi](http://twitter.com/#!/avernois)
