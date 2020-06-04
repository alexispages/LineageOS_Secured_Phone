# III) Création d'un build LineageOS pour piccolo

## 1) Installation d'adb et fastboot

Cette étape a déja été réalisée dans la partie II-4-b). <br/>
Rappel : on télécharge l'archive d'installation à l'adresse suivante : <br/>
https://dl.google.com/android/repository/platform-tools-latest-linux.zip <br/>
Dans notre répertoire personnel, on crée le dossier *adb-fastboot* dans lequel nous allons extraire le contenu de l'archive :
```
$ mkdir ~/adb-fastboot
$ unzip platform-tools_r30.0.1-linux.zip -d ~/adb-fastboot/
```
On édite le fichier *~/.bash_profile* en y ajoutant les lignes suivantes :
```
if [ -d "$HOME/adb-fastboot/platform-tools" ] ; then
 export PATH="$HOME/adb-fastboot/platform-tools:$PATH"
fi
```
On relance notre session afin de prendre en compte les changements opérés dans le fichier *~/.bash_profile*.

## 2) Paquets nécessaires au build

Plusieurs paquets sont nécessaires pour "construire" LineageOS. On utilisera la commande suivante pour les installer :
```
# pacman -S bc bison build-essential ccache curl flex g++-multilib gcc-multilib git gnupg gperf imagemagick lib32ncurses5-dev lib32readline-dev lib32z1-dev liblz4-tool libncurses5 libncurses5-dev libsdl1.2-dev libssl-dev libxml2 libxml2-utils lzop pngcrush rsync schedtool squashfs-tools xsltproc zip zlib1g-dev
```
Certains paquets comme build-essential ne sont pas disponibles sur Arch Linux. Il faudrait donc passer par une autre distribution linux pour procéder au build. Dans mon cas, j'ai choisi d'utiliser Debian.
