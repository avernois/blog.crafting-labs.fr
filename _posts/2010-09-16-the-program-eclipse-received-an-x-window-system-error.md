---
layout: post
title: "The program 'Eclipse' received an X Window System error."
date: 2010-09-16 21:58:00 +0100
comments: false
categories: 
- "bug"
- "eclipse"
- "error"
- "xulrunner"
---
![large eclipse logo.jpg](https://blog-img.crafting-labs.fr/logo/.large_eclipse_logo_s.jpg){: .left-image}
Depuis, la dernière mise à jour de mon système(ubuntu 10.4) et de mon eclipse (helios), ce dernier explosait lamentablement en vol en utilisant l'autocomplétion avec l'immonde erreur :

> The program 'Eclipse' received an X Window System error.
 This probably reflects a bug in the program.
 The error was 'RenderBadPicture (invalid Picture parameter)'.
  (Details: serial 16698 error_code 158 request_code 148 minor_code 7)
  (Note to programmers: normally, X errors are reported asynchronously;
   that is, you will receive the error a while after causing it.
   To debug your program, run it with the --sync command line
   option to change this behavior. You can then get a meaningful
   backtrace from your debugger if you break on the gdk_x_error() function.)

Ca semble assez vilain comme ça mais ça se soigne assez bien.


#version simple
Il suffit de lancer eclipse avec l'option __-vmargs -Dorg.eclipse.swt.browser.XULRunnerPath__[^1]

et voilà...


#version longue
euh, en fait non... je n'ai pas encore vraiment compris l'origine du problème... J'ai trouvé la solution en fouillant le bugzilla d'eclipse, le problème est abordé dans plusieurs bugs dont le [304718](https://bugs.eclipse.org/bugs/show_bug.cgi?id=304718) qui évoque ce workaround.


[^1]: ou de rajouter -Dorg.eclipse.swt.browser.XULRunnerPath dans le eclipse.ini
