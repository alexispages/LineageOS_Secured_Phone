# Fonctionnement d'Android

## I) Présentation d'Android

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

## II) L'architecture d'Android

Android est constitué d'une pile de composants. Le sens de lecture s'effectue de bas en haut. Nous allons analyser par la suite l'ensemble des couches composant le système Android[3].

### a) Le Noyau Linux

Il s'agit de la couche gérant le matériel de l'appareil mobile (écran, caméra, support de stockage, etc...). C'est elle qui va permettre aux logiciels embarqués dans l'appareil d'accéder à ces composants. La version utilisée par Android a été élaborée spécialement pour un environnement mobile en se focalisant sur des aspects tels que la gestion énergétique (batterie) et de la mémoire. En résumé, c'est cette couche qui permet à Android d'être compatible avec un très grand nombre d'appareils aux configurations matérielles très différentes.

### b) Couche d'abstraction matérielle ou Hardware Abstraction Layer (HAL)

Cette couche se compose de plusieurs modules[4] d'une bibliothèque logicielle[5], chacun d'entre eux étant lié à un type spécifique de matériel comme la caméra ou le module bluetooth. Ainsi, lorsqu'une API[6] du framework[7] Java va demander à accéder au matériel de notre appareil, Android chargera le module correspondant au composant à utiliser. C'est cette couche qui permet à une application de s'adpater au matériel embarqué dans un appareil. 

En réalité, le noyau Linux fournit déjà une compatibilité avec le matériel embarqué. L'objectif pour Google en ayant rajouté cette couche est de "sécuriser" le système en rendant privé le code source permettant d'exploiter le matériel d'un appareil. Cette solution permet notamment à Android de s'affranchir de la license open source imposé par l'utilisation du noyau Linux. Ce dernier constituait déjà une HAL et à longtemps été utilisé sans cette couche supplémentaire mais la volonté de Google est désormais d'éviter au maximum son utilisation.

### c) Le moteur d'exécution d'Android

Il s'agit d'un élément crutial du système car c'est ce dernier qui va permettre d'exécuter des applications basée sur le langage de programmation Java et certains services système d'Android. Ce moteur d'exécution se divise en deux parties : un environnement d'exécution des applications, et des bibliothèques de base (Core libraries) sur lesquelles nous reviendrons dans un second temps.

#### *L'environnement d'exécution*

Afin d'exécuter des applications en Java, il existe un outil qui se nomme *Java Runtime Environment* (ou Envrionnement d'exécution Java en français). En outre, ce dernier n'est pas adapté à un environnement mobile et possède de nombreuses fonctionnalités inadaptées. L'enjeu majeur lors du développement d'Android a donc été de développer un environnement d'exécution optimisé pour mieux gérer les ressources physiques du système. L'objectif était de laisser moins d'empreinte mémoire[8] (la quantité de mémoire allouée à une application pendant son exécution) ou d'utiliser moins de batterie.

C'est ainsi qu'est née la machine virtuelle[9] Dalvik, spécialement développée pour les systèmes embarqués.

Schéma du fonctionnement de Dalvik [10]

Le schéma ci-dessus explique le processus de construction d'une application avec Dalvik. Dans un premier temps, le développeur va produire un fichier *.java* contenant une suited'instructions dans le langage de programmation Java. Ce fichier va ensuite être traduit dans un second langage que l'on appelle *bytecode* qui sera contenu à son tour dans un fichier *.class*. On pourra par la suite regrouper différents fichiers *.class* en un fichier *.jar* qui sera exécutable dans l'environement d'exécution Java. Or, la machine virtuelle Dalvik possède son propre bytecode. Il est donc nécessaire de convertir le *bytecode Java* en *bytecode Dalvik* (création d'un fichier *.dex*) afin de pouvoir exécuter une application sur Android.

L'avantage majeur de Dalvik réside dans la gestion des processus[11]. L'objectif va être d'isoler chacun des processus les uns par rapport aux autres en associant un processus à une machine virtuelle. Par ce biais, si un processus dysfonctionne, les autres ne vont pas être impactés. Ainsi, chaque processus est protégé des autres ce qui renforce la protection du système.

À partir de la version 5.0 d'Android (sortie en 2014), Dalvik a été remplacée par l'*Android Runtime* (ART) qui permet de transcrire le *bytecode java* directement en langage machine[12]. Les gains apportés en performance et en autonomie des batteries sont conséquents avec une augmentation de 20 à 30%. En contre-partie, la taille des applications augmente de 20%.

Il ne manque plus qu'une étape avant d'exécuter une application : le manifest. Ce dernier contient diverses informations sur l'application notamment les autorisations dont l'application a besoin pour accéder à des parties protégées du système (accès au stockage, à la caméra, à la géolocalisation etc...) ou à d'autres applications. Il déclare également les autorisations que les autres applications doivent avoir pour accéder au contenu de cette application. Il recense également les fonctionnalités matérielles et logicielles requises par l'application, ce qui affecte les appareils pouvant installer l'application à partir de Google Play. Par exemple, si votre appareil dispose d'une version trop ancienne d'Android, il ne pourra pas installer certaines applications.

En ajoutant ce manifest au langage machine obtenu lors de la dernière étape du processus de construction d'une application, l'environnement d'exécution d'Android (ART) va ainsi pouvoir exécuter notre application qui sera désormais au format *.apk*.

#### *Les "Bibliothèques de base" (Core Libraries)*

Les *Core Libraries* d'Android sont constituées d'une copie des *Core Librairies* de Java 8 (les versions postérieures n'étant pas supportées par Android) et d'un ensemble de bibliothèques basée sur Java spécifiques au développement d'Android. Voici les principales biliothèques de base que l'on peut trouver dans cet ensemble :
- **android.app** - Fournit un accès au modèle d'application et constitue la pierre angulaire de toutes les applications Android.
- **android.content** - Facilite l'accès au contenu, la publication et la communication entre les applications et les composants d'application.
- **android.database** - Utilisé pour accéder aux données publiées par les fournisseurs de contenu et comprend des classes de gestion de base de données[13] *SQLite*.
- **android.graphics** - API de dessin graphique en 2D comprenant des couleurs, des points, des filtres, des rectangles et des canvas[14].
- **android.hardware** - API permettant d'accéder à du matériel tel que l'accéléromètre et le capteur de lumière.
- **android.opengl** - Interface Java pour piloter l'API de rendu graphique en 3D *OpenGL ES*.
- **android.os** - Fournit aux applications l'accès aux services standard du système d'exploitation, notamment les messages, les services système et la communication entre les processus.
- **android.media** - Fournit des classes[15] pour permettre la lecture de fichiers audio et vidéo.
- **android.net** - Un ensemble d'API donnant accès à la partie réseau. Comprend android.net.wifi, qui permet d'accéder à la partie réseau sans fil de l'appareil.
- **android.print** - Comprend un ensemble de classes qui permettent d'envoyer du contenu à des imprimantes configurées à partir d'applications Android.
-  **android.provider** - Un ensemble de classes qui permettent d'accéder aux bases de données standard des fournisseurs de contenu Android notamment celles gérées par les applications de calendrier et de contact.
-  **android.text** - Utilisé pour présenter et manipuler du texte sur l'écran d'un appareil.
-  **android.util** - Ensemble de classes d'utilitaires permettant d'effectuer des tâches telles que la conversion de chaînes de caractères ou de nombres, le traitement XML[16] et la manipulation de la date et de l'heure.
- **android.view** - Fournit les éléments de base des interfaces utilisateur des applications.
-  **android.widget** - Un ensemble de composants d'interface utilisateur pré-construits tels que des boutons, des étiquettes, des listes, des gestionnaires de mise en page, des boutons radio, etc...
- **android.webkit** - Un ensemble de classes destinées à permettre l'intégration de fonctions de navigation sur le web dans les applications.

### d) Bibliothèques C/C++

Les bibliothèques de base d'Android que nous venons de décrire dans la partie précédente sont basées sur Java et fournissent les API principales pour les développeurs qui écrivent des applications Android. Il est important de noter que les bibliothèques de base n'effectuent pas une grande partie du travail réel et constituent, en réalité essentiellement un élément central écrit en Java autour duquel s'inscrit un ensemble de bibliothèques basées sur les langages de programmation C et C++. Lorsque l'on fait appel, par exemple, à la bibliothèque android.opengl pour afficher des graphismes en 3D sur l'écran de l'appareil, la bibliothèque fait en fait appel à la bibliothèque C++ OpenGL ES qui, à son tour, travaille avec les couches sous-jacentes (HAL et noyau Linux) pour effectuer les tâches d'affichage.

Les bibliothèques C/C++ sont incluses pour remplir un large éventail de fonctions diverses, notamment l'affichage graphique en 2D et 3D, la communication TLS/SSL[17], la gestion de bases de données SQLite, la lecture audio et vidéo, le rendu de polices d'écriture bitmap et vectorielles, la gestion des sous-systèmes d'affichage et des couches graphiques et une implémentation de la bibliothèque système C standard (libc)[18].

En pratique, le développeur d'applications Android typique accédera à ces bibliothèques uniquement par le biais des API de la bibliothèque centrale d'Android basée sur Java. Si un accès direct à ces bibliothèques est nécessaire, il peut être réalisé en utilisant l'Android Native Development Kit (NDK) dont le but est d'appeler les méthodes natives des langages de programmation non Java ou Kotlin (tels que C et C++) à partir du code Java en utilisant l'interface native Java (JNI).

### e) Framework API Java

Le cadre d'application (*framework* en anglais) est un ensemble de services qui forment collectivement l'environnement dans lequel les applications Android fonctionnent et sont gérées. Ce cadre met en œuvre le concept selon lequel les applications Android sont construites à partir de composants réutilisables, interchangeables et remplaçables. Ce concept est poussé plus loin en ce sens qu'une application est également capable de publier ses capacités ainsi que toutes les données correspondantes afin qu'elles puissent être trouvées et réutilisées par d'autres applications.

#### Qu'est-ce qu'un service ?

Un service est un composant d'application qui peut effectuer des opérations de longue durée en arrière-plan, et il ne fournit pas d'interface utilisateur. Un autre composant d'application peut démarrer un service, et il continue à fonctionner en arrière-plan même si l'utilisateur passe à une autre application. Un service peut traiter des transactions réseau, jouer de la musique, effectuer des déplacements de fichiers ou interagir avec un fournisseur de contenu, le tout en arrière-plan. Les services système jouent un rôle clé en exposant les fonctions de bas niveau du matériel et du noyau Linux aux applications de haut niveau. Les services système sont actifs du démarrage au redémarrage, c'est-à-dire pendant toute la durée de vie du système.

Il existe 3 types de services :

- **Premier plan** - Un service de premier plan effectue une opération qui est perceptible par l'utilisateur. Par exemple, une application audio utiliserait un service d'avant-plan pour lire une piste audio. Les services d'avant-plan doivent afficher une notification. Les services d'avant-plan continuent de fonctionner même lorsque l'utilisateur n'interagit pas avec l'application.
- **Arrière-plan** - Un service d'arrière-plan effectue une opération qui n'est pas directement remarquée par l'utilisateur. Par exemple, si une application utilise un service pour compacter son stockage, il s'agit généralement d'un service d'arrière-plan.
- **Relié** - Un service est lié lorsqu'un composant d'application se lie à lui en appelant la fonction bindService(). Un service lié offre une interface client-serveur qui permet aux composants d'interagir avec le service, d'envoyer des demandes et de recevoir des résultats. Un service lié ne fonctionne que tant qu'un autre composant de l'application lui est lié. Plusieurs composants peuvent se lier au service en même temps, mais lorsque tous se délient, le service est détruit.

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

Les applications sont situées au sommet de la pile logicielle d'Android. Elles comprennent à la fois les applications natives fournies avec l'implémentation particulière d'Android (par exemple le navigateur web et les applications de messagerie), les applications apportées par le constructeur, les applications pré-installées, les applications fournies par l'opérateur et les applications tierces installées par l'utilisateur après l'achat de l'appareil. Au-delà de l'ensemble des couches que nous avons vu précédemment, c'est de loin celle des applications qui demeure la plus importante car c'est celle à laquelle l'utilisateur est directement confronté.

#### Applications système

La version "pure" d'Android, c'est à dire celle de base fournie par Google contient ainsi de nombreuses applications comme un dialer afin de composer un numéro, un calendrier, une application pour gérer les caméras embarquées au sein de l'appareil ou encore une application pour gérer ses emails, etc...
On peut distinguer deux types d'applications fournies avec Android : celle dont le code source est accessible[19] et celle dont le code source est protégé (Exemples : Google Maps, Gmail, Google photos). Toutes ces applications ne peuvent être désinstallées d'un appareil tant que l'on ne dispose pas d'un accès superutilisateur[20].

#### Applications constructeurs

Certains constructeurs, comme Samsung, fournissent leur propre application pour la lecture de musique ou d'agenda et c'est la raison pour laquelle on se retrouve avec des applications doublon sur un smartphone. 

#### Applications pré-installées

Également, certains constructeurs réalisent des partenariats avec des marques et disposent ainsi d'applications comme le pack Office pré-installées sur leurs appareils. Cela peut être gênant si de très nombreuses applications sont pré-installées comme des jeux à titre d'exemple. Néanmois, on pourra désinstaller l'ensemble de ces applications sans problèmes.

#### Applications opérateur

Si le smartphone a été acheté chez un opérateur, il sera accompagné d'applications installées par ce dernier permettant de suivre sa consommation de données, de gérer certaines fonctionnalités de sa box, etc...

#### Applications tierces

Il s'agit de l'ensemble des applications que l'utilisateur va pouvoir installer en plus de celles déjà présentes sur l'appareil. Le Google Play Store est généralement le lieu de prédilection pour installer de nouvelles applications Android, mais ce n'est pas le seul ! Bien que Google n'autorise pas le téléchargement d'autres magasins d'applications à partir du Google Play Store lui-même, il est tout de même possible de les obtenir en autorisant les applications provenant de sources inconnues. On peut tout à fait utiliser un store d'applications alternatif comme F-Droid[21], un magasin d'applications financés par des dons et dont les applications sont toutes Open Source et gratuites.

## Lexique + Images
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
