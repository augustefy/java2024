# Un petit système de fichiers et ses petites commandes

Le but du TP est de simuler un petit système de fichiers avec des répertoires et des fichiers textes sur lesquels on pourra appliquer des commandes (`ls -R`, `dump`, `du`, …).

## Fonctionnalités

* Tous les fichiers devront avoir un nom, une date de création (une vraie date hein !), ainsi que des droits (leur version en octal : 644, 750, etc.) qu'on ne pourra pas modifier une fois créés. Si non spécifiés, les droits par défaut seront 755 pour les dossiers et 644 pour n'importe quel autre fichier. On devra aussi pouvoir récupérer leur taille;
* Un fichier texte aura comme contenu initial celui passé en argument à sa construction. On devra aussi pouvoir rajouter du texte à ce dernier et récupérer l'ensemble du texte qu'il contient. Sa taille sera la longueur de son contenu textuel;
* La conversion d'un fichier texte en chaîne de caractères respectera le format :  
  "TextFile `nom_du_fichier` (`droits`) created on `date_de_creation`"
* Un répertoire pourra contenir plusieurs fichiers (au sens large) qui seront triés et uniques;
* La taille d'un répertoire sera le nombre de fichiers qu'il contient augmenté de 1;
* Deux fichiers sont identiques s'ils ont le même nom. Ils sont ordonnés par ordre alphabétique en fonction de leur nom;
* On pourra ajouter un fichier à un répertoire. Si le fichier est déjà présent, il faudra lever une `IllegalArgumentException` avec pour message : "This directory already contains the file nom_du_fichier";
* On devra pouvoir récupérer le contenu du répertoire sous forme d'une collection non modifiable;
* La conversion d'un répertoire en chaîne de caractères respectera le format :  
  "Directory `nom_du_fichier` (`droits`) created on `date_de_creation`"
* Une classe (`LsR`) implémentera le listing récursif d'un fichier : pour un fichier texte ça affichera simplement le fichier sur la sortie standard. Pour un dossier, on affichera une ligne du style "Directory [`nom_du_dossier`] content :" suivi du listing de ses fichiers. On terminera le listing d'un dossier par une ligne "-----".  
  *Les plus téméraires pourront tenter d'indenter le listing comme sur l'exemple, mais ne le faites que si vous avez fini le reste*
* Une classe (`Dump`) permettra d'enregistrer par sérialisation le contenu d'un fichier dans un vrai fichier (un de votre OS). Si une exception se produit, le texte "Le fichier n'a pas pu être écrit." sera écrit sur la *sortie d'erreur*, et le programme continuera comme si de rien n'était.
* Un `Dump` pourra être créé en spécifiant le chemin d'accès du fichier (celui de votre OS) dans lequel est effectuée la sauvegarde. Si ce chemin n'est pas spécifié, on utilisera le nom du fichier par défaut défini dans la classe qu'on placera dans le HOME de l'utilisateur (vous pouvez obtenir ce dernier grâce à l'appel `System.getProperty("user.home")`);
* On devra pouvoir ajouter d'autre commandes dans le futur (par exemple `du` qui affichera la taille totale de n'importe quel fichier) : pensez-y au moment de la conception !
* On devra pouvoir simuler des «petits scripts», c'est-à-dire créer des listes de commandes qu'on appliquera à un fichier.

# Exemple de résultat attendu

Voici l'affichage par `LsR` d'un `TextFile` simple, suivi de l'affichage d'un `Directory` qui contient à la fois deux `TextFile` et un `Directory` qui lui-même contient 4 `TextFile`. On finit en enregistant la hiérarchie avec un `Dump`.

```
TextFile Matrix.txt (644) created on 2018-03-16

Directory [home] content :
  TextFile H2G2 le guide du voyageur galactique.txt (644) created on 2018-03-16
  Directory [bpoo] content :
    TextFile TP1.java (644) created on 2018-03-16
    TextFile TPVoitures.java (644) created on 2018-03-16
    TextFile notes.txt (644) created on 2018-03-16
    TextFile énoncé.txt (644) created on 2018-03-16
  -----
TextFile news.txt (644) created on 2018-03-16
-----

Enregistrement dans le fichier /home/provot/hierarchy_dump
```
