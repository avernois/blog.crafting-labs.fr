---
layout: post
title: "ArdFeedback : rendez visible vos builds jenkins"
date: 2012-08-13 11:11:00 +0100
comments: false
categories: 
- "arduino"
- "craftsmanship"
- "diy"
- "geekeries"
- "integration"
- "jenkins"
---
[![2012.08.10-Ardfeedback.046.jpg](https://blog-img.crafting-labs.fr/ardfeedback/.2012.08.10_-_Ardfeedback.046_s.jpg){: .left-image}
](https://blog-img.crafting-labs.fr/ardfeedback/2012.08.10_-_Ardfeedback.046.jpg)
J'aime beaucoup [Jenkins](http://www.jenkins-ci.org), je l'installe presque partout où je passe.

Ça faisait longtemps que je voulais bricoler un truc pour rendre physiquement visible le statut des builds.
Bon, [il existe déjà un paquet de plans](https://wiki.jenkins-ci.org/display/JENKINS/Use+Jenkins#UseJenkins-ExtremeFeedback), plus ou moins détailléS pour faire faire s'allumer des des orbs, des feux ou même [des nounours](https://wiki.jenkins-ci.org/pages/viewpage.action?pageId=20250625).

Mais c'est quand même plus drôle de le faire soi même :)


Résultat, un petit script à charger dans un arduino, un schéma de montage et un contrôleur à faire tourner sur la machine relié à l'arduino par usb. 

# Le matos
Pour le prototypage, il vous faudra : 
* un arduino uno
* 8 leds 10mm, 3 vertes[^1], 2 jaunes, 3 rouges
* 8 résistance qui vont bien avec vos leds.[^2]
* un plaque à essai
* plein de fils pour connecter tout ça.

Perso, je me suis fourni chez les ptits gars de [Snootlab](http://www.snootlab.com) qui, en plus d'être compétents et sympathiques, ont le bon goût d'habiter à coté de chez moi :p

# Le montage

C'est simple, mais efficace :)

![montage](https://raw.github.com/avernois/ardFeedback/master/img/ardfeedback_bb.png)

Le schema est réalisé avec [Fritzing](http://fritzing.org). Le source est dispo sur [github](https://github.com/avernois/ardFeedback/tree/master/schema)

# Un peu de code pour piloter tout ça
Oui, parce que bon, l'électronique c'est marrant, mais ça fait pas tout :)

## ArdFeedback

Dispo sur github : [https://github.com/avernois/ardFeedback]

Une fois chargé dans l'arduino, il permettra d'allumer les leds en fonction de commandes reçues sur le port série (via l'USB).

Une commande est un caractère. Actuellement[^3], le système comprend : 
* 'R' : allume les leds rouges et éteint les autres
* 'Y' : allume les leds jaunes et éteint les autres
* 'G' : allume les leds vertes et éteint les autres
* 'B' : allume les leds les unes après les autres

C'est basique, mais ça rempli l'objectif :)

## ArdFeedback-Control

Dispo sur github : [https://github.com/avernois/ardFeedback-control]

Il s'agit un petit code ruby qui se charge de scruter régulièrement votre jenkins[^4] et de demander à l'arduino d'allumer les bonnes leds.

### Utilisation


> ruby lib/ard_feedback.rb

Options:

* --jenkins, -j : jenkins api url (default: http://localhost:8080/api/xml)
* --serial, -s : Serial port use to communicate with arduino (default: /dev/ttyACM0)
* --refresh, -r : Delay between requests to jenkins (in seconds) (default: 30)
*  --help, -h : Show this message

# Et voilà !

Amusez vous, n'hésitez pas à forker et faire des PR pour proposer des améiliorations[^5]

Enjoy !

[![2012.08.10-Ardfeedback.008.jpg](https://blog-img.crafting-labs.fr/ardfeedback/.2012.08.10_-_Ardfeedback.008_m.jpg)
](https://blog-img.crafting-labs.fr/ardfeedback/2012.08.10_-_Ardfeedback.008.jpg)

# TL;DR
* [ArdFeedback on github](https://github.com/avernois/ardFeedback)
* [ArdFeedback-Control on github](https://github.com/avernois/ardFeedback-control)


[^1]: ou des bleues pour être ''jenkins' style'' ;)
[^2]: moi je suis parti sur des 120 ohms
[^3]: ça va surement évoluer, le mieux est de se référer au README qui vient avec les sources
[^4]: via l'api xml
[^5]: c'est fait un peu à l'arrache, alors il y en a forcément :)
