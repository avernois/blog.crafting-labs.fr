---
layout: post
title: "Prezi offline sous linux"
date: 2010-12-07 00:23:00 +0100
comments: false
categories: 
- "flash"
- "offline"
- "presentation"
- "prezi"
- "ubuntu"
---
![prezi logo.jpg](https://blog-img.crafting-labs.fr/logo/.prezi_logo_s.jpg){: .left-image}
[Prezi](http://www.prezi.com), c'est un système pour faire des présentations un peu originals. Prezi, c'est une sympathique alernative aux lineaires powerpoint ou open office. Le système d'édition est en flash et en ligne, et fonctioinne très bien sous linux.
Par contre, officiellement, la version gratuite de présentation offline n'est supporté que pour Windows et MacOS.

Mais en bidouillant un peu, ça fonctionne aussi très bien sous linux (testé sur ubuntu 10.10 32b et 64b). Et comme je suis un grand gentil, je vous explique la bidouille en question.


Bon, déjà, rendons à Caesar ce qui lui appartient : c'est [Stick84](http://stick.gk2.sk/blog/2010/05/prezi-offline-in-linux/) qui est à l'origine de la bidouille[^1].

## préambule
Cette manip a été testé sous ubuntu 10.10 32bit et 64bit (respectivement sur mon laptop et mon netbook).

Je suppose que vous avez le flash 10 officiel d'adobe correctement configuré pour votre navigateur.

## préparer la prezi
Bon, vous avez bien jouer avec [prezi](http://www.prezi.com), et vous avez une super belle présentation trop de la balle qui déchire.
Téléchargez là dans un répertoire qui va bien `~/presentation/` par exemple.
Dans une console :

cd ~/presentation/__
unzip votrepresentation.zip
///
Par la suite, je nommerai `yourprezidir` le répertoire crée lors de la décompression.
Si vous parcourez le contenu de`yourprezidir`, vous découvrirez un `prezi.exe`[^2] et un `prezi.app`[^3].
En fait, la version MacOs, modulo la structure, c'est rien d'autre qu'une application flash. Et ça nous arrange bien.

Dans une console : 

~~~ bash
cd yourprezidir
cp prezi.app/Contents/Resources/movie.swf ./
~~~

Et voilà, votre prezi est prête. Il n'y a plus qu'à installer et configure le player flash qui la lira.

## flashplayer standalone
Alors, pour jouer vos prezi, il vous faudra un player flash standalone, c'est à dire utilisable depuis la ligne de commande.
Pour cela, il faut commencer par télécharger le fichier [flash_player_10_linux_dev.tar.gz](http://download.macromedia.com/pub/flashplayer/updaters/10/flash_player_10_linux_dev.tar.gz).
Copier le dans un répertoire, par exemple `~/soft`

Dans une console :

~~~ bash
cd ~/soft/
tar -xvzf flash_player_10_linux_dev.tar.gz
cd flash_player_10_linux_dev/standalone/release
tar -xvzf flashplayer.tar.gz
~~~

Et vous voilà avec un joli player flash en ligne de commande.
Je ne peux que vous conseiller de faire en sorte que l'exécutable flashplayer soit dans votre $PATH. D'ailleurs, je vous le conseille tellement que je ferai comme si c'était le cas :)

## configurer flashplayer
Par défaut, flash player en standalone, est configuré pour ne pas autoriser les appels de ressources externes. Et chose très drôles[^4], il n'y a aucun moyen[^5] de configurer par une option de la ligne de commande.

Pour autoriser l'accès aux ressources externes, il faut accéder au plugin flash qui charge le gestionnaires de conf depuis le site de macromedia[^6]. Actuellement, c'est par [ici](http://www.macromedia.com/support/documentation/en/flashplayer/help/settings_manager04a.html) que ça se passe.[^7].

Depuis le plugin, il faut ajouter le répertoire dans lequel vous avez mis votre présentation prezi (`~/presentation/` si vous avez suivi mes conseils). Cela autorisera votre présentation à charger les autres SWF dont elle a besoin.

## jouer votre présentation
Voilà, maintenant si tout s'est bien passé, plus rien ne devrait vous empêcher de lire votre superbe présentation. Il ne vous reste plus qu'à la lancer.
Dans une console :

~~~ bash
cd ~/presentation/yourprezidir/
flashplayer movie.swf
~~~

Enjoy !


[^1]: bravo et merci à lui
[^2]: l'application windows
[^3]: la version MacOS
[^4]: en fait non, je trouve même ça assez pitoyable
[^5]: du moins je n'en ai pas trouvé et stick84 non plus
[^6]: je vous avais dit que c'était pitoyable non ?
[^7]: il semble que cette page ait tendance à se déplacer. Pour la retrouver : google + `flash global security settings content creators`
