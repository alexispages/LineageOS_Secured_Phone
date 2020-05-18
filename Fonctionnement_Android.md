# I) Fonctionnement d'Android

## 1) Présentation d'Android

### a) Histoire
Lancé en juin 2007, Android est aujourd'hui le système d'exploitation le plus utilisé au monde sur smartphone [1]. Après le rachat de la société par Google en 2005, le géant américain a continué à travailler dessus et, aujourd'hui encore, l'améliore autant que possible. Chaque année, Google propose une nouvelle version majeure d'Android et, de manière plus régulière, il met à disposition diverses mises à jour de sécurité mineures.

### b) Qu'est-ce qu'Android ?

Android est ce que l'on appelle un système d'exploitation (Operating Sytem en anglais). Son rôle est de faire le lien entre le smartphone et l'utilisateur. Ce dernier va ainsi pouvoir interagir avec les composants du smartphone par le biais d'une interface graphique.

Le format des appareils mobiles étant différent, Android a donc du être adapté pour faciliter leur utilisation. Basé sur le noyau[2] Linux, Android est développé par la société Google et est supporté par de très nombreuses entreprises : 
- Opérateurs : T-Mobile, Bouygues Telecom, etc. 
- Constructeurs : Samsung, LG, HTC, etc. 
- D’autres acteurs nécessaire à cet cet éco-système : Intel, Qualcomm ou encore Nvidia 
Cet ensemble d’entreprises supportant Android se nomme l’Open Handset Alliance (OHA) et est composé d’une trentaine d’acteurs.

### c) Les différentes versions du système

La déclinaison la plus basique (la plus "pure") se nomme Android Stock, c’est celle qui est utilisée sur les appareils de Google comme la gamme Pixel par exemple. Certains constructeurs ont également pris le parti de proposer une expérience "pure" en rejoignant le programme Android One. Néanmoins, la plupart des constructeurs de smartphones utilisent la version de base d’Android (Android Open Source Project ou AOSP) à laquelle ils ajoutent les composants développés par Google et ce que l'on appelle une "surcouche" venant rajouter des fonctionnalités et modifiant l'apparence de base du système de Google.

En conclusion, on peut dire qu'Android s'est placé en véritable leader du marché des systèmes d'exploitation pour appareils mobiles (téléphones et tablettes), en proposant une expérience basée sur une interface modulable capable de correspondre au plus grand nombre.

## 2) L'architecture d'Android

Android est constitué d'une pile de composants. Le sens de lecture s'effectue de bas en haut. Nous allons analyser par la suite l'ensemble des couches composant le système Android[3].

### a) Le Noyau Linux

Il s'agit de la couche gérant le matériel de l'appareil mobile (écran, caméra, support de stockage, etc...). C'est elle qui va permettre aux logiciels embarqués dans l'appareil d'accéder à ces composants. La version utilisée par Android a été élaborée spécialement pour un environnement mobile en se focalisant sur des aspects tels que la gestion énergétique (batterie) et de la mémoire. En résumé, c'est cette couche qui permet à Android d'être compatible avec un très grand nombre d'appareils aux configurations matérielles très différentes.

### b) La Couche d'abstraction matérielle ou Hardware Abstraction Layer (HAL) propriétaire de Google

Cette couche se compose de plusieurs modules[4] d'une bibliothèque logicielle[5], chacun d'entre eux étant lié à un type spécifique de matériel comme la caméra ou le module bluetooth. Ainsi, lorsqu'une API[6] du framework[7] Java va demander à accéder au matériel de notre appareil, Android chargera le module correspondant au composant à utiliser. C'est cette couche qui permet à une application de s'adpater au matériel embarqué dans un appareil. 

En réalité, le noyau Linux fournit déjà une compatibilité avec le matériel embarqué. L'objectif pour Google en ayant rajouté cette couche est de "sécuriser" le système en rendant privé le code source permettant d'exploiter le matériel d'un appareil. Cette solution permet notamment à Android de s'affranchir de la license open source imposé par l'utilisation du noyau Linux. Ce dernier constituait déjà une HAL et à longtemps été utilisé sans cette couche supplémentaire mais la volonté de Google est désormais d'éviter au maximum son utilisation.

### c) Le moteur d'exécution d'Android

Il s'agit d'un élément crutial du système car c'est ce dernier qui va permettre d'exécuter des applications basées sur le langage de programmation Java et certains services système d'Android. Ce moteur d'exécution se divise en deux parties : un environnement d'exécution des applications, et des bibliothèques de base (Core libraries) sur lesquelles nous reviendrons dans un second temps.

#### *L'environnement d'exécution*

Afin d'exécuter des applications en Java, il existe un outil qui se nomme *Java Runtime Environment* (ou Envrionnement d'exécution Java en français). En outre, ce dernier n'est pas adapté à un environnement mobile et possède de nombreuses fonctionnalités inadaptées. L'enjeu majeur lors du développement d'Android a donc été de développer un environnement d'exécution optimisé pour mieux gérer les ressources physiques du système. L'objectif était de laisser moins d'empreinte mémoire[8] (la quantité de mémoire allouée à une application pendant son exécution) ou d'utiliser moins de batterie.

C'est ainsi qu'est née la machine virtuelle[9] Dalvik, spécialement développée pour les systèmes embarqués.

Schéma du fonctionnement de Dalvik [10]

Le schéma ci-dessus explique le processus de construction d'une application avec Dalvik. Dans un premier temps, le développeur va produire un fichier *.java* contenant une suite d'instructions dans le langage de programmation Java. Ce fichier va ensuite être traduit dans ce que l'on appelle du *bytecode Java* qui sera contenu à son tour dans un fichier *.class*. On pourra par la suite regrouper différents fichiers *.class* en un fichier *.jar* qui sera exécutable dans l'environement d'exécution Java. Or, la machine virtuelle Dalvik possède son propre bytecode. Il est donc nécessaire de passer du *bytecode Java* au *bytecode Dalvik* (création d'un fichier *.dex*) avec une fonction nommée *dx* afin de pouvoir exécuter une application sur Android.

L'avantage majeur de Dalvik réside dans la gestion des processus[11]. L'objectif va être d'isoler chacun des processus les uns par rapport aux autres en associant un processus à une machine virtuelle. Par ce biais, si un processus dysfonctionne, les autres ne vont pas être impactés. Ainsi, chaque processus est protégé des autres ce qui renforce la protection du système.

À partir de la version 5.0 d'Android (sortie en 2014), Dalvik a été remplacée par l'*Android Runtime* (ART) qui permet de transcrire le *bytecode java* directement en langage machine[12]. Les gains apportés en performance et en autonomie des batteries sont conséquents avec une augmentation de 20 à 30%. En contre-partie, la taille des applications a augmenté de 20%.

Il ne manque plus qu'une étape avant d'exécuter une application : le manifest. Ce dernier contient diverses informations sur l'application notamment les autorisations dont l'application a besoin pour accéder à des parties protégées du système (accès au stockage, à la caméra, à la géolocalisation, etc...) ou à d'autres applications. Il déclare également les autorisations que les autres applications doivent avoir pour accéder au contenu de cette application. Il recense aussi les fonctionnalités matérielles et logicielles requises par l'application, ce qui affecte les appareils pouvant installer l'application à partir du Google Play Store. Par exemple, si votre appareil dispose d'une version trop ancienne d'Android, il ne pourra pas installer certaines applications.

En ajoutant ce manifest au langage machine obtenu lors de la dernière étape du processus de construction d'une application, l'environnement d'exécution d'Android (ART) va ainsi pouvoir exécuter notre application qui sera désormais au format *.apk*.

#### *Les "Bibliothèques de base" (Core Libraries)*

Les *Core Libraries* d'Android sont constituées d'une copie des *Core Librairies* de Java 8 (les versions postérieures n'étant pas supportées par Android) et d'un ensemble de bibliothèques basées sur Java spécifiques au développement d'Android. Voici les principales biliothèques de base que l'on peut trouver dans cet ensemble :
- **android.app** - Fournit un accès au modèle d'application et constitue la pierre angulaire de toutes les applications Android.
- **android.content** - Facilite l'accès au contenu, la publication et la communication entre les applications et les composants d'applications.
- **android.database** - Utilisée pour accéder aux données publiées par les fournisseurs de contenu et comprend des classes de gestion de base de données[13] *SQLite*.
- **android.graphics** - API de dessin graphique en 2D comprenant des couleurs, des points, des filtres, des rectangles et des canvas[14].
- **android.hardware** - API permettant d'accéder à du matériel tel que l'accéléromètre et le capteur de lumière.
- **android.opengl** - Interface Java pour piloter l'API de rendu graphique en 3D *OpenGL ES*.
- **android.os** - Fournit aux applications l'accès aux services standards du système d'exploitation, notamment les messages, les services système et la communication entre les processus.
- **android.media** - Fournit des classes[15] pour permettre la lecture de fichiers audio et vidéo.
- **android.net** - Un ensemble d'API donnant accès à la partie réseau. Comprend android.net.wifi, qui permet d'accéder à la partie réseau sans fil de l'appareil.
- **android.print** - Comprend un ensemble de classes qui permettent d'envoyer du contenu à des imprimantes configurées à partir d'applications Android.
-  **android.provider** - Un ensemble de classes qui permettent d'accéder aux bases de données standards des fournisseurs de contenu Android notamment celles gérées par les applications de calendrier et de contact.
-  **android.text** - Utilisé pour présenter et manipuler du texte sur l'écran d'un appareil.
-  **android.util** - Ensemble de classes d'utilitaires permettant d'effectuer des tâches telles que la conversion de chaînes de caractères ou de nombres, le traitement XML[16] et la manipulation de la date et de l'heure.
- **android.view** - Fournit les éléments de base des interfaces utilisateur des applications.
-  **android.widget** - Un ensemble de composants d'interface utilisateur pré-construits tels que des boutons, des étiquettes, des listes, des gestionnaires de mise en page, des boutons radio, etc...
- **android.webkit** - Un ensemble de classes destinées à permettre l'intégration de fonctions de navigation sur le web dans les applications.

### d) Bibliothèques C/C++

Les bibliothèques de base d'Android que nous venons de décrire dans la partie précédente sont basées sur Java et fournissent les API principales pour les développeurs qui écrivent des applications Android. Il est important de noter que les bibliothèques de base n'effectuent pas une grande partie du travail réel et constituent, en réalité essentiellement un élément central écrit en Java autour duquel s'inscrit un ensemble de bibliothèques basées sur les langages de programmation C et C++. Lorsque l'on fait appel, par exemple, à la bibliothèque android.opengl pour afficher des graphismes en 3D sur l'écran de l'appareil, la bibliothèque fait en fait appel à la bibliothèque C++ OpenGL ES qui, à son tour, travaille avec les couches sous-jacentes (Noyau Linux et HAL propriétaire de Google) pour effectuer les tâches d'affichage.

Les bibliothèques C/C++ sont incluses pour remplir un large éventail de fonctions diverses, notamment l'affichage graphique en 2D et 3D, la communication TLS/SSL[17], la gestion de bases de données SQLite, la lecture audio et vidéo, le rendu de polices d'écriture bitmap et vectorielles, la gestion des sous-systèmes d'affichage et des couches graphiques et une implémentation de la bibliothèque système C standard (libc)[18].

En pratique, le développeur d'applications Android accédera à ces bibliothèques uniquement par le biais des API de la bibliothèque centrale d'Android basée sur Java. Si un accès direct à ces bibliothèques est nécessaire, il peut être réalisé en utilisant l'Android Native Development Kit (NDK) dont le but est d'appeler les méthodes natives des langages de programmation non Java ou Kotlin (tels que C et C++) à partir du code Java en utilisant l'interface native Java (JNI).

### e) Java API Framework

Le cadre d'application (*framework* en anglais) est un ensemble de services qui forment collectivement l'environnement dans lequel les applications Android fonctionnent et sont gérées. Ce cadre met en œuvre le concept selon lequel les applications Android sont construites à partir de composants réutilisables, interchangeables et remplaçables. Ce concept est poussé plus loin en ce sens qu'une application est également capable de publier ses capacités ainsi que toutes les données correspondantes afin qu'elles puissent être trouvées et réutilisées par d'autres applications.

#### Qu'est-ce qu'un service ?

Un service est un composant d'application qui peut effectuer des opérations de longue durée en arrière-plan. Il ne fournit pas d'interface utilisateur. Si un autre composant d'application démarre un service, celui déjà lancé continuera à fonctionner en arrière-plan même si l'utilisateur passe à une autre application. Un service peut traiter des transactions réseau, jouer de la musique, effectuer des déplacements de fichiers ou interagir avec un fournisseur de contenu, le tout, en arrière-plan. Les services système jouent un rôle clé en exposant les fonctions de bas niveau du matériel et du noyau Linux aux applications de haut niveau. Les services système sont actifs du démarrage au redémarrage, c'est-à-dire pendant toute la durée de vie du système.

Il existe 3 types de services :

- **Premier plan** - Un service de premier plan effectue une opération qui est perceptible par l'utilisateur. Par exemple, une application audio utiliserait un service d'avant-plan pour lire et afficher celle en cours de lecture. Les services d'avant-plan affichent une notification et continuent de fonctionner même lorsque l'utilisateur n'interagit pas avec l'application.
- **Arrière-plan** - Un service d'arrière-plan effectue une opération qui n'est pas directement remarquée par l'utilisateur. Par exemple, si une application utilise un service pour compacter son stockage, il s'agit généralement d'un service d'arrière-plan.
- **Relié** - Un service est lié lorsqu'un composant d'application se lie à lui en appelant la fonction *bindService()*. Un service lié offre une interface client-serveur qui permet aux composants d'interagir avec le service, d'envoyer des demandes et de recevoir des résultats. Un service lié ne fonctionne que tant qu'un autre composant de l'application lui est lié. Plusieurs composants peuvent se lier au service en même temps, mais lorsque tous se délient, le service est détruit.

#### Les services du framework

Le framework d'Android comprend les principaux services suivants :

- **Activity Manager** - Contrôle tous les aspects du cycle de vie des applications et de leurs activités.
- **Fournisseurs de contenu** - Permet aux applications de publier et de partager des données avec d'autres applications.
- **Gestionnaire de ressources** - Fournit l'accès aux ressources intégrées non codées telles que les chaînes de caractères, les paramètres de couleur et la disposition de l'interface utilisateur.
- **Gestionnaire de notifications** - Permet aux applications d'afficher des alertes et des notifications à l'utilisateur.
- **Système de visualisation** - Ensemble extensible d'éléments visuels utilisées pour créer les interfaces utilisateur des applications.
- **Gestionnaire de paquets** - Système permettant aux applications de trouver des informations sur d'autres applications actuellement installées sur l'appareil.
- **Gestionnaire de téléphonie** - Fournit à l'application des informations sur les services de téléphonie disponibles sur l'appareil, comme le statut et les informations sur l'abonné.
- **Gestionnaire de localisation** - Fournit l'accès aux services de localisation permettant à une application de recevoir des mises à jour sur les changements de localisation.

### f) Les applications

Les applications sont situées au sommet de la pile logicielle d'Android. Elles comprennent à la fois les applications natives fournies avec l'implémentation particulière d'Android (par exemple le navigateur web et les applications de messagerie), les applications apportées par le constructeur, les applications pré-installées, les applications fournies par l'opérateur et les applications tierces installées par l'utilisateur après l'achat de l'appareil. La couche applicative est l'une des plus importantes car c'est celle à laquelle l'utilisateur est directement confronté. On distingue deux catégories d'applications sur Android dont nous détaillerons la composition ci-dessous.

#### Applications système

Dans un premier temps, Android dispose d'applications dites "système" qui ne peuvent être désinstallées d'un appareil (sauf si l'on dispose d'un accès superutilisateur[20] sur ce dernier). On trouve de très nombreuses applications dans ce cas de figure : 
- **Applications de base d'Android** - La version "pure" d'Android, c'est à dire celle de base fournie par Google contient de nombreuses applications comme un dialer afin de composer un numéro, un calendrier, une application pour gérer les caméras embarquées au sein de l'appareil ou encore une application pour gérer ses emails, etc... On peut distinguer deux types d'applications fournies avec Android : celle dont le code source est accessible[19] et celle dont le code source est protégé (Exemples : Google Maps, Gmail, Google photos).
- **Applications constructeurs** - De nombreux constructeurs fournissent leurs propres applications équivalentes à celle proposées par Google et c'est la raison pour laquelle on se retrouve avec des applications doublon sur un smartphone.
- **Applications opérateurs** - Si le smartphone a été acheté chez un opérateur, il sera accompagné d'applications installées par ce dernier permettant de suivre sa consommation de données, d'accéder à certains services, etc... (ex : les applications *Orange et moi* ou *Cloud Orange*)

#### Applications désinstallables

Ces applications ont toutes un point commun : elles peuvent être désinstallées de l'appareil quels que soit les droits dont dispose l'utilisateur. Elles proviennent de diverses sources :
- **Applications pré-installées** - Certains constructeurs réalisent des partenariats avec des marques et disposent ainsi d'applications comme le pack Office ou divers jeux pré-installés sur leurs appareils.
- **Applications tierces** - Il s'agit de l'ensemble des applications que l'utilisateur va pouvoir installer en plus de celles déjà présentes sur l'appareil. Le Google Play Store est généralement le lieu de prédilection pour installer de nouvelles applications Android, mais ce n'est pas le seul ! Bien que Google n'autorise pas le téléchargement d'applications en dehors du Google Play Store lui-même, il est tout de même possible de les obtenir **en autorisant les applications provenant de sources inconnues**. On pourra ainsi utiliser un store d'applications alternatif comme F-Droid[21]. Il s'agit un magasin d'applications financé par des dons et dont les applications sont toutes Open Source et gratuites. Également, on peut récupérer le fichier *.apk* d'une application pour l'installer sans passer par un magasin d'applications. En effet, il existe des sites web comme *apkmirror.com* qui constituent une bibliothèque rencensant de très nombreuses applications téléchargeables au format *.apk*.

## 3) Système de fichiers et points de montage

### Qu'est-ce qu'un système de fichiers ?

Dans notre cas, le terme *système de fichiers* désigne l'organisation hiérarchique des fichiers au sein d'un système d'exploitation[22]. De façon générale, un système de fichiers est une façon de stocker les informations et de les organiser dans des fichiers sur ce que l'on appelle des mémoires secondaires (pour un smartphone, il s'agira d'une mémoire eMMC[23], UFS[24] ou d'une carte SD). Une telle gestion des fichiers permet de traiter et de conserver des quantités importantes de données ainsi que de les partager entre plusieurs programmes informatiques. Il offre à l'utilisateur une vue abstraite sur ses données et permet de les localiser à partir d'un chemin d'accès.

### Qu'est-ce qu'un point de montage ?

Un point de montage est un répertoire (dossier) à partir duquel sont accessibles les données se trouvant sous forme d'un système de fichiers sur une partition[25] d'un support de stockage.
Dans un système Windows, les périphériques de stockage de données et les partitions sont affichés comme des disques indépendants situés au sommet de l'arborescence du système. Sous Unix[49], en revanche, ils sont inclus dans l'arborescence car Unix traite aussi les partitions et périphériques de stockage comme des fichiers.

### Structure du système de fichiers d'Android

Android utilise plusieurs partitions pour organiser les fichiers et dossiers. On retrouve principalement 11 points de montage sur un appareil Android dont on donnera la liste ci-dessous. On pourra noter toutefois qu'il peut y avoir des points de montage supplémentaires différant d'un modèle à l'autre. En outre, les 11 partitions ci-dessous peuvent être trouvées sur n'importe quel appareil Android : 

Schéma des différentes partitions sur Android (à refaire)

S'ajoute à ces partitions celle d'un éventuel support de stockage supplémentaire comme une carte SD ce qui nous donne ceci :

- **/boot**
- **/system**
- **/recovery**
- **/data**
- **/storage**
- **/cache**
- **/sys**
- **/proc**
- **/sbin**
- **/root**
- **/dev**
- **/sdcard** ou **/sd-ext** selon les appareil

### Détail des points de montage sur Android

- #### /boot
C'est la partition de démarrage d'un appareil Android sans laquelle le système est incapable de démarrer. Elle comprend le noyau Linux utilisé par Android ainsi que sa version compressée (*vmlinuz*). On trouve également un fichier nommé *initrd* qui contient les modules essentiels au bon fonctionnement du noyau (les pilotes réseau, de l'écran, du disque, etc...) ainsi qu'un fichier *ramdisk.img*. Il s'agit d'un disque virtuel, c’est à dire un élément considéré comme un disque de stockage par Android mais qui n’en est pas un. En réalité, ce "disque" est composé d'une partie de la mémoire vive de l'appareil afin d'obtenir un démarrage le plus rapide possible. Il contient notamment le répertoire principal d'Android.

- #### /system
Cette partition contient le répertoire principal d'Android. Cela inclut l'ensemble des bibliothèques et paquets natifs du framework d'Android comme l'interface graphique[28] et toutes les applications AOSP préinstallées sur l'appareil. Au démarrage, cette partition est montée en lecture seule à partir d'un morceaudu fichier *ramdisk.img*. L'effacement de cette partition supprimera Android de l'appareil mais ce dernier pourra tout de même démarrer en mode recovery pour installer un nouveau système.

- #### /recovery
La partition de restauration est spécialement conçue pour la sauvegarde. Elle peut être considérée comme une partition de démarrage alternative, permettant d'effectuer des opérations de récupération et de maintenance avancées. Sur certains smartphone, après plusieurs tentatives de démarrage échouée, la procédure de démarrage va basculer sur un second fichier *ramdisk.img* qui est propre au mode recovery. C'est à partir de ce fichier que la partition /recovery va être montée.

- #### /data
Il s'agit de la partition de données utilisateur. Elle contient les données de l'utilisateur comme les contacts, sms, paramètres et toutes les applications Android installées par l'utilisateur. Lorsque l'on effectue une réinitialisation de l'appareil, c'est cette partition est effacée.

- #### /storage
Cette partition contient également des données utilisateur comme les photos, vidéos, musiques et documents présents sur votre appareil. Tout comme /home/nom_de_l'utilisateur sous Unix, cette partition gèrent plusieurs utilisateurs sous cette forme : /storage/emulated/numéro_utilisateur (0 par défaut).

- #### /cache
La partition de *cache* est celle où Android stocke les données et les composants d'applications fréquemment utilisés afin d'y accéder plus rapidement. L'effacement du cache n'affecte pas les données personnelles mais élimine simplement les données qui s'y trouvent. Elles se remplira à nouveau en utilisant l'appareil.

#### Les partitions héritées des systèmes Unix

Parmi les points de montage d'Android, on retrouve bon nombre d'éléments des systèmes Unix (répertoires /sys, /proc, /dev, /sbin, /root). D'autres, quant à eux, ont été déplacés dans la partition /system. Par exemple /etc est devenu /system/etc. C'est aussi le cas de /bin, /usr, /lib.

- #### /sys
Ce répertoire contient des informations provenant directement du noyau en grande partie sur les périphériques et drivers. Il possède son propre système de fichiers : *sysfs*  

- #### /proc
Contient des informations fournies par le noyau sur l'état d'exécution du sytème (quantité de mémoire système, périphériques montés, configurations matérielles, etc...). Il possède son propre système de fichiers : *procfs*

- #### /sbin
On peut y trouver un ensemble d'outils d'administration du système ne pouvant être utilisés que par un superutilisateur.

- #### /root
Il s'agit du répertoire personnel de l'utilisateur root. Ce dernier est vide par défaut car Android ne laisse pas facilement la possibilité à un utilisateur de disposer des droits d'administrations sur le système (contrairement à la grande majorité des systèmes Unix et à Windows).

- #### /dev
Ce répertoire rassemble l'ensemble des fichiers spécifiques aux périphériques embarqués et branchés à l'appareil. Ils sont créés lors de l'installation du système et avec l'exécution du script */dev/MAKEDEV*. Ce répertoire permet d'établir un lien entre le système et un périphérique via une interface.

- #### /sdcard
Elle ne fait pas partie de la mémoire interne de l'appareil. Il s'agit de l'espace de stockage d'une carte SD que l'utilisateur peut utiliser de la manière qu'il souhaite. On peut y stocker documents, photos, vidéos, données des applications, etc... L'effacer est parfaitement sûr, à condition d'avoir préalablement sauvegarder les données qui y étaient présentes. Si certaines applications envoyaient leurs données sur cet espace de stockage, elles seront perdues.

- #### /sd-ext
Ce n'est pas une partition Android standard, mais elle apparaît à l'utilisation de systèmes d'exploitation alternatifs comme LineageOS. Il s'agit en fait d'une partition **/data** supplémentaire sur la carte SD permettant d'augmenter l'espace de stockage pour l'utilisateur sur des appareils ayant peu de mémoire interne allouée à la partition /data.

### Type de système de fichiers

Il existe de nombreux système de fichiers qui peuvent être utilisés selon diverses carcatéristiques telles que le système d'exploitation ou la taille maximale des fichiers pouvant être stocké par exemple. Dans le cas d'Android, de nombreux systèmes de fichiers peuvent être utilisé du fait que le système repose sur le noyau Linux. De plus, certains fabricants ont adopté leur propre système de fichiers sur leurs appareils à l'image de Samsung qui utilise F2FS[29] sur certains de ses modèles.

Voici la liste non exaustive des systèmes de fichiers pouvant être utilisés sous Android pour la mémoire interne :
- **EXT2/EXT3/EXT4** : Ext signifie EXTended file systems. Ce sont les standards de système de fichiers utilisés sur Linux. Le dernier en date est l'EXT4[30] qui succède à JFFS2 et YAFFS à partir de la version 2.3.
- Créé par Microsoft pour les dispositifs à mémoire flash[31], le système de fichiers **exFAT** *(table d'allocation de fichiers étendue en français)* ne fait pas partie du noyau Linux standard. Cependant, il fournit un support pour les appareils Android dans certains cas.

Concernant les dispositif de stockage amovibles (carte SD notamment), il existe également une liste de systèmes de fichiers compatibles : 
- **EXT2/EXT3/EXT4** On utilise là aussi l'EXT4
- **VFAT** (Virtual FAT[32]) qui est très souvent utilisé sur les cartes SD

## 4) Processus de démarrage d'Android

### a) Introduction

En informatique, le démarrage consiste à mettre en marche un appareil informatique (dans notre cas, un smartphone) jusqu'à ce qu'il puisse être utilisé. Il peut être lancé par un matériel tel qu'une pression sur un bouton, ou par une commande logicielle. Après la mise sous tension, un appareil est relativement limité en terme d'action et ne peut lire qu'une partie de sa mémoire appelée mémoire morte[33]. Un petit programme appelé "firmware" (*micrologiciel* en français) y est stocké. Il permet d'accéder à d'autres types de mémoire, comme la mémoire interne et la carte SD. Ce micrologiciel est capable de charger des programmes dans la mémoire interne du smartphone et de les exécuter. Un gestionnaire de démarrage peut également être exécuté en option notamment pour des opérations de maintenance et de récupérarion.
Le processus de démarrage d'un smartphone Android se déroule en 5 étapes que nous détaillerons dans chacune des sous parties ci-dessous.

Schéma du processus de démarrage d'Android [34]

### b) Boot ROM et Bootloader

Lors de la mise sous tension d'un appareil, un premier code du nom de *"Boot ROM"* directement intégré au sein du processeur[35] va être lancé. Le code qu'il contient a pour but de lancer un second code nommé *"bootloader"* (ou *"chargeur d'amorçage"* en français) dans la mémoire vive de l'appareil. 

Le chargeur d'amorçage est un morceau de code dont l'objectif principal est de charger un système d'exploitation, de mettre en place un environnement minimal dans lequel ce système d'exploitation peut fonctionner et de lancer le processus de démarrage. 

Une des tâches principales du chargeur d'amorçage consiste à mettre en place la gestion de la mémoire et les options de sécurité de l'appareil. Ces éléments sont essentiels avant de lancer le noyau Linux. Le bootloader contient deux fichiers importants : *init.s* et *main.c*. Le code qu'ils contiennent va se charger d'initialiser les matériels embarqués tels que le clavier, l'horloge système, etc.

Plus important encore, le chargeur d'amorçage vérifie l'intégrité des partitions de démarrage et de récupération (respectivement *boot* et *recovery* vues dans la partie III) avant de passer au lancement du noyau Linux. En effet, si la partition *boot* est endommagée, l'appareil ne procèdera pas au démarrage.

### c) Noyau Linux

Avant de démarrer les programmes et applications de l'espace utilisateur qui composent Android, le noyau Linux effectue la majeure partie de l'initialisation du matériel, des pilotes[36] et du système de fichiers.
Les opérations suivantes sont réalisées dans l'ordre : 
- Initialisation du **noyau Linux** (les zones de mémoire et d'Entrées/Sorties sont initialisées ainsi que la table des processus recensant l'ensemble des processus)
- Initialisation des **pilotes**[36]
- le système de fichier /root du superutilisateur est monté[37]
- Le premier processus **init** est lancé

Schéma lancement init[38]

### d) Init

Le processus **init** est un élément clé de la séquence de démarrage d'Android, il est chargé de monter les répertoires systèmes tel que **/sys**, **/dev** ou encore **/proc** et d'initialiser les principaux éléments du système Android en exécutant les commandes de deux fichiers :
- **init.rc**, un fichier générique, commun à tous les appareils Android
- **init.<nom_de_la_machine>.rc** un fichier spécifique à l'appareil (exemple : init.starlte.rc pour un Samsung Galaxy S9).

Dans ces fichiers, nous pouvons trouver des commandes qui sont responsables du lancement de processus appelés **daemons**. Il s'agit de processus s'exécutant en arrière plan plutôt que sous le contrôle direct d'un utilisateur. Parmi eux se trouve notamment :

- adbd (Android Debug Bridge Deamon) - Permet d'exécuter des commandes[39] sur son smartphone
- debuggerd (Debugger Deamon) - Chargé de gérer les demandes de processus liés au plantage[40] d'une application
- rild (Radio Interface Layer Deamon) - permet à l'appareil de dialoguer avec le matériel radio embarqué (utilisé par les applications ayant besoin du réseau cellulaire. Exemple : Appels, SMS/MMS)

### e) Zygote et ART

Après avoir démarré l'ensemble des *deamons*, le processus *init* va lancer un processus nommé **Zygote**. Il s'agit d'une **machine virtuelle ART** (Android Runtime pour rappel) contenant l'ensemble des ressources du framework d'Android (Bibliothèques C/C++ et framework Java 8). Ce processus se met en veille lorsque tous les éléments qu'il contient sont pré-chargés.

Lorsqu'une application va être lancée par le système, le processus Zygote va se réveiller et lui fournir tous les éléments dont elle a besoin avant de se remettre en veille. Une machine virtuelle ART va ainsi être créée avec l'ensemble des éléments nécessaires (hérités de Zygote) à son bon fonctionnement. Chacune des demandes de l'application va se traduire par un processus afin de charger le plus d'éléments simultanées possible. C'est grâce à ce processus de création des applications que ces dernières peuvent démarrer très rapidement sur Android.

A ce stade, on observe à l'écran l'animation de démarrage (logo de Google ou du fabriquant de l'appareil) et les processus lancés sont les suivants :

Schéma deamons + Zygote [41]

### f) Service Manager et System Server

Suite au lancement de Zygote, le processus *init* va désormais lancer le processus **Runtime** qui va à son tour lancer le processus **Service Manager** (ou *Gestionnaire de services* en français) qui gère l'enregistrement et la consultation des services comme le DNS[42]. *Runtime* va définir *Service Manager* comme gestionnaire de contexte par défaut pour les services ce qui nous donne ceci :

Schéma daemons + Zygote + Service Manager [43]

Ensuite, Zygote va créer une nouvelle VM ART et y démarrer le **System Server**. Ce dernier va initialiser les services système suivant : 

- Power Manager - Gestionnaire d'alimentation
- Activity Manager - Gestionnaire d'activité
- Telephony Registry - Registre téléphonique
- Package Manager - Gestionnaire de paquets[44]
- Battery Service - Service de batterie
- Lights Service - Service de luminostité
- Vibrator Service - Service de vibration
- Alarm Manager - Gestionnaire d'alarme
- Window Manager - Gestionnaire de fenêtre
- Bluetooth Service - Service du Bluetooth
- Location Manager - Service de localisation
- etc...

L'ensemble de ces services vont être enregistrés auprès du *Service Manager* :

Schéma daemons + Zygote + Service Manager + Services + System Server [45]

A partir de ce moment, il ne reste plus qu'une étape : démarrer le **Lanceur d'applications** qui va nous permettre d'exécuter d'autres applications comme son nom l'indique. Pour cela, Zygote va lancer une nouvelle machine virtuelle ART contenant notre application ***Home***. A compter de cet instant **notre système est prêt** et on peut le représenter de cette manière :

Schéma daemons + Zygote + Service Manager + Services + System Server + App Launcher [46]
Ecran d'acceuil smartphone (Android 10) [47]

### g) Lancement d'une application quelconque

Lorsque l'utilisateur va appuyer sur l'icone de l'application qu'il souhaite lancer : 
1) Le lanceur d'applicaiton va envoyer l'information vers les divers services dont cette dernière a besoin (service bluetooth, service de localisation, etc...).
2) Le gestionnaire de service va faire appel aux gestionnaire de paquets, gestionnaire d'activité et gestionnaire de fenêtres pour envoyer une requête à Zygote
3) et 4. L'application va démarrer dans une machine virtuelle ART à l'aide de Zygote :

Schéma daemons + Zygote + Service Manager + Services + System Server + App Launcher + Application quelconque [48]

## 5) Lexique + Images
- [1] Parts de marché d'Android en 2019 :
https://mobilemarketing.fr/2019/04/30/android-sapproche-des-80-de-parts-de-marche/
- [2] https://fr.wikipedia.org/wiki/Noyau_Linux
- [3] https://developer.android.com/guide/platform/images/android-stack_2x.png
- [4] https://fr.wikipedia.org/wiki/Module_(programmation)
- [5] https://fr.wikipedia.org/wiki/Biblioth%C3%A8que_logicielle
- [6] https://fr.wikipedia.org/wiki/Interface_de_programmation
- [7] https://fr.wikipedia.org/wiki/Framework
- [8] https://fr.wikipedia.org/wiki/M%C3%A9moire_vive
- [9] https://fr.wikipedia.org/wiki/Machine_virtuelle
- [10] https://user.oc-static.com/files/322001_323000/322271.png
- [11] https://fr.wikipedia.org/wiki/Processus_(informatique)
- [12] https://en.wikipedia.org/wiki/Machine_code
- [13] https://fr.wikipedia.org/wiki/Base_de_donn%C3%A9es
- [14] https://en.wikipedia.org/wiki/Canvas_(GUI)
- [15] https://en.wikipedia.org/wiki/Class_(computer_programming)
- [16] https://fr.wikipedia.org/wiki/Extensible_Markup_Language
- [17] https://en.wikipedia.org/wiki/Transport_Layer_Security
- [18] https://en.wikipedia.org/wiki/C_standard_library
- [19] Liste des applications Open Source fournies par Google sur Android :
https://android.googlesource.com/platform/packages/apps
- [20] https://en.wikipedia.org/wiki/Superuser
- [21] https://f-droid.org/fr/
- [22] https://en.wikipedia.org/wiki/Operating_system
- [23] https://en.wikipedia.org/wiki/MultiMediaCard
- [24] https://en.wikipedia.org/wiki/Universal_Flash_Storage
- [25] https://fr.wikipedia.org/wiki/Partition_(informatique)
- [26] https://techblogon.com/wp-content/uploads/2019/04/partition-size-in-android-device1.jpg
- [27] https://overclocking.com/quest-ce-quun-ramdisk/
- [28] https://en.wikipedia.org/wiki/Graphical_user_interface
- [29] https://en.wikipedia.org/wiki/F2FS
- [30] https://en.wikipedia.org/wiki/Ext4
- [31] https://fr.wikipedia.org/wiki/M%C3%A9moire_flash
- [32] https://fr.wikipedia.org/wiki/Virtual_FAT
- [33] https://fr.wikipedia.org/wiki/M%C3%A9moire_morte
- [34] https://miro.medium.com/max/866/0\*4zrPhMmFvSwkfJcg.png
- [35] https://fr.wikipedia.org/wiki/Processeur
- [36] https://fr.wikipedia.org/wiki/Pilote_informatique
- [37] Lorsque l'on *"monte"* un répertoire, le système d'exploitation peut alors accéder au contenu du système de fichiers qui lui est associé.
- [38] https://miro.medium.com/max/1134/1*\_HGgPepdyE5kpStEGdbN5w.png
- [39] https://fr.wikipedia.org/wiki/Commande_informatique
- [40] https://fr.wikipedia.org/wiki/Plantage
- [41] https://miro.medium.com/max/1400/1*\orUG4TqFnTJ0uSIFycJ2vA.png
- [42] https://fr.wikipedia.org/wiki/Domain_Name_System
- [43] https://miro.medium.com/max/882/1*\HiTZMUbRRHxdCnwN4i-xww.png
- [44] https://fr.wikipedia.org/wiki/Paquet_(logiciel)
- [45] https://miro.medium.com/max/1234/1\*b_RGj4GGf8HrIteP6BxIow.png
- [46] https://miro.medium.com/max/1214/1*\OuWPRO_hIc60mLnFRlhnPA.png
- [47] https://upload.wikimedia.org/wikipedia/commons/thumb/8/8a/Android_Q_Beta6_screenshot.png/250px-Android_Q_Beta6_screenshot.png
- [48] https://miro.medium.com/max/1400/1\*DNmreF9wbTyxnLJFp4djOw.png
- [49] https://fr.wikipedia.org/wiki/Unix
