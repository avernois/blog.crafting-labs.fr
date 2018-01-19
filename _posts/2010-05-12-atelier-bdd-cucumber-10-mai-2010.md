---
layout: post
title: "Atelier BDD Cucumber -- 10 mai 2010"
date: 2010-05-12 00:47:00 +0100
comments: false
categories: 
- "agilité"
- "bdd"
- "cucumber"
- "gherkin"
- "sigmat"
- "test"
---
![sigmat.PNG](https://blog-img.crafting-labs.fr/logo/.sigmat_s.jpg){: .left-image}
Hier, l'association SigmaT organisait un atelier BDD avec des vrais morceaux de live code dedans. 
C'est notre bon camarade [Guillaume Saint Etienne](http://www.dotnetguru2.org/gse/index.php) qui s'est attaqué à cet exercice périlleux et une petite quinzaine de personnes étaient là pour assister à l'événement.


Donc, ce soir, c'est ??BDD|Behaviour Driven Development??. En français dans le texte, ça donne Développement Conduit par les Comportements.
C'est un atelier qui tombe à pic pour moi, car avec l'équipe que je viens de rejoindre, nous démarrons le développement d'un gros projet web, et la question d'un framework pour automatiser les tests fonctionnels est forcement d'actualité :) Pour l'instant, nous hésitons entre fitnesse et cucumber.

Revenons au sujet, les comportements, c'est la description du comportement[^1] d'une application lorsqu'elle est soumise à des évènements alors qu'elle est dans un certain état.
En gros, ça s'exprime par quelque chose de la forme :

__Étant donné__ <un contexte>

__Quand__ <un événement>

__Alors__ <un comportement>


Si vous remettez ça dans la langue de shakespeare, ça donne __Given__ ... __When__ ... __Then__ Et voilà, modulo un peu de présentation et vous obtenez les bases de Gherkin[^2] le langage de description de comportement défini pour [Cucumber](http://cukes.info/)[^3], un framework[^4] pour faire du BDD.

Je connais bien ce type comportement, c'est essentiellement le format que j'utilise pour aider un product owner à spécifier les tests fonctionnels associés à une user story. Ça a l'avantage d'obliger à avoir des phrases simples, facile à comprendre par tous et facile à rajouter au fil des discussions avec l'équipe.

Mais ce que nous propose Guillaume, c'est d'utiliser cette représentation comportementale pour décrire des tests techniques, qui seront donc entièrement écrit par les développeurs. Pour cela, il nous a montré comment cela pouvait se passer par l'exemple. Pour l'occasion, il avait préparé une application juste suffisamment évolué pour pouvoir servir d'exemple concret et crédible sans nous faire perdre trop de temps dans des dev longs et peu intéressants. 

Guillaume étant un spécialiste dotnet, il n'a pas utilisé le pionnier Cucumber[^5] mais [Specflow](http://www.specflow.org/) son équivalent dans le langage de Redmond et se basant sur le même langage de description, Gherkin. 
Specflow permet d'intégrer ces tests directement dans le cadre de Nunit, le pendant .Net de Junit.

Il commence alors par décrire un test technique (avec pour sujet un controller d'une architecture MVC) en utilisant le langage Gherkin. Ensuite Specflow rentre en jeu, son rôle est d'interpréter ce texte en appelle à des méthodes.
Évidemment, pour l'instant, nous n'avons encore écrits aucun bout de code, alors le test échoue. Les messages d'erreurs sont explicitent : Specflow ne trouve pas les méthodes qui doivent implémenter le test. Aidé par ces erreurs, nous pouvons implémenter trois méthodes, une pour le Given, une pour le When et une pour le Then.
C'est dans cette dernière qu'il faudra faire réussir ou échouer le test à grand coup d'__assert__[^6].

Maintenant que le test est écrit, on peut le passer. Bien sur, il échoue puisque le code concret de l'application n'est pas écrit. On se retrouve alors dans un schéma bien connu du TDD : le test est là, et échoue, il ne reste qu'à écrire le code qui lui permettra de passer. Une fois le test vert, on décrit un nouveau test, on l'implémente, il échoue et on écrit le code nécessaire pour que ça passe.

Donc, voilà, c'était un atelier intéressant, d'autant que le public était très participatif et avec de l'expérience sur la problématique des tests, qu'ils soient fonctionnels ou unitaires.
La démo de Guillaume a été régulièrement interrompu par des discussions intéressantes et constructives sur la nature même des tests, leur portée et la façon de les exprimer.

Je pense que comme moi, la majorité des participants a été surpris que l'on aborde par cette approche des tests techniques. Personnellement, cela ne m'a pas convaincu, et je crois que je ne suis pas le seul.
Si je suis convaincu de l'intérêt d'exprimer en langage compréhensible par un non développeur[^7] les tests fonctionnels, je ne vois pas l'intérêt de le faire pour des tests purement techniques. Cela rajouterait une couche qui me semble redondante avec le code d'un test unitaire qui se doit d'être lisible et compréhensible pour ceux qui passeront derrière nous. Peut être que cela peut aider des développeurs débutants en test unitaire à formaliser leurs besoins.

Un grand bravo à Guillaume pour la prise de risque de faire du code en live et d'avoir réussi à supporter toutes nos interruptions, commentaires et discussions. Mention spéciale pour son maniement de la loupe :)

Le temps nous a manqué pour aborder un aspect plus fonctionnel, mais des rumeurs courent au sujet d'une suite, et peut-être même, soyons fous, d'un atelier dédié à Fitnesse[^8].

Quand à moi, je pense maintenant que Fitnesse est le meilleur choix pour nos besoins.


[^1]: surprement non
[^2]: en français : cornichon
[^3]: en français : concombre
[^4]: comestible ? :)
[^5]: écrit en ruby et utilisé en ruby ou en java
[^6]: C'est là une des différences avec Fitnesse dans lequel on n'écrit jamais d'assertion, c'est le framework qui se charge de vérifier que le résultat obtenu est celui attendu
[^7]: au hasard, le product owner :)
[^8]: David, ceci est un appel :D
