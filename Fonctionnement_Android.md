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


[1] Parts de marché d'Android en 2019 :
https://mobilemarketing.fr/2019/04/30/android-sapproche-des-80-de-parts-de-marche/<br/>
[2] Le noyau est le cœur du système, c'est lui qui s'occupe de fournir aux logiciels une interface de programmation pour utiliser le matériel d'une machine.<br/>
[3] https://developer.android.com/guide/platform/images/android-stack_2x.png<br/>
[4] https://fr.wikipedia.org/wiki/Module_(programmation)<br/>
[5] https://fr.wikipedia.org/wiki/Biblioth%C3%A8que_logicielle<br/>
[6] https://fr.wikipedia.org/wiki/Interface_de_programmation<br/>
[7] https://fr.wikipedia.org/wiki/Framework<br/>
