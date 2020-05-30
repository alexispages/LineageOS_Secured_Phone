# II) Installation de LineageOS

Dans cette partie, nous allons procéder à l'installation d'un sytème d'exploitation alternatif à Android nommé ***LineageOS***. L'ensemble des opérations vont être réalisées sur un *BQ Aquaris M5* fonctionnant sur la version "pure" d'Android 7.0.0.

## 1) Qu'est-ce que LineageOS ?

*LineageOS* est un système d'exploitation libre et gratuit disponible sur smartphones et tablettes basé sur l'Android Open Source Project (AOSP). Il succède à *CyanogenMod* lorsque *Cyanogen Inc*. a annoncé qu'elle arrêtait le développement et fermait l'infrastructure à l'origine du projet. Comme *Cyanogen Inc.* a conservé les droits sur le nom de Cyanogen, le projet a été rebaptisé *LineageOS*.

Logo LineageOS [1]

*LineageOS* a été officiellement lancé le 24 décembre 2016 et son code source a été rendu disponible à la fois sur *GitHub*[2] et *GitLab*[3]. Comme pour toutes les versions d'Android, les versions de ce système d'exploitation sont spécifiques à un seul modèle d'appareil. Depuis son lancement, les différentes version de *LineageOS* sont disponibles pour 109 modèles de smartphones avec plus de 1,7 million d'installations actives en 2017.

*LineageOS* permet à la communauté de s'impliquer dans le développement de différentes manières via :
- Un wiki[4] contenant des informations concernant l'installation, le support et le développement de LineageOS.
- Une plateforme pour la gestion des traductions
- Un Gitlab Issues pour le suivi des bogues[5]
- Une page de statistiques, qui permet d'afficher le nombre d'installations actives des utilisateurs qui choisissent de rapporter ces statistiques.
- Deux plateformes d'échanges pour les utilisateurs avec un canal de discussion Reddit officiel (*r/lineageos*) et deux canaux sur Freenode *#lineageos* et *#lineageos-dev*).
- Des forums *XDA-developpers* ont aussi été utilisés par les membres de la communauté Lineage depuis le premier lancement du logiciel. De nombreux appareils n'étant pas pris en charge par les versions officielles, les membres de la communauté développent donc leurs propres versions non officielles qui permettent à de nombreux modèles d'utiliser Lineage. Ces versions non-officielles sont souvent accompagnées de logiciels destinés à aider l'expérience de l'utilisateur. Elles sont également accompagnées de bogues connus et de problèmes de sécurité qui peuvent ne pas être vus dans les versions officielles.

En août 2017, l'équipe LineageOS a organisé une enquête dans laquelle elle a demandé aux utilisateurs de lui faire part de leurs commentaires afin d'améliorer le développement du système d'exploitation. Les résultats ont été publiés en octobre et, selon l'équipe, ils ont utilisé les données recueillies pour améliorer la prochaine version : LineageOS 15. La deuxième enquête d'été a été logiquement menée en août 2018 pour la version 16 du système d'exploitation.

## 2) Pourquoi LineageOS ?

On peut légitimement se demander quelles sont les raisons qui ont motivé ce choix. En effet, il existe de très nombreuses alternatives à Android comme *Replicant*, *OmniROM* ou encore */e/* pour ne citer qu'elles. Néanmoins, le nombre d'appareils supportés est bien moins important (si l'on prend en compte les versions officielles et non officielles) et la communauté moins vaste que celle de *LineageOS*. On ne peut cependant pas dire qu'il s'agisse de "mauvais" systèmes d'exploitation car il remplissent tous le même rôle à leur manière : nous **libérer des services Google et de l'exploitation de nos données.**
Nous allons maintenant lister l'ensemble des avantages qu'apporte LineageOS

### a) Les fonctionnalités
LineageOS offre plusieurs fonctionnalités que l'on ne retrouve pas dans l'Android Open Source Project (À noter que certaines d'entre elles sont tout de même fournies par les constructeurs sur leurs smartphones). Parmi elles, on peut citer :

#### Fonctions de personnalisation

- Personnalisation des boutons - On peut définir un emplacement personnalisé pour les boutons de la barre de navigation, ou activer les boutons intégrés à l'écran pour les appareils dotés de boutons matériels.
- *Caffeine* - Il s'agit d'un outil permettant d'éviter la mise en veille de certaines applications. Cette fonctionnalité est également disponible pour système complet pendant un certain labs de temps que l'on peut définir.
- *LiveDisplay* - Permet d'ajuster la température de couleur de l'affichage en fonction de l'heure de la journée (couper la lumière bleu le soir).
- Personnalisation de l'écran de verrouillage - L'écran de verrouillage permet toutes sortes de personnalisations, y compris celle des couvertures d'album lorsqu'un lecteur de musique est lancé. Ces dernières sont affichées avec un visualiseur de musique. On trouve également la fonctionnalité permettant, à l'aide d'un double appui sur l'écran, de le rallumer/l'éteindre lorque notre appareil est en mode veille.
- Styles - Définit thème global sombre ou clair et personnalise les couleurs prédominentes du système. Cette fonctionnalité peut également être gérée automatiquement par le système en fonction du fond d'écran ou du moment de la journée (avec LiveDisplay).
- Profils système - Activez ou désactivez des paramètres en fonction du profil sélectionné (par exemple, un profil "Accueil" et un profil "Travail"). Le profil peut être sélectionné soit manuellement, soit à l'aide d'un "déclencheur", par exemple en se connectant à un point d'accès WiFi spécifique, en se connectant à un appareil Bluetooth, etc...
- Disposition de l'écran d'acceuil personnalisée - Affichage des application selon le motifs 3x3, 4x4, 5x5 ou 6x6.

#### Fonctions de sécurité et de confidentialité

- Brouillage du code PIN - Pour les utilisateurs qui sécurisent leur appareil avec un code PIN, la disposition des chiffres peut être modifiée à chaque fois que l'appareil se verrouille pour qu'il soit difficile pour d'autres personnes d'identifier votre code de verrouillage en regardant par-dessus votre épaule.
- Protection de la vie privée - Permet à l'utilisateur de régler avec précision les autorisations accordées à chaque application. Pour certaines autorisations, il est possible de définir une approbation manuelle à chaque fois que l'autorisation est demandée. Il est également possible de savoir à quelle fréquence les applications utilisent une autorisation spécifique.
- Apps protégées - Cachez des applications spécifiques derrière un verrou sécurisé. Cela fonctionne en parallèle avec Trebuchet ; l'icône de l'application est supprimée du lanceur d'applications et des "dossiers sécurisés" peuvent être créés pour accéder facilement à ces applications. Un schéma est utilisé pour verrouiller ces applications.
- Certains "numéros sensibles", tels que les numéros d'assistance en cas d'abus, ne sont pas inclus dans le journal des appels pour des raisons de confidentialité.
- *Trust* - Outil contribuant à la sécurité de l'appareil et à la protection de la vie privée.

#### Développeurs et fonctions d'utilisateur avancé

- *LineageSDK* - un ensemble d'API permettant aux développeurs d'applications d'intégrer leurs applications aux fonctionnalités spécifiques de LineageOS telles que les profils système, les styles et la météo.
- Enregistreur d'appels téléphoniques, non disponible dans tous les pays, en raison de restrictions légales.
- Fournisseurs de données météo - Affichage de la météo dans des widgets ou des applications utilisant un fournisseur de données météo. Cette fonctionnalité n'est pas incluse par défaut ; un fournisseur doit être téléchargé à partir du site web de LineageOS Downloads. Les développeurs d'applications peuvent créer à la fois des fournisseurs et des consommateurs de données météorologiques.

### b) Support d'un appareil

À titre d'exemple, je dispose d'un BQ Aquaris M5 sorti en 2015 dont le support officiel des mises à jour a été stoppé en 2017. Grâce à LineageOS, il est possible de disposer de mises à jour supplémentaires jusqu'en Mars 2019 ce qui représente une durée de support non négligeable contrairement à celui fourni initialement par un fabriquant. Un smartphone Android dépassant rarement les 3 ans de support pour les mises à jour, l'utilisation de LineageOS peut apporter une réelle plus value.

### c) Les applications

Comme nous l'avions vu dans la première partie de ce mémoire, les smartphones embarquent de très nombreuses applications pré-installées (applications systèmes, Google Apps, applications constructeurs, applications pré-installées, applications opérateur). En installant LineageOS, seules les applications systèmes (Ex : appels, messages) seront présentes sur notre smartphone. Ces applications sont développées par Google mais sont entièrement Open Source et ne nécessitent pas l'utilisation des services Google. En résumé, avec LineageOS, le nombre d'applications déjà installées sur notre smartphone sera réduit au strict nécessaire évitant ainsi d'avoir un grand nombre d'applications inutiles à désinstaller lors du premier démarrage !

### d) Les services Google

Comme nous l'avons vu dans l'Introduction de ce mémoire, Google fournit avec son système d'exploitation ce que l'on appelles les ***GSF (Google Services Framework)***[6]. Dans cette partie, nous allons voir qu'elle peut être l'ampleur de leur utilisation par Google avec un exemple basé sur le rapport ***"Google Data Collection" (document 1 en Annexe)*** détaillant le quotidien d'un utilisateur fréquent des services Google.

[7] Image Life with Google Services

Comme on peut le voir ci dessus, un total de 13 activités ont pu être recensées par la collecte de données liée au smartphone. Google va tirer de précieuses informations de l'ensemble de ces activités : 

1. Les goûts musicaux de l'utilisateur sont connus grâce à l'application *Google Play Music* (cela pourrait très bien être *Spotify* ou encore *Deezer* qui utilisent les services Google et dont une partie des données est transmise).

2. Grâce à la géolocalisation, on sait que l'utilisateur s'est rendu à une garderie donc qu'il a un ou plusieurs enfants. 

3. Toujours grâce à la géolocalisation, on sait que notre utilisateur a pris le métro. Il s'agit certainement du meilleur moment de la journée pour afficher une notification liée à l'actualité afin que ce dernier puisse la consulter. 

4. L'utilisateur a fait une recherche sur des médicaments en lien avec un rhume, lui ou son/ses enfants peuvent donc être malade. Des études ont démontré qu'un individu était plus vulnérable en étant malade et sa capacité à acheter augmentait de surcroît. Il sera certainement judicieux d'afficher plus de publicité incitant à l'achat compulsif durant une courte période.

5. L'utilisateur s'est rendu à pied du métro à son lieu de travail (d'après les données de géolocalisation)

6. L'utilisateur a utilisé Maps afin de trouver un lieu pour déjeuner

7. En utilisant l'application *Starbucks*, il a été identifié que cette personne a commandé un café ce qui nous informe sur ses habitudes en terme de consommation de boisson (revente de statistiques possible).

8. L'utilisateur a pris rendez-vous chez le médecin, un événement a été ajouté dans l'application *Google Calendar* à partir de l'email de confirmation.

9. À partir de l'application *Google Pay*, on sait que notre utilisateur s'est rendu à la pharmacie pour acheter des médicaments (certainement en lien avec un rhume)

10. À partir de l'application *Uber*, notre utilisateur s'est rendu de son lieu de travail à son domicile.

11. L'utilisateur a fait une recherche d'hôtels sur le site web *Expedia.com*, des publicités en lien avec sa recherche lui seront proposées.

12. En utilisant l'enceinte connectée *Google Home*, notre utilisateur a joué une musique pour son/ses enfants. Nous sommes à présents sûrs qu'il a des enfants.

13. L'utilisateur a regardé un show télévisé sur *Youtube*. On connaît à présent ses goûts en terme de contenu vidéo et les futures recommandations à afficher sur *Youtube*. Des vidéos pour enfants seront certainement également proposées afin que ces derniers utilisent eux aussi les services de Google et y soient habitués dès leur plus jeune âge.

Ainsi, à partir des informations récoltées en une seule journée, Google en sait déjà énormément sur vous : **votre famille, vos habitudes, vos goût musicaux, votre lieu de travail, qui est votre médecin, ce que vous achetez, etc...** Très rapidement, Google saura presque tout sur vous et pourra revendre l'ensemble de ces données à de nombreux annonceurs qui pourront vous cibler de manière très efficace par la publicité ou à des services de diffusion qui connaîtront les contenus les plus adaptés à votre profil, etc... 

L'outil le plus redoutable dans cette stratégie de récolte de données reste **la géolocalisation**. En effet, on pense souvent être protégé en désactivant la géolocalisation, le Wi-Fi ou encore le Bluetooth mais il n'en est rien. Dans un premier temps, une géolocalisation grossière peut être effectuée à partir des coordonnées GPS du smartphone. Ensuite, afin d'affiner la position de l'appareil, les identifiants des antennes de téléphonie auxquelles le smartphone est connecté peuvent être transmis. On peut aussi géolocaliser le smartphone à partir du signal Wi-Fi qu'il émet. C'est aussi le cas du signal Bluetooth qui permet de fournir jusqu'à l'étage exact auquel nous sommes situés. Également, il existe des paramètres au sein du smartphone (pouvant être désactivés par l'utilisateur) ayant pour objectif de scanner les réseaux Wi-Fi ou appareils Bluetooth à proximité en vue de s'y connecter **même si le Wi-Fi ou le Bluetooth étaient jusqu'à présents désactivés**. Une fois un appareil détecté, ce dernier va transmettre sa position vers le notre et on pourra ainsi en déduire notre propre géolocalisation. Les points d'accès Wi-Fi publics étant très présents en ville, la géolocalisation y est grandement facilitée. Google peut déterminer avec un degré de confiance élevé si un utilisateur est immobile, s'il marche, court, fait du vélo, prend le train ou la voiture. Pour ce faire, il suit les coordonnées de localisation d'un utilisateur à intervalles réguliers, en combinaison avec les données des capteurs embarqués (ex : un accéléromètre) au sein du smartphone. C'est avec ces procédés que Google peut quasiment vous géolocaliser à tout moment (sauf si vous êtes en mode avion ce qui est très peu fréquent) faisant de votre smartphone un espion hors pair.

Ceci nous amène au point le plus important lorsque l'on installe LineageOS : **il n'y a plus de *GSF***. En effet, nativement, LineageOS ne dispose pas des services de Google et met un point d'honneur à ne pas espionner les utilisateurs de son système d'exploitation et revendre leurs données aux plus offrants.

## 3) Comment remplacer les services Google ?

### a) Impact des services Google

Les services Google, bien qu'ils constituent un réel obstacle à la mise en place de notre "smartphone libre" jouent un rôle essentiel pour le bon fonctionnement de très nombreuses applications. Sans services Google, l'ensemble des applications de Banking ou de navigation ne pourront pas fonctionner. Il est tout à fait possible de passer par leurs équivalents disponible sur le web. Néanmoins, toutes les applications ne disposent pas d'une version accessible depuis le web. De plus, certaines applications populaires, malgré le fait qu’elles soient open source, nécessitent aujourd’hui l’installation des bibliothèques propriétaires de Google.

### b) La solution MicroG

[8] Logo MicroG

**MicroG GmsCore** est une implémentation libre et ouverte du framework des Google Play Services. Il permet aux applications qui font appel à l'API propriétaire de Google de fonctionner sur des variantes d'*AOSP* comme *LineageOS* ou *Replicant*. C'est un outil puissant pour reprendre la main sur ses données personnelles tout en continuant de profiter des fonctionnalités de base d'Android. En effet, avec cette alternative, il n'y a nullement besoin de disposer d'un compte Google sur son smartphone. C'est cet élément qui est fondamental car même si certaines fonctionnalités nécessitent de faire appel aux serveurs de Google, les données envoyées ne permettront pas de vous identifier et de faire l'objet d'un traitement quelconque.

### c) Les avantages apportés par MicroG

Voici la liste des fonctionnalités apportées par MicroG :
- **Remplacement des Google Play Services** pour la quasi-totalité des applications du Google Play Store (certaines applications ne fonctionne pas correctement).
- **Fournit un service de localisation en ligne/hors ligne** avec le module Unified Network Location Provider (UnifiedNlp) qui gère les appels des applications vers le Network Location Provider de Google. Pour remplacer l'outil de Google, on peut par exemple installer le Mozilla Location Service (MLS) qui est un service ouvert permettant aux appareils de déterminer leur emplacement en fonction de la présence d'infrastructures réseau comme les balises Bluetooth, les antennes de téléphonie cellulaire et les points d'accès WiFi. Ce service de localisation en réseau complète les systèmes de navigation par satellite tels que l'A-GPS.
- **Peu gourmand en ressources** (batterie, mémoire et processeur) car très peu de données sont véhiculées vers les serveurs de Google (seuls quelques services nécessitent un passage par ces serveurs).
- **Pas de publicité ciblée** car pas de tracker d'activité d'installé.
- **Entièrement libre et ouvert** contrairement aux services de Google qui éloignent Android de sa vocation à être Open Source.

### d) Compatiblité avec LineageOS

Afin de pouvoir utiliser MicroG, notre système Android doit supporter le **Signature Spoofing** qui permet à GmsCore de simuler l'existence du Play Service officiel pour les applications qui appellent l'API de Google. Or, ce n'est pas le cas avec LineageOS. Néanmoins, il existe une version nommée *"LineageOS for microG"* qui implémente directement toutes les fonctionnalités de MicroG au sein de LineageOS. C'est cette version que nous allons installer par la suite et qui ne nécessite aucune modification particulière lors de l'installation par rapport à une version classique de LineageOS.

## 4) ADB et Fastboot

### a) Qu'est-ce que ADB et Fastboot ?

L'**Android Debug Bridge (adb)** est un outil de développement qui facilite la communication entre un appareil Android et un ordinateur personnel. Cette communication se fait le plus souvent par un câble USB, mais les connexions Wi-Fi sont également prises en charge.
**Fastboot** est un outil inclu dans le paquet Android SDK utilisé principalement pour modifier le système de fichiers flash via une connexion USB depuis l'ordinateur hôte.

### b) Installation

La procédure d'installation va être réalisée à partir d'Arch Linux. Selon le système d'exploitation utilisé, les étapes peuvent être différentes.
Dans un premier temps, on télécharge l'archive d'installation à l'adresse suivante : <br/>
https://dl.google.com/android/repository/platform-tools-latest-linux.zip
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

# Lexique + Images
- [1] https://upload.wikimedia.org/wikipedia/commons/thumb/f/f3/LineageOS_Logo.svg/512px-LineageOS_Logo.svg.png
- [2] https://fr.wikipedia.org/wiki/GitHub
- [3] https://fr.wikipedia.org/wiki/GitLab
- [4] https://fr.wikipedia.org/wiki/Wiki
- [5] https://fr.wikipedia.org/wiki/Bug_(informatique)
- [6] https://apkpure.com/google-services-framework/com.google.android.gsf
- [7] https://digitalcontentnext.org/wp-content/uploads/2018/08/DCN-Google-Data-Collection-Paper.pdf
- [8] https://microg.org/img/microg_full_colored.svg
