---
layout: post
title: "Le test unitaire et les méthodes privées"
date: 2013-10-21 17:08:00 +0100
comments: false
categories: 
- "code"
- "privée"
- "test"
---
![Private property. So what ? d'Alexandre Dulaunoy](https://blog-img.crafting-labs.fr/illustration/flickr/.flickr_adulau_propriete_privee_s.jpg){: .left-image}
Une question qui revient souvent lorsque j'anime un coding dojo ou durant ma [session sur les tests unitaires](http://avernois.github.io/prez-before_after_tdd) :

> Faut-il tester les méthodes privées ?

Réponse courte et définitive[^1]:

> Non.


# l'aspect pratique : c'est un peu crade

Et oui, déjà, l'aspect pratique de la chose arrête. Par définition, une méthode privée ne peut pas être appelé depuis l'extérieur de la classe dans laquelle elle est définie.
Pour pouvoir les tester je vois 3 solutions :

## mettre le code de test dans la classe de prod ?
Bon, je pense que vous comprendrez de vous même que ce n'est pas une bonne idée.

## passer la méthode en ''protected'' ?
C'est la solution que je rencontre le plus souvent. C'est probablement la pire, à mon sens.
Passer une méthode en ''protected'', c'est la rendre visible en dehors de la classe[^2].
Passer une méthode en ''protected'', c'est donc donner à notre classe des fonctionnalités qui ne font pas partie de son contrat de base.

Vous modifiez donc le contrat de votre classe dans le but de le tester. L'effort est louable (plus de test) mais le résultat l'est moins (vous contraignez votre classe à faire plus que ce qu'elle a besoin.).
Au final, votre détail d'implémentation (la méthode privée) devient une contrainte (elle est utilisable par d'autre). Bof...

## abuser de réflexion/introspection pour changer la visibilité de la méthode
Alors là, la méthode elle est privée, et hop, maintenant, hop, magie, elle est ''protected'' le temps que je fasse mon test et hop elle redevient privée. 
Changer à la volée la visibilité d'une méthode est rarement une bonne chose puisque vous allez alors l'utiliser dans un contexte pour lequel elle n'a pas été prévue.
Vous forcez sa nature. C'est cruel et violent...

J'ai aussi vu des gens passer la méthode en protected, écrire les tests, vérifier qu'ils passent bien, commenter les tests, repasser la méthode en privé. Mais ça, mon esprit n'arrive pas à concevoir que cela puisse exister et persiste à essayer de me convaincre que j'ai rêvé cet exemple[^3].

Donc tester des méthodes privées, c'est loin d'être simple, et présenté comme je le fais ça ne semble vraiment pas très sains ni une bonne idée.
Malheureusement, comme je suis le premier à dire que ''Ce n'est pas parce que c'est complexe[^4] qu'il ne faut pas le faire'', je vais poursuivre sur des considérations un peu plus conceptuelles.

# back to concept
## et un test unitaire c'est quoi ?
Alors, il y a a peu près autant de définition des tests unitaires que de gens qui ont écrit des définitions des tests unitaires[^5].
Pour moi[^6] les tests unitaires servent à définir et vérifier le comportement de notre code tel qu'il sera perçu par ceux qui l'utiliseront.

Le test unitaire s'intéresse au ''quoi'', qu'est-ce que fait notre méthode/classe/bout de code et pas au ''comment'' il le fait.

## c'est quoi une méthode privée ?
Une méthode privée, c'est une méthode qui n'est accessible que par la classe dans laquelle elle est définie[^7].
Cela veut dire que, seule, cette méthode n'offre rien au monde extérieur. Seule, une méthode privée n'a pas de raison d'exister.

Si elle existe, c'est qu'elle est utilisée par une méthode publique. En fait, si elle existe, c'est uniquement du au choix d'un développeur à un moment, principalement motivé par deux raisons :
* supprimer de la duplication en factorisant un bout de code utilisé dans plusieurs méthodes de la même classe
* améliorer la lisibilité/compréhension en éclatant en plusieurs morceaux cohérents une méthode un peu grosse.

Donc, l'apparition d'une méthode privée est motivée par un choix d'implémentation et pas un comportement extérieur. C'est une petite astuce technique qui peut[^8] rendre du code plus clair et plus maintenable.
Si pour une raison quelconque je décide de ne plus utiliser de méthodes privées ou de les ''inliner'', cela n'aura absolument aucune conséquence sur le comportement extérieur de mon code.

En gros, la méthode privée est liée au ''comment'' et pas au ''quoi''. Donc, elle n'est, à priori, pas concernée par les tests unitaires.

## Et pourquoi on ne testerait pas le comment ?
Ben parce que tester le ''comment'' c'est tester des détails d'implémentation.
Et avoir des tests liés aux détails d'implémentation, c'est compliquer inutilement toute tentative de modification ultérieure.
Si un jour[^9], on veut modifier comment un bout de code répond à un problème, on se retrouve à devoir modifier une grosse partie des tests liées aux détails. 

On se retrouve vite avec des tests rouges parce qu'ils n'ont plus de raison d'exister et des tests rouges qui devraient revenir verts. Et faire le tri entre les deux, devient une complication sans nom à démêler le quoi du comment.

Alors que si mes tests s'acharnent à ne vouloir tester que le ''quoi'', je peux bien modifier tout de que je veux à l'intérieur, si mes tests sont tous verts à la fin, j'ai la certitude que mon nouveau code fait au moins la même choses que ce qu'il faisait avant.
Je n'ai pas à me poser la question ''ok, ce test là est rouge, c'est normal ou pas ?''. Non, si je m’intéresse au ''quoi'', un test rouge n'est jamais normal[^10].
Je n'ai pas non plus à me poser la question '' faut que je modifie le code ou le test pour que ça repasse au vert ?''. Non, si je m'intéresse au ''quoi'', c'est forcement mon code qui ne fait pas le travail.

## Alors je reste avec du code qui n'est pas testé ?
Et c'est là que la magie opère. Puisque vos méthodes privées ne sont qu'un détail d'implémentation dont l'existence et le comportement n'est justifié que par leur utilisation dans des méthodes publiques, alors ces méthodes privées sont automatiquement testées au travers des tests des méthodes publiques.

Autrement dit, une fois vos méthodes publiques testées, vos méthodes privées devraient être intégralement couvertes. Si ce n'est pas le cas, c'est soit que vous avez oublié des tests, soit que votre méthode privée fait des choses qui ne sont d'aucune utilité pour répondre aux besoins de vos méthodes publiques. Dans ce cas, il faut probablement les nettoyer.

##Oui mais mes méthodes privées sont grosses et compliquées, des tests seraient bien pratiques
Des fois, on voit des méthodes privées qui font pleins de trucs ou des choses si compliquées, qu'avoir des tests seraient quand même bien pratique.
C'est vrai. On en voit.

Mais la plupart du temps[^11], c'est signe qu'il est grand temps d'extraire cette logique dans une nouvelle classe dont les méthodes publiques pourront être correctement testées.


# Conclusion
Tester des méthodes privées, c'est généralement crade et normalement inutile et redondant.




-- Illustration : [Private property. So what ?](http://www.flickr.com/photos/adulau/8460794157/) d'Alexandre Dulaunoy  [CC BY-SA 2.0](http://creativecommons.org/licenses/by-sa/2.0/deed.en)

-- un grand merci à [Ludo](https://twitter.com/ludopradel), [Nicolas](https://twitter.com/ndeverge) et [Claude](https://twitter.com/claudeaubry) pour les lectures attentives.

-- edit :
* 21/10/2013 : suite aux très pertinentes remarques de [Bernard](https://twitter.com/notarianni/status/392321221347389440) et [Laurent](https://twitter.com/Morendil/status/392383611485573120) rajout d'un paragraphe sur les grosses méthodes privées compliquées


[^1]: pour l'instant
[^2]: même si ceux qui peuvent s'en servir restent restreints au package ou à la hiérarchie descendante selon les langages
[^3]: malheureusement, ce n'était pas un rêve.
[^4]: notez que j'utilise complexe et pas compliqué
[^5]: voir un peu plus, car certaines personnes changent d'avis au court du temps. C'est mon cas :)
[^6]: et un bon nombre d'autres
[^7]: tiens, je l'ai pas déjà dit ça ? :)
[^8]: quand c'est bien fait
[^9]: et il arrive souvent
[^10]: sauf si je décide de changer le comportement de mon code évidement, mais ce n'est plus le même sujet :)
[^11]: parce que j'aime pas utiliser ''toujours''
