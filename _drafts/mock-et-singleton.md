---
layout: post
title: "Mock et singleton"
categories: 
---
Quand j'interviens dans une équipe de dev pour les aider à progresser dans leurs pratiques, il y a toujours un moment où arrive cette discussion : 


> - tu nous conseilles quoi comme outil pour faire des mocks ?

> - ça dépend. Pourquoi vous avez besoin de faire des mocks ?

> - ben, on est en train d'écrire des tests unitaires pour notre base de code, et on a des dépendances qu'il faudrait mocker.

> - quelle genre de dépendance ?

> - un singleton

Premier détail marrant, c'est qu'il faut toujours du temps avant qu'ils n'avouent que c'est un singleton qui leur pose problème. Jamais eu une équipe à qui me l'annonce sans que j'ai à creuser :)[^1].

Alors je parle de singleton, mais ça pourrait aussi être un appel de méthode statique, ou l'utilisation d'une variable global. Dans la suite, je parlerai de singleton, mais ça marche pour les autres cas.

# C'est quoi le problème des singletons ?
Alors, il y a pleins de problèmes avec ce pattern, qui mériteraient un article rien que pour eux.
Je vais me contenter de parler du problème de testabilité.

Et voilà, tester une méthode qui fait appel a un singleton est un enfer. Parce que justement, sauf à faire des trucs vicieux avec le bytecode[^2], on ne peut pas intercepter l'appel fait à un singleton. Parce que notre singleton, il est là, tout le temps et partout et on peut l'utiliser directement sans avoir besoin que quelqu'un[^3] ne vous donne une référence sur lui.

Et donc, il est quasiment impossible de pouvoir configurer les comportements qu'on attend de lui en fonction du cas que l'on teste.

Autre problème, puisque sa durée de vie est celle de l'exécution, tous les tests utiliseront le même singleton, et il est à prévoir des effets de bords indésirable très rapidement.

# Premier cas : c'est pas mon problème
Exemple bidon : Imaginons une application web, et une méthode doThings() appartenant à un service métier.
Cette méthode retournerait des trucs en fonction de l'utilisateur connecté et d'un paramètre.
Et pour récupérer l'utilisateur connecté, PAF, on fait appelle au singleton WebSession (qui contient les informations de la session en cours).


///yash java
ReturnValue doThing(UsefullParameter parameter) {
    ...
    User user = WebSessionSingleton.getInstance().getLoggedUser();
    doSomethingWith(user);
    ...
}
///

Et là, on voit tout de suite qu'en plus du singleton pénible, en vrai, on a un autre malaise STUPID : via WebSession, mon service métier est fortement couplé avec mon système qui gère la présentation des données (la couche web). Et ça, c'est très moyen.
On peut alors se demander : est-ce réellement la responsabilité de mon service d'aller fouiller la session pour récupérer l'utilisateur connecté ?.

Ici, la réponse est non : mon service métier ne devrait même pas avoir conscience qu'il y a un truc web au-dessus de lui. Ça n'est pas son problème. Il doit se concentrer sur son métier[^4].

Donc la solution au problème devient simple. Plutôt que de faire appel au singleton dans le service, on passe l'utilisateur en paramètre.

///yash java
ReturnValue doThing(UsefullParameter parameter, User user) {
    ...
    dSomethingWith(user);
    ...
}
///

Le singleton a été repoussé au loin, la méthode devient testable.
Et voilà. Problème réglé.

Et j'entends déjà au fond de la salle : Oui, je ne peux pas changer l'appel comme ça, la méthode est appelé un peu partout et utilisé par d'autres équipes.

Qu'à cela ne tienne, pour le reste du monde qui ne veut pas être propre[^5], on peut facilement maintenir les apparences pour eux en rajoutant une méthode ayant le prototype d'origine qui fait appel
///yash java
ReturnValue doThing(UsefullParameter parameter) {
   this.monService(parameteur, WebSessionSingleton.getInstance().getLoggedUser(););
}
///

Et hop, vous avez fait votre refactoring, et le monde n'y a rien vu (pour l'instant). Vous pouvez tranquillement tester la nouvelle méthode doThing avec 2 paramètres et propager la bonne nouvelle au reste du monde[^6].

# Deuxième cas : si, si, c'est mon problème



# Épilogue
En vrai, je n'ai rien contre les singletons, c'est pratique. J'en utilise même souvent. Par contre, je veille à ce que mon code ne sache pas que cela en est un. Il n'y a que la partie chargé de la plomberie (ou mon container d'application) qui sera au courant.


[^1]: peut être parce qu'une conversation au tour de l'accronyme STUPID (Singleton, Tight coupling, Untestable, Premature Optimisation, Indescriptive Naming, Duplication) arrive souvent très tôt dans mes interventions
[^2]: ce que font très bien certains outils de mock, mais mon point ici est justement de vous montrer comment ne pas en avoir besoin :)
[^3]: autre que lui même
[^4]: SRP, Single Responsability Principle, ça vous parle ? :)
[^5]: oui, j'exagère
[^6]: et faire en sorte qu'ils arrêtent de se servir de l'ancienne
