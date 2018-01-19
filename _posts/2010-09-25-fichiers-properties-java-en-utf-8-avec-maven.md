---
layout: post
title: "fichiers .properties java en UTF-8 avec maven"
date: 2010-09-25 19:41:00 +0100
comments: false
categories: 
- ".properties"
- "ISO-8859-1"
- "java"
- "maven"
- "native2ascii"
---
![pom.xml.jpg](https://blog-img.crafting-labs.fr/logo/.pom.xml_s.jpg){: .left-image}
Une des limitations de java bien pénible pour nous les français, et autres gens, qui utilisons accents et caractères étranges, c'est l'obligation pour les fichiers .properties d'être encodés en ISO-8859-1... Et tous les caractères qui ne rentrent pas dans le moule se doivent d'être écrit en unicode. Autant dire que nos élégants caractères accentués se retrouve sous l'immonde forme \\u00e9, illisible et impossible à écrire...

Heureusement, maven et sa ribambelle de plugin sont encore là pour nous sauver la mise.


# Le problème
Pour faire les choses bien et faciliter l'internationalisation de votre appli en java, vous avez sorties toutes vos textes dans des fichiers .properties. Sauf que ceux-ci se doivent toujours d'être en ISO-8859-1[^1]. Si vous lisez l'unicode dans le texte, ça ne vous pose pas de soucis.
Mais si comme moi, vous aimez les accents[^2], êtes allergique à l'unicode et pensez que l'UTF-8, c'est quand même vachement bien, maven et le plugin native2ascii sont faits pour vous.
 
# La solution
# préliminaire
Pour mettre en oeuvre la solution, il faut que votre projet soit en maven2.

note : il semble que le plugin ne fonctionne pas avec la jvm JRockit 1.5. Pas de soucis avec la 1.5 de Sun[^3].

# le plugin native2ascii
Le sauveur c'est le plugin maven native2ascii.
Pour les détails, native2ascii est un outils fourni avec le jdk sun[^4] qui convertit un fichier de n'importe quel encodage vers ISO-8859-1.

Donc, dans votre pom.xml, dans la section `<build><plugins>`, il faut rajouter l'appel au plugin et sa configuration.

{% highlight xml %}
<plugin>
    <groupId>org.codehaus.mojo</groupId>
      <artifactId>native2ascii-maven-plugin</artifactId>
      <executions>
          <execution>
              <id>native2ascii</id>
              <goals>
                  <goal>native2ascii</goal>
              </goals>
              <!-- specific configurations -->
              <configuration>
	          <encoding>UTF8</encoding>
                  <src>src/main/java</src>
                  <includes>**/*.properties</includes>
              </configuration>
          </execution>
      </executions>
</plugin>
{% endhighlight %}

La configuration du plugin :

* `<encoding>` permet de préciser le format d'origine du fichier à convertir.
* `<src>` le repertoire depuis lequel on va chercher les fichiers.
* `<includes>` le pattern des fichiers à traiter.

Par défaut, `native2ascii` placera les fichiers convertis dans le répertoire `${project.build.directory}/native2ascii`

## filtrer les resources
C'est bien, on a nos fichiers dans le bon format dans un répertoire. C'est bien beau, encore faut-il utilisés ceux-ci et pas leurs versions en UTF-8 qui se trouvent avec le code.
Pour cela, on va dire à maven de ne pas utiliser les fichiers .properties qui sont dans le code, et utiliser à la place ceux que l'on vient de convertir. Et au passage, ça fera même du filtering sur les fichiers :)
Dans la section `<build>`, on rajoute ou modifie la section `<resources>` :

{% highlight xml %}
<resources>
    <resource>
        <filtering>true</filtering>
        <directory>src/main/java</directory>
        <includes>
           [...]
        </includes>
        <!-- on exclut les fichiers .properties présents dans les sources -->
        <excludes>
            <exclude>**/*.properties</exclude>
        </excludes>
    </resource>
    <!-- on filtre les .properties convertis par native2ascii -->
    <resource>
        <filtering>true</filtering>
        <directory>${project.build.directory}/native2ascii</directory>
        <includes>
            <include>**/*.properties</include>
        </includes>
    </resource>
</resources>
{% endhighlight %}

La première `<resource>`, c'est pour dire à maven d'exclure des ressources les fichiers .properties qui sont dans le répertoire des sources.
La seconde `<resource>`, c'est pour dire à maven de faire du filtering sur les fichiers convertis par native2ascii. Après le filtering, ils seront placés au coté des sources que maven utilisera pour la compile et le packaging.

Et voilà, c'est aussi simple que ça.

#Pour aller plus loin

* la page du plugin maven [native2ascii](http://mojo.codehaus.org/native2ascii-maven-plugin/) sur Codehaus
* la javadoc de la classe [`Properties`](http://download.oracle.com/javase/6/docs/api/java/util/Properties.html)
* la doc de l'outil [native2ascii](http://download.oracle.com/javase/6/docs/technotes/tools/solaris/native2ascii.html) chez --Sun-- Oracle
### Remerciements
Merci à Olivier Huber pour m'avoir suggéré qu'une telle manip devait exister lors de son passage par chez nous pour donner une excellente formation Wicket.


[^1]: connu aussi sous le nom de Latin-1, autrement dit, l'alphabet des anglophones sans accents
[^2]: et militez activement pour le retour de l'accentuation des capitales
[^3]: oui, je sais, c'est Oracle maintenant, mais j'arrive pas à m'y faire
[^4]: ce qui explique peut être pourquoi ça ne fonctionne pas avec celle de BEA :)
