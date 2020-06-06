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

## 4) Mise en place de la commande repo

Pour télécharger l'outil **repo** et le rendre exécutable, on entre ceci :
```
$ curl https://storage.googleapis.com/git-repo-downloads/repo > ~/bin/repo
$ chmod a+x ~/bin/repo
```
On édite le fichier *~/.bash_profile* en y ajoutant les lignes suivantes :
```
# set PATH so it includes user's private bin if it exists
if [ -d "$HOME/bin" ] ; then
    PATH="$HOME/bin:$PATH"
fi
```
On met à jour notre envionnement :
```
$ source ~/.bash_profile
```

## 5) Configuration de git

L'outil **repo** exige que l'on s'identifie pour synchroniser Android. On exécutera alors les commandes suivantes pour s'identifier sur git :
```
git config --global user.email "vous@exemple.com"
git config --global user.name "Votre Nom"
```

## 6) Téléchargement du code source de LineageOS

Afin d'initialiser le dépôt de la vesion **14.1 de LineageOS**, on entre ces commandes :
```
$ cd ~/android/lineage
$ repo init -u https://github.com/LineageOS/android.git -b cm-14.1
repo has been initialized in /home/apages/android/lineage
```
Il est fortement recommandé d'utiliser La configuration par défaut pour l'outil **repo**. Les valeurs par défaut de la commande **repo** sont *-j 4* et *-c*. *-j 4* signifie qu'il y aura quatre connexions simultanées. Si l'on observe des problèmes de synchronisation, on pourra abaisser cette valeur à *-j 3* ou *-j 2*. D'autre part, l'option *-c* demande à l'outil repo de ne récupérer que la branche courante au lieu de toutes les branches disponibles sur GitHub c'est à dire seulement la version de LineageOS qui nous intéresse.
Pour lancer le téléchargement du code source sur notre ordinateur, on entrera ce qui suit :
```
$ repo sync
```
À noter que cette étape prendra plusieurs dizaines de minutes ! Une fois le téléchargement terminée, vous obtiendrez le résultat suivant :
```
repo sync has finished successfully.
```

## 7) Mise en place de la configuration matérielle et du noyau

On vérifie que l'on se situe toujours dans le répertoire *~/android/lineage* :
```
$ pwd
/home/apages/android/lineage
```
On lance ensuite le téléchargement de la configuration matérielle spécifique à notre appareil et du noyau :
```
$ source build/envsetup.sh
$ breakfast piccolo
```
Important : certains appareils nécessitent que le répertoire *vendor* soit rempli avant d'exécuter la commande *breakfast*. Si l'on reçoit une erreur concernant les *vendor makefiles*, il faut se rendre à l'étape "8) Extraire les blobs propriétaires". Il vous faudra alors relancer la commande breakfast après l'étape 8).

## 8) Extraction des blobs propriétaires

### a) Qu'est-ce qu'un blob propriétaire ?

Un pilote de périphérique propriétaire est un pilote de périphérique à source fermée publié uniquement en code binaire. On appelle ce type de pilote **"*blob*" ou "*binary blob*"**. <br/>
Les blobs propriétaires peuvent être extraits soit depuis notre appareil fonctionnant déjà sous LineageOS, soit depuis un zip d'installation de LineageOS. Nous allons décrire ici les étapes nécessaires pour extraire des fichiers propriétaires à partir d'un zip installation. <br/>

### b) Les différents types d'OTA

Avant de commencer, il est nécessaire de connaître la différence entre les types d'OTA :
- OTA par blocs : le contenu de la partition du système est stocké dans un fichier .dat/.dat.br sous forme de données binaires.
- OTA basé sur un fichier : le contenu de la partition système est disponible dans un dossier du système nommé zip.
- OTA basé sur la charge utile : le contenu de la partition système est stocké dans un fichier .img à l'intérieur du fichier payload.bin.

### c) Analyse du fichier d'intallation *.zip*

Pour cette partie, nous allons avoir besoin du fichier ***lineage-14.1-20190303-microG-piccolo.zip***. 3 cas sont possibles :
1) Le fichier zip ne contient pas de dossier *system* ou il est presque vide contient un fichier nommé *system.transfer.list* au niveau de la racine. Il s'agit alors d'un OTA basé sur des blocs. Dans ce cas, on procédera à l'*extraction de blobs propriétaires à partir d'OTA basés sur des blocs* (voir https://wiki.lineageos.org/extracting_blobs_from_zips.html#extracting-proprietary-blobs-from-block-based-otas).
2) La totalité de la partition système est située dans le dossier *system* et il n'y a pas de fichier *system.transfer.list*. Il s'agit alors d'un OTA basé sur des fichiers. Dans ce cas, on procédera à l'*extraction de blobs propriétaires à partir d'OTA basés sur des fichiers* (voir https://wiki.lineageos.org/extracting_blobs_from_zips.html#extracting-proprietary-blobs-from-file-based-otas).
3) Si vous n'êtes pas dans l'un de ces deux cas, alors il faudra procéder à l'*extraction de blobs propriétaires à partir d'OTA basés sur la charge utile* (voir https://wiki.lineageos.org/extracting_blobs_from_zips.html#extracting-proprietary-blobs-from-payload-based-otas).

On entre la commande suivante pour vérifier le contenu de notre fichier après l'avoir extrait dans le répertoire *lineage-14.1-20190303-microG-piccolo* :
```
$ ls ~/home/apages/lineage-14.1-20190303-microG-piccolo
boot.img  file_contexts.bin  install  META-INF  system  system.new.dat  system.patch.dat  system.transfer.list
```
On remarque que notre archive zip contient un fichier *system.transfer.list* au niveau de la racine. Nous nous trouvons donc dans le 1er cas (**OTA basé sur des blocs**).
Certains OTA basés sur des blocs sont divisés en plusieurs fichiers : un pour la partition système et ceux pour d'autres partitions comme *vendor, product, oem, odm, etc...* Si tel est le cas, il y aura plusieurs fichiers sous la forme \*.transfer.list correspondants à chacune des partitions présentes dans la racine du zip LinageOS.
Si notre fichier OTA basé sur des blocs comporte plusieurs partitions séparées, on va devoir extraire, décompresser et convertir chacun des fichiers de la même manière que pour le fichier *system.transfer.list* comme indiqué ci-après. <br/>

### d) Extraction des blobs propriétaires à partir d'OTA basés sur des blocs

Dans notre cas, notre répertoire contient seulement un fichier *system.transfer.list*
On crée un répertoire temporaire et on s'y déplace :
```
$ mkdir ~/android/system_dump/
$ cd ~/android/system_dump/
```
On extrait le fichier *system.tranfer.file* et *system.new.dat.br* ou *system.new.dat* à partir du zip LineageOS :
```
$ unzip ~/lineage-14.1-20190303-microG-piccolo.zip system.transfer.list system.new.dat*
Archive:  /home/apages/lineage-14.1-20190303-microG-piccolo.zip
signed by SignApk
  inflating: system.new.dat          
  inflating: system.transfer.list 
```
Nous allons maitenant télécharger une copie de *sdat2img*. Ce script est capable de convertir le contenu d'OTAs basés sur des blocs en dépôts pouvant être montés. *sdat2img* est disponible dans le dépôt git suivant que vous pouvez cloner avec :
```
$ git clone https://github.com/xpirt/sdat2img
Clonage dans 'sdat2img'...
remote: Enumerating objects: 109, done.
remote: Total 109 (delta 0), reused 0 (delta 0), pack-reused 109
Réception d'objets: 100% (109/109), 26.36 KiB | 499.00 KiB/s, fait.
Résolution des deltas: 100% (27/27), fait.
```
On utilise *sdat2img* pour extraire l'image du système :
```
$ python sdat2img/sdat2img.py system.transfer.list system.new.dat system.img
[...]
Done! Output image: /home/apages/android/system_dump/system.img
```
Comme onpeut le voir ci-dessus, un fichier *system.img* a été créé. Nous allons monter cette image de la manière suivante :
```
$ mkdir system/
# mount system.img system/
```
On se rend dans le répertoire *~/android/lineage/device/bq/piccolo* et on exécute le script *extract-files* avec pour cible *~/android/system_dump/*. Cela permet d'indiquer au script *extract-files.sh* de récupérer les fichiers à partir du répertoire *~/android/system_dump/system* que l'on vient de monter plutôt qu'à partir d'un appareil connecté.:
```
$ cd ~/android/lineage/device/bq/piccolo
$ ./extract-files.sh ~/android/system_dump/
```
Une fois tous les fichiers propriétaires extraits, on démonte le répertoire *~/android/system_dump/system* :
```
# umount /home/apages/android/system_dump/system
```
Enfin, on supprime le répertoire *~/android/system_dump* dont nous n'avons plus besoin :
```
$ rm -rf ~/android/system_dump/
```
Pour compléter la commande *breakfast* de la partie 7), on l'exécutera à nouveau :
```
$ cd ~/android/lineage/
$ breakfast piccolo
```

## 9) Activation de la mise en cache

### a) Qu'est-ce que la mise en cache ?
Un cache est une couche de stockage de données grande vitesse qui stocke un sous-ensemble de données pour que les demandes futures pour ces données soient traitées le plus rapidement possible en accédant à leur emplacement. La mise en cache permet de réutiliser efficacement ces données stockées en utilisant du matériel à accès rapide comme de la RAM (mémoire vive).

### b) Mise en place de l'outil ccache
Pour activer la mise en cache, nous allons utiliser l'outil **ccache** ce qui va nous permettre d'accélérer la procédure de build. Pour cela, on ajoute les lignes suivantes au fichier *~/.bashrc* :
```
export USE_CCACHE=1
export CCACHE_EXEC=/usr/bin/ccache
```
Ensuite, on indique la quantité maximale d'espace disque que l'on souhaite utiliser avec ccache. On prendra une valeur entre 25 Go et 100 Go. La vitesse du *build* sera considérablement augmentée (par exemple : une procédure d'une heure peut être réduite à 20 minutes). Si l'on crée un *build* pour un seul appareil, 25Go à 50Go seront suffisants. Si l'on prévoie de créer un *build* pour plusieurs appareils qui ne partagent pas le même noyau, on choisira plutôt entre 75Go et 100Go d'espace disque.
**ATTENTION : Cet espace sera occupé en permanence sur votre disque !**
Pour définir la quantité maximale d'espace disque à utiliser avec ccache (ici 50Go), on entrera ceci :
```
$ ccache -M 50G
Set cache size limit to 50.0 GB
```
On pourra également activer la *compression ccache*. Bien que cela puisse impliquer un léger ralentissement des performances, cette option augmente le nombre de fichiers contenus dans le cache. Pour l'activer, on ajoutera la ligne suivante au fichier *~/.bashrc* :
```
export CCACHE_COMPRESS=1
```

## 10) Configuration de l'outil *Jack*

Jack est une chaîne d'outils[1] Java actuellement utilisée pour contruire LineageOS 14.1 et 15.1. Il est connu pour manquer souvent de mémoire s'il n'est pas configuré correctement. On peut corriger simplement ce défaut en ajoutant au fichier *~/.bashrc* cette ligne afin de lui allouer 4Go de RAM :
```
export ANDROID_JACK_VM_ARGS="-Dfile.encoding=UTF-8 -XX:+TieredCompilation -Xmx4G"
```
## 11) Lancement de la procédure de *build*

Nous allons maintenant lancer la procédure de build avec les commandes suivantes :
```
$ croot
$ brunch piccolo
```

## Lexique
- [1] https://fr.wikipedia.org/wiki/Cha%C3%AEne_d%27outils_Devops
