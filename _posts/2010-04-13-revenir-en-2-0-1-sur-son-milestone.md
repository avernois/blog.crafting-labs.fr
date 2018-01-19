---
layout: post
title: "Revenir en 2.0.1 sur son milestone"
date: 2010-04-13 19:13:00 +0100
comments: false
categories: 
- "2.0.1"
- "2.1"
- "android"
- "milestone"
- "motorola"
- "restauration"
---
![android.gif](https://blog-img.crafting-labs.fr/logo/.android_s.jpg){: .left-image}
Comme moi et beaucoup d'autres vous vous êtes précipité pour installer la nouvelle mise à jour en 2.1 sur votre milestone. Et comme moi et beaucoup d'autres, après un bref moment de joie, vous avez déchanté devant l'instabilité du système avec une seule envie, oublier cette erreur et retrouver cette chère 2.0.1 qui marchait pas si mal.

Et bien c'est faisable ! Et en plus, je vous explique comment.


# Mise en garde
Attention, la manip qui suit va remplacer tout ce qui se trouve dans la mémoire interne du téléphone. Donc si vous avez des choses importantes (des sms, des configs, des applis, et autre) sauvegardez les précieusement en dehors de votre téléphone !

Attention, je n'ai testé cette manip que depuis un tel qui n'a jamais été bidouillé (pas de root, pas de manip bizarre, de rom modifié, etc). Si ça n'est pas votre cas, peut être, ça marche, peut être ça marche pas :)

Attention, dans tous les cas, je ne garantie aucun résultat. Peut être ça marche, peut être ça marche pas. Ça marché pour moi, y'a pas de raison que ça soit pas le cas pour vous, mais peut être pas !

Allez, j'arrête là pour les avertissements, vous aurez compris le principe : je ne suis responsable de rien :) Passons au chose sérieuse.

# Les choses sérieuses
## Environnement
Cette manip se fait sous windows[^1]. Il vous faudrai quelque truc en plus :

* un cable usb-micro usb pour connecter votre milestone
* les drivers qui vont bien pour votre appareil[^2]
* le logiciel [RSD-lite 4.6](http://aschen.net/android/RSDLite4.6.msi)
* le fichier [SBF de la 2.0.1](https://rsddownload.motorola.com/download/SHOLS_U2_01.15.0_UCASHLSEMEAB1B803F.0R_USASHLS00AZRTEMARA_P016_A003_HWp2a_1FF.sbf.gz)

Avec tout ça, vous devriez être paré. Évidemment, il faut que les drivers et RSD Lite soient installés, il faudra également décompressé le fichier .gz du SBF[^3].

## Démarrer en mode bootloader
Normalement, on a maintenant tout ce qu'il faut pour commencer. La première étape est redémarrer votre milestone en mode bootoader. Pour cela :

* éteindre le téléphone
* ouvrir le clavier physique
* appuyer sur le haut du pad et appuyer en même temps sur le bouton d'allumage. Maintenez les deux jusqu'à ce que vous voyez apparaître un écran noire avec quelque truc écrit en blanc. C'est le mode bootloader

## Charger le sbf
Il ne reste plus qu'à flasher tout ça.

* brancher votre milestone à votre pc via le câble réseau
* lancer RSD Lite. Il doit reconnaitre votre téléphone. 
* sélectionner votre fichier SBF.
* appuyez sur start.
* attendez. Votre téléphone va rebooter plusieurs fois. Surtout ne le débranchez pas tant que RSD ne vous indique pas que tout va bien dans la liste de progression.

Si tout c'est bien passez, vous voilà de retour en 2.0.1. Avec seulement 3 bureaux et pas de reconnaissance vocale, mais la possibilité d'être appelé sans problème et ça reste ce que je demande en premier à un  téléphone :)

Vous n'avez plus qu'a réinstaller vos logiciels et restaurer vos sauvegardes. Enjoy :)

Ce petit tuto a été écrit grâce aux infos trouvées sur le wiki [and-developers.com](http://www.and-developers.com/).


[^1]: je n'ai pas essayé, mais peut être que ça fonctionnerait sous wine
[^2]: si vous êtes passé en 2.1, c'est que vous les avez déjà :)
[^3]: avec un soft comme 7-Zip par exemple
