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
On installera donc les paquets de cette manière :
```
# apt install bc bison build-essential ccache curl flex g++-multilib gcc-multilib git gnupg gperf imagemagick lib32ncurses5-dev lib32readline-dev lib32z1-dev liblz4-tool libncurses5 libncurses5-dev libsdl1.2-dev libssl-dev libxml2 libxml2-utils lzop pngcrush rsync schedtool squashfs-tools xsltproc zip zlib1g-dev
```
Il est également nécessaire d'installer le kit de développement Java (*Java OpenJDK*). Dans notre cas, nous souhaitons créer un build de LineageOS 14.1. Il nous faudra donc installer *OpenJDK 1.8*. On ajoute le dépôt adopt OpenJDK :
```
$ wget -qO - https://adoptopenjdk.jfrog.io/adoptopenjdk/api/gpg/key/public | sudo apt-key add -
# add-apt-repository --yes https://adoptopenjdk.jfrog.io/adoptopenjdk/deb/
```
On installe *OpenJDK 1.8* :
```
# apt update
# apt install adoptopenjdk-8-hotspot
$ java -version
openjdk version "1.8.0_222"
OpenJDK Runtime Environment (AdoptOpenJDK)(build 1.8.0_222-b10)
OpenJDK 64-Bit Server VM (AdoptOpenJDK)(build 25.222-b10, mixed mode)
```

## 3) Création des répertoires de build

Dans cette partie, nous allons créer les répertoires nécessaires à l'environnement de build :
```
$ mkdir -p ~/bin
$ mkdir -p ~/android/lineage
```
Le répertoire *~/bin* contiendra l'outil **repo** et le répertoire *~/android/lineage* contiendra le code source de LineageOS.
