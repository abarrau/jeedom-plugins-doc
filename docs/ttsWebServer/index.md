# Description

Ce plugin vous permet de générer des messages TTS via un Web Service dédié hébergé sur Android (donc aucune utilisation du cloud).
Pour permettre cette fonction, ce plugin nécessite obligatoirement l'installation de l'application Android du même nom (TTS Web Server).

Le plugin dispose des fonctionnalités suivantes : 

* de diffuser sur différents players :
	* local sur l'équipement Android (téléphone, tablette,...)
	* via le plugin ttsWebServer (pour les plugins intégrés) `(*1)(*2)`
	* via les commandes d'un plugin Tiers, utilisant les librairies du plugin ttsWebServer `(*2)` 
* de sauvegarder les messages générés sur : 
	* un espace de partage distant (ex: NAS Synology)
	* localement sur la box Jeedom
* d'une bibliothèque des messages complètement administrable, ainsi que la possibilité d'utiliser tous les moteurs `(*3)` installés sur votre équipement Android. 

	
`(*1)`: **les plugins associés doivent obligatoirement être installés** pour que la diffusion sur ces players fonctionnent correctement (pour certains, les commandes "dire" des plugin initiaux sont réutilisés).
_Remarque:_ si le plugin n'est pas installé, la diffusion de la synthèse par celui-ci ne sera pas proposée au niveau du TTS Web Server.<br/>
`(*2)`: voir la liste des plugins compatibles (interne et tiers) en annexe.<br/>
`(*3)`: par défaut, le moteur Google, mais aussi si vous achetez des voix supplémentaires (Voxygen par exemple).

Les commandes du Serveur TTS peuvent être utilisées via le Widget (standard jeedom) sur les dashboard/design, mais également au niveau des scénarios.

<span style="color:blue;">**NOTE :** </span>
* _dans la suite du document, "TTS Web Server" est abrégé en "TWS"._
* _sur les différentes interfaces (configuration, équipement, ...) pour chaque paramètre, une icone avec un "?" permet d'obtenir des informations sur le paramètre et permet déjà d'apporter un niveau de compréhension._

## # Représentation des 2 widgets possibles

![widgets](https://abarrau.github.io/jeedom-plugin-ttsWebServer-doc/assets/images/ttsWebServer_screenshot7.jpg)

# Configuration

## # PRE-REQUIS avant toute utilisation 

Ces "pré-requis" peuvent constituer une description pas à pas des tâches à suivre avant de commencer à utiliser le plugin. 

* Sur la page configuration : 
	* Vérifier que les dépenses sont bonnes
	* Cocher la case "bouton "Ajouter"" si la dépendance "ARP-SCAN" ne peut pas s'installer `(*1)`
	* Cocher l'option "Afficher le panel mobile"
* Sur votre terminal Android : 
	* Activer le paramètre "source inconnue" (généralement accessible dans les paramètres de sécurité)
	* Autoriser le stockage de fichiers pour l'application TWS (action à faire, une fois l'installation terminée, étapes ci-dessous)
* Depuis l'interface mobile de Jeedom `(*2)`, se rendre sur le menu plugin :
	* cliquer sur l'icone TWS et installer l'application
	* lancer l'application
* Sur la page des équipements :
	* lancer une découverte > les équipements (application distante TWS) apparaitront !

`(*1)` <span style="color:red;">**POINT d'ATTENTION :**</span> si les dépendances ne s'installent pas correctement, décocher la fonction "découverte", et relancer les dépendances ; ça devrait être OK à ce moment là. 
`(*2)` l'interface mobile est accessible via un navigateur Web, il n'est pas question ici de l'application mobile de Jeedom.


## # Version Android

Pour l'installation de l'APK, la version du build minimum d'Android autorisé est le "19", correspondant à la version 4.4 (kitkat).
_Pour plus d'information se référer à l'adresse : [https://source.android.com/source/build-numbers](https://source.android.com/source/build-numbers)._


## # Installation et configuration du plugin

Après téléchargement du plugin, vous devez l'activer pour profiter de ces fonctionnalités.

La mise à niveau / installation des "Dépendances" est essentielle pour disposer de toutes les fonctionnalités du plugin. 
_(pour plus d'informations sur les dépendances : [https://github.com/abarrau/jeedom-plugin-ttsWebServer-doc/wiki/TTS-Web-Server-Plugin-:-liste-des-d%C3%A9pendances](https://github.com/abarrau/jeedom-plugin-ttsWebServer-doc/wiki/TTS-Web-Server-Plugin-:-liste-des-d%C3%A9pendances))_

Des paramètres de configuration vous sont proposés, mais les valeurs par défaut peuvent être conservées.

![Configuration du plugin](https://abarrau.github.io/jeedom-plugin-ttsWebServer-doc/assets/images/ttsWebServer_screenshot2.jpg)

| Paramètre | Description |
|--|--|
| Autoriser la diffusion sur  | Liste les types de player où le TTS peut être diffusé (dépend des plugins intégrés et installés).<br/> Si vous ne souhaitez pas que le plugin TWS propose une commande pour un type de player (ex: Sonos), vous pouvez le décocher. <br/> _**Remarque :** <br/>- après l'installation de TWS, si vous installez un nouveau plugin de player, il ne sera pas coché par défaut (car non connu de TWS) ; <br/>- les plugins tiers ne sont pas pris en comptes dans cette liste._  |
| (Maintenance) Autoriser la suppression des fichiers temporaires "résiduels" | Si l'option est activée, une maintenance quotidienne (à 0h), est réalisée pour supprimer des différents répertoires du plugin les fichiers générés temporairement.<br/>_**Remarque :** une suppression est déjà opérée au fil de l'eau théoriquement._ <br/>Un bouton vous permet de réaliser l'opération manuellement à tout moment. |
| (Maintenance) Vérifier l'existence des fichiers | Si l'option est activée, une maintenance quotidienne (à 0h), est réalisée pour vérifier si les fichiers listés dans la bibliothèque sont bien présents, en fonction du "lieu" de sauvegarde défini. <br/>En cas d'erreur, une icone s'affiche dans la colonne "emplacement" sur la bibliothèque. <br/> Un bouton vous permet de réaliser l'opération manuellement à tout moment. |
| (Maintenance) Rechercher les fichiers "orphelins" | Permet de rechercher les fichiers orphelins (présents sur l'espace de stockage, mais absents de la bibliothèque). 2 valeurs possibles: <br/> - <span style="color:blue;">"création en bibliothèque"</span>: le fichier est recréé dans la bibliothèque, mais sans phrase associée; cela vous permet d'avoir une vision de ce que vous avez dans le répertoire de stockage et les supprimer au besoin. <br/>- <span style="color:blue;">"suppression"</span>: le fichier est directement supprimé. |
| (Maintenance) Suppression fichiers anciens | Permet de supprimer les fichiers dont la date d'utilisation est plus ancienne que la durée sélectionnée.<br/> Valeurs possibles: Désactivé, 15j, 30j, 90j, 180j. |
| (Distant) TimeOut des requêtes | Définit la durée de timeout de la requête émise entre le plugin et l'application Android TTS Web Server. <br/> Valeurs possibles: 10, 15, 30 et 60 secondes. |
| (Distant) Fréquence de récupération des logs | Définit la fréquence à laquelle, le plugin TWS ira récupérer les logs disponibles sur l'application Android TWS, pour les enregistrer localement sur jeedom. <br/> Valeurs possibles: Désactivé, 5, 15, 30 mins, 1h, 3h. |
| Modes autorisés pour l'ajout d'équipement distant "TTS Web Server" | Propose 2 choix : le bouton "Ajouter" (avec saisie manuelle), et le bouton "Découverte". <br/>_**Remarque :**<br/> - le bouton "Découverte" n'est disponible que si la dépendance "ARP-SCAN" est installée. <br/>- le bouton "Ajouter" n'est pas proposé par défaut (il a été rajouté suite à la rencontre des difficultés pour certains utilisateurs)._ | 

## # Page des équipements TWS

![Page Equipement](https://abarrau.github.io/jeedom-plugin-ttsWebServer-doc/assets/images/ttsWebServer_screenshot1.jpg)

Cette page se découpe en 3 zones : 

* la **Gestion** : permet d'afficher les outils de configuration du plugin : 
	* "Découverte" : permet de lancer la découverte de nouveaux équipements sur le réseau `(*1)`
	* "Synchroniser" : permet de lancer la synchronisation des players pour voir s'il y en a de nouveaux disponibles et configurés dans Jeedom ; ces découvertes permettront de créer les commandes développées dans le plugin TWS ; tous les "types" de players configurés disposeront de leur propre commande. 
	* "Réglages TTS" : accès aux paramètres du serveur (lieu sauvegarde, encodage, nom des commandes, ...)
	* "Configuration" : accès à la page de configuration

* les **TTS Web Server (application distante)** (Android) : 
	* liste des Web Server distants découverts 

* les **Players TTS** : 
	* liste des players détectés en fonction du plugin associé (_Remarque : ces icones ne sont pas cliquables, c'est juste informatif_).

<span style="color:blue;">**NOTES :**</span> 
* `(*1)`: Pour disposer de ce bouton, les fonctions linux "ARP-SCAN" et "NC" doivent être installées.
De plus l'application Android doit être lancée et active, ainsi que le device (tablette,...) en service et non en veille, sinon la découverte ne pourra pas se faire.
* En cliquant sur l'icone tableau à coté de la zone recherche, vous permet de passer d'un affichage "icone" à un affichage sous forme de "tableau".
![Page Equipement (tableau)](https://abarrau.github.io/jeedom-plugin-ttsWebServer-doc/assets/images/ttsWebServer_screenshot1_tableau.jpg)

## # Description des paramètres du Serveur TWS

Cette page est appelée via l'équipement "Réglages TTS" et permet de configurer le "coeur" du serveur TTS.

* Cet équipement ne doit <span style="color:red;">**JAMAIS**</span> être supprimé ; le cas échéant, le plugin ne pourrait plus fonctionner.
* _S'il y avait suppression par erreur, en cliquant sur l'icone (globe), une proposition de recréation de l'équipement serait proposée._

#### -- L'onglet **<u>"Equipement"</u>** présente les informations standard de Jeedom : 

* Définition du Nom (_Remarque : peut être modifié sans impact_) ; 
* Objet parent : emplacement d'affichage de l'équipement ; 
* les statuts : activé et visible ; (_Remarque: si cet équipement était désactivé, le plugin ne pourrait plus fonctionner_). 

![Page Equipement (tableau)](https://abarrau.github.io/jeedom-plugin-ttsWebServer-doc/assets/images/ttsWebServer_TWS1.jpg)

#### -- L'onglet **<u>"Paramètres"</u>** présente les paramètres de configuration : 

![Page Paramètres](https://abarrau.github.io/jeedom-plugin-ttsWebServer-doc/assets/images/ttsWebServer_screenshot5.jpg)

**Paramètres d'utilisation** : 

| Paramètre	| Description |
|--|--|
| Format de fichier/encodage | Définit le format pour conserver les fichiers. Valeurs possibles: Wav ou MP3. <br/>**Remarque :** En archivage "local", le format MP3 est obligatoire pour permettre une diffusion en mode "radio" sur les différents player. |
| Autoriser l'archivage | Définit l'emplacement où seront stockés les fichiers enregistrés. <br/>Valeurs possibles : <br/> - "aucun" : le fichier est supprimé après son utilisation <br/>- "Distant (nas)": archivage sur un espace distant (autre paramètre à configurer) <br/>- "Local (box jeedom)" : archive les fichiers dans un répertoire local linux sur la box Jeedom `(*1)` |
| _(si Distant)_ <br/> Serveur et dossiers de stockage	| Permet de préciser l'adresse ip et le chemin d'accès au répertoire où les fichiers audios doivent être sauvegardés. <br/> Le champ dossier doit contenir le nom du dossier de partage et le nom du répetoire de stockage. <br/> **Remarque :** il ne peut y avoir qu'un seul niveau de répertoire de stockage. | 
| _(si Distant)_ <br/>Utilisateur et mot de passe | Renseignez les utilisateurs et mot de passe pour accéder à l'espace de partage. |
| Gestion de la diffusion en fonction de la voix | Cette option permet de définir le comportement souhaité par rapport à un même texte à diffusion en fonction de la voix, 2 cas possibles : <br/>- <span style="color:blue;">"Diffusion fichier existant, même si voix différente"</span> : au moment de la diffusion du message, si le message existe en bibliothèque avec une voix différente, le message est quand même diffusé. <br/> - <span style="color:blue;">"Générer un fichier systématiquement, si voix différente"</span> : au moment de la diffusion du message, si le message existe en bibliothèque pour une voix différente, un nouveau message est quand même généré avec la nouvelle voix ; vous aurez donc 2 fois le même contenu de message en bibliothèque pour 2 voix différentes. |

**Liste des applications distantes "TTS Web Server"** :

Cette zone vous permet de définir l'ordre de sollicitation des applications distantes TWS. Cette fonctionnalité est sollicitée si vous diffusez un message sur un équipement autre qu'une tablette/téléphone (exemple: Sonos, ....).

Vous pouvez donc utiliser vos applications distantes en mode "cluster", le 1er est sollicité en priorité, s'il n'est pas disponible le suivant est testé, et ainsi de suite... 

_**Remarque :** La voix configurée au niveau de l'application TWS sera alors utilisée pour la synthèse. Si vous avez configuré des voix différentes, la diffusion dépendra donc de l'application TWS disponible._

Pour définir l'ordre, sélectionnez l'icone "double flêche" et déplacez vos équipements en fonction de votre besoin/souhait ; n'oubliez pas d'enregistrer ensuite.

<span style="color:blue;">**NOTE :**</span>
`(*1)`: l'emplacement par défaut se trouve au même niveau que le répertoire "html" du serveur, et s'appelle "dataTTSWebServer". 
_(exemple en configuration Apache: `/var/www/dataTTSWebServer/`)_


#### -- L'onglet **<u>"Player TTS"</u>** affiche les différents players disponibles : 

![Page Player TTS](https://abarrau.github.io/jeedom-plugin-ttsWebServer-doc/assets/images/ttsWebServer_TWS3.jpg)

Depuis cette page, vous pouvez renommer le nom des commandes qui ont été détectées comme des players potentiels pour la diffusion de TTS.
Ce nom apparait au niveau du widget (bouton de validation d'envoi du texte à synthétiser) sur le widget de l'équipement "Serveur".  
Vous pouvez également paramétrer son affichage ou non (si la case est décochée, la commande ne sera pas affichée sur l'équipement "Serveur").

_**Remarque :** cette liste présente uniquement pour les commandes générées pour les plugins intégrés à TWS ; les commandes des plugins tiers ne sont pas référencées ici._

<span style="color:blue;">**NOTE :**</span>
L'enregistrement de ce nouveau nom (ou changement de paramètres) doit obligatoirement être enregistré par le bouton "enregistré" au niveau de chaque ligne (colonne "Action").

## # Description des paramètres des équipements de synthèse (en relation avec l'appli Android)
 
Un bouton "dupliquer", permet de dupliquer l'équipement et les commandes associées.

#### -- L'onglet **<u>"Equipement"</u>** présente les informations standard de Jeedom.
(idem équipement "Réglage TTS")

#### -- L'onglet **<u>"Paramètres"</u>** présente les paramètres disponibles au niveau de l'équipement hébergeant l'application TWS : 

![Page Paramètres](https://abarrau.github.io/jeedom-plugin-ttsWebServer-doc/assets/images/ttsWebServer_screenshot3.jpg)

**Paramètres d'utilisation** : 

| Paramètre	| Description |
|--|--|
| Voix `(*1)` | liste les voix disponibles sur cet équipement. <br/> - Un bouton "Synchronisation" permet de récupérer les voix disponibles sur l'équipement distant. <br/> - Un bouton "Ecouter" permet d'écouter un exemple de la voix directement sur l'équipement. |
| Pas de cache en lecture locale | Par défaut, en lecture locale sur un équipement distant, le fichier audio généré par la synthèse est renvoyé; permettant de compléter la bibliothèque des messages. <br/> En cochant cette option, aucun fichier ne sera renvoyé, et la bibliothèque ne sera pas renseignée. |

<span style="color:blue;">**NOTE :**</span>
`(*1)`: le changement de voix entre moteur "Voxygen" est assez rapide. Toutefois, le retour sur le moteur "Google" peut générer un temps de latence assez important.  <br/>
Il est donc déconseillé de faire le "yoyo" entre les voix (du moins avec la voix Google), même pour tester !


**Paramètres d'utilisation et Divers** : 

| Paramètre	| Description |
|--|--|
| Adresse IP (wifi) | Les champs @IP sont à renseigner uniquement si l'ajout de l'équipement est fait manuellement. <br/> Si l'équipement a été créé par une "découverte", ces champs sont complétés et non modifiables (grisés). |
| Type d'équipement & Application | _(non utilisé, uniquement à titre d'information)_ |

#### -- L'onglet **<u>"Commandes"</u>** présente les commandes disponibles au niveau de l'équipement local hébergeant l'application TWS : 

![Page Paramètres](https://abarrau.github.io/jeedom-plugin-ttsWebServer-doc/assets/images/ttsWebServer_TWS5.jpg)

Ces commandes sont créées à la création de l'équipement. Vous ne pouvez ni en ajouter, ni en supprimer (elles seront créées lors d'un enregistrement).
Les actions possibles : modifier le nom, paramétrer si vous les affichez ou non et si vous souhaitez historiser les données ou non.
 
| Paramètre	| Description |
|--|--|
| Statut WS | Remonte l'état du service de l'application TWS distante. <br/> _**Remarque :** cette information est mise à jour à chaque requête vers l'application._ <br/> Cas à prendre en compte: dans le cas d'un timeout de la requête TTS, l'état passera à "0". |
| Batterie | Remonte le niveau de batterie de l'équipement distant où est hébergé l'application TWS (en %). <br/> _**Remarque :** le niveau de batterie reste à la dernière valeur connue lorsque l'application distante TWS n'est pas joignable._ |
| Dire | Cette commande permet d'envoyer une demande de diffusion TTS sur l'équipement distant.  <br/>(La même commande se retrouve aussi sur l'équipement "Serveur" pour l'équipement distant en question.) <br/> _**Remarque :** dans ce cas, la fonction "cluster" ne s'applique pas._ |
| Relancer Service | Cette commande permet de relancer le Service sur l'application TWS distante. <br/>_(Attention: cette action NE DEMARRE PAS l'application, elle relance uniquement le service d'écoute.)_ |

#### -- L'onglet **<u>"Etats / infos"</u>** présente de remonter des informations liée à l'application TWS : 

![Page Etats/Infos](https://abarrau.github.io/jeedom-plugin-ttsWebServer-doc/assets/images/ttsWebServer_screenshot4.jpg)

La définition de chaque champ de cette page est décrite directement sur la page, via l'icone "?" à coté du titre.



##  # L'application Android (APK)

###  -- Assistance pour l'installation de l'application

L'APK n'est pas disponible sur le playStore, (_pas la peine de le chercher_).
L'installation peut se faire via le plugin en activant la page "mobile" dans la configuration du plugin.

Depuis votre appareil, allez sur le menu "Plugin", puis "TTS Web Server".
Une page rappelant les pré-requis pour l'installation est affichée.
Après avoir respecté ces pré-requis, cliquez sur l'icone TWS et l'apk est téléchargé sur votre Android (téléphone/tablette), puis son installation est proposée. 

L'application peut être installé sur un appareil Android (tablette,...), fonctionnement en Wifi ou sur une VM, fonctionnement en éthernet. 

![Téléchargement APK](https://abarrau.github.io/jeedom-plugin-ttsWebServer-doc/assets/images/ttsWebServer_install_apk.jpg)

<span style="color:red;">**REMARQUE :**</span><br/>
L'application n'étant pas connue du playStore, vous devez autoriser les "sources inconnues" le temps de l'installation. 
<span style="color:red;">Une fois l'installation terminée, je recommande vivement de revenir à l'état initial en désactivant à nouveau les "sources inconnues", afin d'éviter tout risque à votre équipement Android.</span>

L'APK peut aussi être téléchargé depuis l'adresse suivante (prendre la dernière version systématiquement) : <br/> [https://github.com/abarrau/jeedom-plugin-ttsWebServer-doc/tree/master/apk](https://github.com/abarrau/jeedom-plugin-ttsWebServer-doc/tree/master/apk)


###  -- Présentation de l'application

L'application Android TWS dispose de 3 écrans, ayant des fonctionnalités différentes. 

#### -- Le **<u>"Menu (icone)"</u>** situé en haut, permet de basculer d'un écran à l'autre. 

* Crayon : permet d'afficher les logs de l'application APK 
	* en rouge = service éteint ; 
	* en vert = service démarré (en écoute pour la synthèse) ; 
* Personnage : affiche la liste des messages synthétisés ; 
* Globe : affiche la page "principale", d'état et de démarrage/arrêt du service. 

#### -- L'écran **<u>"principal"</u>** présente les informations et activation du service. 

![APK Ecran 1](https://abarrau.github.io/jeedom-plugin-ttsWebServer-doc/assets/images/ttsWebServer_APK3.png)

| Information | Description |
|--|--|
| Statut | Précise le statut de l'application, en lien avec la couleur de l'icone globe. |
| icone "double flêche" | permet de re/démarrer le service |
| icone "carré" | permet de stoper le service |
| Date de démarrage | donne la date où le service à démarré |
| Nb Synthèse | affiche le nombre de synthèse réalisée au cours de la session |
| Date dernière requête | donne la date de la dernière requête reçue |
| Moteur TTS (actif) | indique le dernier moteur utilisé pour générer un message |
| Adresse IP / Port | affiche l'adresse ip et le port d'écoute |
| Date de démarrage | affiche l'heure de démarrage de l'application APK |
| Moteur TTS (défaut) | indique le moteur utilisé par défaut (peut être différent de celui "actif") |


#### -- L'écran des **<u>"Messages synthétisés"</u>** présente la liste des messages générés durant la session de démarrage de l'application APK. 
Cette liste est remise à vide à chaque redémarrage de l'application (ou manuellement sur demande). 

#### -- L'écran de **<u>"Logs"</u>** affiche la log courante de l'application. 
(Les données affichées sont plutôt techniques).

Cet écran permet d'afficher les logs de l'application pour permettre le debug en cas de problème. 

![APK Ecran 1](https://abarrau.github.io/jeedom-plugin-ttsWebServer-doc/assets/images/ttsWebServer_APK2.png)

Le rafraichissement se fait automatiquement (par défaut 5sec), ou manuellement en cliquant sur l'icone "flêches inversées".

L'icone "Poubelle" supprime le fichier (remise à blanc). 


#### -- L'écran de **<u>"Paramétrages"</u>** de configuration de l'application APK. 

Cet écran est accessible par le menu de configuration depuis l'écran principal. 

![APK Ecran 1](https://abarrau.github.io/jeedom-plugin-ttsWebServer-doc/assets/images/ttsWebServer_APK1.png)

| Paramètre	| Description |
|--|--|
| Lancement au démarrage | Si coché, l'application TWS se lance automatiquement au démarrage de l'appareil Android. (conseillé) |
| Ecran Affiché par défaut | Au lancement de l'application, permet de définir l'écran à afficher ; 2 valeurs possibles : "écran principal" (par défaut) ou "écran message". |
| Lancement à l'ouverture | Permet de lancer le service TTS au démarrage de l'application TWS (conseillé). |
| Afficher données techniques | Sur l'écran message, permet d'afficher les données techniques (durée de génération du fichier son, et emplacement de stockage) |
| Temps de rafraichissement des logs | Permet de définir la fréquence de rafraichissement automatique des logs sur l'écran "Logs". | 


## # La bibliothèque des messages

Pour pouvoir la visualiser, vous devez activer le "panel desktop" depuis la page de configuration du plugin.

![Liste des messages](https://abarrau.github.io/jeedom-plugin-ttsWebServer-doc/assets/images/ttsWebServer_screenshot6.jpg)

Ce tableau présente la liste des messages enregistrés et renseignés dans la bibliothèque du plugin. <br/>
Par défaut, l'ordre d'affichage correspond au dernier message synthétisé ou utilisé, mais l'ordre peut être modifié pour réaliser vos recherches. 
L'utilisateur peut également filtrer les valeurs recherchées.

Des icones peuvent apparaitre, permettant d'identifier des points d'attention vis-à-vis du fichier : 

- <span style="color:red;">"*!*"</span> (à coté de la taille) : indique que le fichier présente une taille faible (inférieure à 90ko). Si vous utilisez ce fichier en lecture locale ou via Squeezebox/SynoAudio, le fichier peut ne pas être lu correctement car pas assez volumineux pour "activer" une lecture.
- <span style="color:fuchsia;">"*?*"</span> (à coté de l'emplacement) : impossible d'indiquer si ce fichier existe, car son emplacement est différent de celui configuré actuellement ; 
- <span style="color:red;">"*x*"</span> (à côté de l'emplacement) : le fichier n'a pas été trouvé à l'emplacement indiqué. 

Le bouton "Tout Supprimer" permet de supprimer toutes les données présentes dans la bibliothèque, ainsi que les fichiers orphelins détectés sur l'espace de stockage en cours de configuration. +

## # Fonctionnalités complémentaires disponibles

### -- Lecture spécifique des unités (scénarios)

Généralement, la diffusion de la température se fait de la manière suivante : "12,5 degrés". 
Si vous rentrez ces informations dans un format spécifique dans votre champs de saisie, vous pourrez obtenir une diffusion au format "12 degrés 5". 

Le format à utiliser est le suivant : `@U|valeur|unité@`, exemple:  `@U|12.5|degrés@`, ou avec une commande jeedom : `@U|\#[cuisine][oregon][température]#|degrés@`. 

A savoir : 
* si les décimales égalent "0", le zéro n'est pas diffusé (exemple: `@U|12.0|degrés@`, il sera diffusé : "12 degré"). 
* la valeur de l'unité n'est pas obligatoire (exemple: `@U|valeur@`), ... mais sans intérêt.

## # Les API

### -- Application Android

Une API est mise à disposition pour comprendre et troubleshooter les échanges entre le plugin et l'application. <br/>
Elle est disponible sur l'espace Github : 
[https://github.com/abarrau/jeedom-plugin-ttsWebServer-doc/wiki/TTS-Web-Server-Android-:-Description-des-m%C3%A9thodes](https://github.com/abarrau/jeedom-plugin-ttsWebServer-doc/wiki/TTS-Web-Server-Android-:-Description-des-m%C3%A9thodes).

### -- Intégration des fonctionnalités TWS dans des plugins tiers

Une API est mise à disposition pour permettre aux développeurs de plugins tiers d'utiliser les fonctionnalités de ce plugin TWS, pour récupérer (par exemple) des fichiers audios issus du plugin TWS. <br/>
La documentation est disponible sur l'espace Github : 
[https://github.com/abarrau/jeedom-plugin-ttsWebServer-doc/wiki/TTS-Web-Server-Plugin-:-fonctions-pour-plugins-tiers](https://github.com/abarrau/jeedom-plugin-ttsWebServer-doc/wiki/TTS-Web-Server-Plugin-:-fonctions-pour-plugins-tiers).


## # Synthèse des intégrations _(juin 2019)_

|Plugin| Type d'intégration  |
|--|--|
|Sonos| Commande développée dans TWS |
|Squeezebox| - Plugin tiers/TWS intégré <br/> - Commande développée dans TWS _(amenée à disparaitre au profils de l'intégration)_ |
|Syno Audio|Commande développée dans TWS |
|Google Home Local| Plugin tiers/TWS intégré|
|Xiaomi Talk| Plugin tiers/TWS intégré|
|GCast (officiel)| Plugin tiers/TWS intégré|


## ?? Pourquoi ce plugin ??

Plugin démarré suite à des échanges avec @Masterfion, qui voulait à tout pris utiliser des voix Voxygène, les voix pico ou google étaient considérées "non optimal". <br/>
L'objectif était donc de pouvoir intéroger un android depuis Jeedom, pour qu'il nous retourne un fichier audio qui serait diffusé sur Sonos. <br/>
La conclusion est ce plugin ! <br/>
Plusieurs développeurs ont identifier "l'intérêt" du plugin et de la qualité de la voix, et ont intégrer ce plugin au leur (Merci à eux !).<br/>
... bonne utilisation. <br/>
