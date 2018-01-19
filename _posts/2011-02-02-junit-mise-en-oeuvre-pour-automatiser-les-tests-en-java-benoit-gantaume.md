---
layout: post
title: "JUnit Mise en oeuvre pour automatiser les tests en Java -- Benoit Gantaume"
date: 2011-02-02 22:31:00 +0100
comments: false
categories: 
- "chronique"
- "java"
- "junit"
- "tdd"
- "test"
---
![gantaume-junit.jpeg](https://blog-img.crafting-labs.fr/couverture/.gantaume_-_junit_s.jpg){: .left-image}
__Présentation de l'éditeur :__

> Ce livre sur l’automatisation des tests avec JUnit s'adresse à toutes les personnes impliquées dans des projets de développement logiciel et désireuses de découvrir le potentiel de JUnit. Quelle que soit la façon dont l'équipe de développement travaille, que vous soyez débutant ou expert, manager, développeur, architecte ou chef de projet, ce livre vous permettra d'appréhender les tests automatiques, de les insérer dans une logique de fabrication de logiciels et de les mettre en œuvre efficacement.

> Le premier chapitre est destiné à introduire rapidement JUnit de manière concrète. Cette partie intéressera surtout les développeurs utilisant JUnit pour la première fois. La seconde partie s'adressera autant aux personnes ayant des responsabilités techniques que managériales et permettra de mieux comprendre les enjeux de l'automatisation des tests ainsi que leur imbrication dans le processus de la création de logiciels. Enfin la troisième partie sera dédiée aux techniques avancées de test permettant d'utiliser les tests automatiques comme un élément de compétitivité économique.
>
> Pour tirer le meilleur profit de ce livre, il est intéressant que le lecteur dispose des connaissances de base de la programmation Objet avec le langage Java, la connaissance des Design Patterns étant un plus.
>
> À la fin de cet ouvrage, vous serez capable de concevoir et mettre en œuvre une stratégie de tests automatiques et de tester votre code à différents niveaux.

> Les éléments disponibles en téléchargement sur le site [www.editions-eni.com](http://www.editions-eni.com), contiennent les codes sources de la calculatrice et du serveur de calcul, les deux projets exemples menés tout au long du livre.



Chic, chic, chic, un livre sur les tests, avec JUnit et java en support, le tout écrit en français par un français, il n'en fallait pas plus pour que je saute dessus :). Vite commandé, vite reçu, et vite lu[^1].

Pour commencer cette chronique, petite précision : contrairement à ce que le titre peut laisser croire, JUnit n'est pas le sujet central, si vous cherchez une documentation exhaustive passez votre chemin. Le vrai sujet, c'est les tests, et c'est ça qui est bien cool. Évidemment JUnit est tout de même à l'honneur car tous les points théorique et pratique sont illustré par du code Java et des tests JUnit 3 et 4. 

C'est d'ailleurs le second bon point bien agréable, il y a beaucoup de code. Des exemples simples, mais concrets, efficaces et bien choisis. C'est clair, c'est un livre écrit par un développeur pour des développeurs. Cependant, le texte est très bien écrit et compréhensible par tous.

Bon concrètement, de quoi parle ce livre ? De tests, et de leur automatisation en Java avec JUnit[^2].
Il s'agit essentiellement de tests unitaires, même si les tests fonctionnels de plus haut niveau font quelques apparitions. Et point de vue tests unitaires, on fait bien le tour de la question.

Deux premières parties sont consacrées au pourquoi et au quoi des tests unitaire, ainsi qu'un petit guide de démarrage pour utiliser JUnit avec votre système préféré (eclipse, maven ou intellij'DEA). C'est clair et assez complet tout en restant pragmatique. Et même si on n'est pas encore vraiment les mains dans la technique on a déjà du code.

Arrive ensuite la technique, le comment. Comment tester, les techniques, les outils. Là encore, c'est bien fait avec un chapitre assez complet sur les bouchons et le modelage des tests. On fait également un passage par les outils de mesure de couverture, Emma, Cobertura et Clover, les avantages et les inconvénients de ces outils.
Tout un chapitre est également consacré aux Test Driven Development ou pilotage par les tests.

Enfin, un petit tour par les outils périphériques comme --hudson-- Jenkins, pour l'intégration continue, DBUnit pour les tests de DAO[^3] ou JUnitPerf que je ne connaissais pas et qui peut s'avérer sympathique.

Et voilà, on est 280 pages plus tard et on a fait un tour d'environ assez agréable sur le sujet des tests en java avec JUnit. C'est complet et pragmatique à la fois. Il est régulièrement rappelé que c'est au développeur[^4] de trouver le juste niveau de tests. C'est un discours sensé et réaliste sur le point souvent très bas dont on part quand on arrive sur un projet.

Je l'ai déjà dit, il y a beaucoup de code de bonne facture[^5] dans l'ouvrage. C'est un de ses points forts, c'est aussi le plus gros reproche que lui fait. Non sur sa qualité ou son intérêt mais sur la forme. Comme trop souvent, l'indentation est vraiment mal foutue ce qui rend difficile la lecture du code si la ligne dépasse la largeur de page. Bon, c'est pas très grave, mais c'est dommage.

En conclusion, Benoit Gantaume signe là un très bon livre qui couvre un spectre suffisamment large pour intéresser aussi bien les débutants que les confirmés. Les premiers trouveront de quoi s'initier aux tests et tout ce qu'il faut pour s'y mettre, pour les autres, il fourmille de petites astuces bien pratiques. Pour ma part, cela me conforte dans mes pratiques même si je dois parfois[^6] me battre pour les pratiquer et les communiquer aux autres.






Achetez le sur amazon : [JUnit, Mise en oeuvre pour automatiser les tests en Java ](http://www.amazon.fr/gp/product/2746060612?ie=UTF8&tag=monbloamoique-21&linkCode=as2&camp=1642&creative=19458&creativeASIN=2746060612) de Benoit Gantaume



[^1]: mouais, bon, priorité oblige, il s'est écoulé un peu de temps entre la réception et la lecture
[^2]: comme quoi le titre n'est pas si mal choisi :)
[^3]: mais perso, je préfère ma solution à base de hsqldb :)
[^4]:  et l'équipe dans laquelle il se trouve
[^5]: mais parce qu'il faut bien que je chipote, je suis pas fan des new Long(6) :)
[^6]: souvent :(
