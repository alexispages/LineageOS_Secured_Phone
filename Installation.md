# II) Installation de LineageOS

Dans cette partie, nous allons procéder à l'installation d'un sytème d'exploitation alternatif à Android nommé ***LineageOS***. L'ensemble des opérations vont être réalisées sur un *BQ Aquaris M5* fonctionnant sur la version "pure" d'Android 7.0.0.

## 1) Qu'est-ce que LineageOS ?

*LineageOS* est un système d'exploitation libre et gratuit disponible sur smartphones et tablettes basé sur l'Android Open Source Project (AOSP). Il succède à *CyanogenMod* lorsque *Cyanogen Inc*. a annoncé qu'elle arrêtait le développement et fermait l'infrastructure à l'origine du projet. Comme *Cyanogen Inc.* a conservé les droits sur le nom de Cyanogen, le projet a été rebaptisé *LineageOS*.

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

À titre d'exemple, je dispose d'un BQ Aquaris M5 sorti en 2015 dont le support officiel des mises à jour a été stoppé en 2017. Grâce à LineageOS, il est possible de disposer de mises à jour supplémentaires jusqu'en Mars 2019 ce qui représente une durée de support non négligeable contrairement à celui fourni initialement par un fabriquant. Un smartphone Android dépassant rarement les 3 ans de support pour les mises à jour, l'utilisation de LineageOS apporte une réelle plus value.
