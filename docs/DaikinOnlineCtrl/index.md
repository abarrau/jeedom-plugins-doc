# Description

Ce plugin permet de piloter les climatiseurs Daikin par l'intermédiaire du module Wifi "Online Controller".

# Configuration

## # PRE-REQUIS : 

Vous devez avoir installé et configuré le module wifi Daikin Online Controller pour pouvoir utiliser ce plugin. <br/>
Sans ce boitier, le plugin ne pourra pas agir sur la clim directement. Il n'est pas prévue pour fonctionner avec des modules infra-rouge (par exemple). <br/>
Vous pouvez vous reporter à l'annexe 1 qui explique comment installer et configurer ce module wifi. <br/>

## # Installation et configuration du plugin

Après téléchargement du plugin, vous devez l'activer pour profiter de ces fonctionnalités.

![Configuration](https://abarrau.github.io/jeedom-plugin-DaikinOnlineCtrl-doc/assets/images/DaikinOnlineCtrl_screenshot2.jpg)
	
Le module wifi Daikin ne permet actuellement pas d’exploiter les modes *powerfull* et *oeil intelligent*. <br/>
Le plugin Daikin Online Ctrl simule donc ces 2 modes tout en vous permettant d’affiner leurs réglages. <br/>

*Santé des modules :*
Il peut arriver qu’un module wifi ne soit plus exploitable (retour d’erreur à chaque commande) mais toujours joignable pour permettre au plugin, via sa fonction de soin automatique, de lui envoyer un ordre de redémarrage.

[cols="2,2,8", frame="topbot", options="header"]
|=======================
| Paramètre	| Type | Description
3+| == Powerful ==
| Durée | Liste de choix | Permet de définir la durée de cette action. Au bout de ce temps, l'équipement revient aux valeurs initiales. +
Choix possibles : 5, 10, 15 ou 20 minutes.
| Degrés supplémentaires | Liste de choix | Définit le nombre de degrés à ajouter à la consigne ou la sonde durant ce temps de powerful. +
Choix possibles : 3, 4, 5 ou 6 degrés. 
| Température de référence | Liste de choix | Définit à partir de quelle valeur les degrés supplémentaires sont ajoutées pour définir la nouvelle valeur de consigne. +
Choix possibles : sonde ou consigne.
| Force l'arrêt | Action | Permet d'arrêter le mode powerful sur tous les modules. + 
Ce mode étant simulé, si une difficulté est rencontré durant son utilisation, cette action permet de revenir à un mode "normal" ; par contre les valeurs initiales ne sont pas repositionnées automatiquement et vous devrez le faire manuellement. 
3+| == Oeil intelligent ==
| Autorise la fonction | Checkbox + 
_(décoché par défaut)_ | Définie si cette fonction "virtuelle" peut être utilisée au niveau du plugin. Si oui, les options complémentaires ci-dessous sont proposées.
| Durée absence | Liste de choix | Permet de définir la durée de cette action. Au bout de ce temps, l'équipement abaisse la température en fonction de la valeur configurée ci-dessous. +
Choix possibles : 5, 10, 15 ou 20 minutes.
| Abaisse la température | Liste de choix | Définit le nombre de degrés en moins à appliquer à la consigne durant une absence détectée. +
Choix possibles : 2, 3, 4 ou 5 degrés. 
3+| == Santé des modules ==
| Soigne les modules | Checkbox + 
_(décoché par défaut)_ | Si l'option est activitée et qu'un module est détecté "en erreur", un ordre de redémarrage est envoyé au module. 
Remarque: cette fonction n'est possible que si c'est le module qui indique son état d'erreur (err=255); il n'y a pas d'autre cas du demande se redémarrage.
|=======================

Le plugin propose également l'accès à une "réplique" de l'application mobile de Daikin. Pour y accéder, autoriser le "panel mobile".

''''
### Description des paramètres de l'équipement

La configuration des équipements est accessible à partir du menu plugins, dans la catégorie "Bien-être". +

image::../images/DaikinOnlineCtrl_configuration02.png[]

La page du plugin Daikin regroupe l’ensemble des modules configurés : +

image::../images/DaikinOnlineCtrl_configuration03.png[]

Cliquez sur “Ajouter” pour ajouter un module. Renseignez ensuite les *paramètres de bases*. +
L’aide contextuelle apporte tous les détails nécessaires à la configuration du module. +

image::../images/DaikinOnlineCtrl_screenshot3.jpg[]

[cols="2,2,8", frame="topbot", options="header"]
|=======================
| Paramètre	| Type | Description
| Nom de l’équipement | Zone de texte | Nom donné à votre équipement, il s'affiche sur le widget. + 
*Remarque :* +
- il est possible de le masquer si vous cocher l'option "Ne pas afficher le nom" dans la configuration de la commande; + 
- ce nom contient également un lien depuis le dashboard permettant de revenir directement à la configuration.
| Objet parent 	| Liste de choix | Associe l'équipement à un objet (permettant de définir sa position sur le dashboard)
| Activer	| Checkbox + 
_(décoché par défaut)_ | Si coché, active l'équipement. +
*Remarque :* Si l'option est décochée, l'équipement est désactivé et aucune requête ne sera échangé avec le module ; l'équipement est _"en attente"_.
| Visible	| Checkbox +
_(décoché par défaut)_ | Si l'option est cochée, affiche l'équipement. +
*Remarque :* Si l'option est décochée, l'équipement fonctionne normalement; les requêtes continues d'être envoyées, mais il ne s'affiche pas sur votre dashboard.
| Autre Widget	| Checkbox + 
_(décoché par défaut)_ | Cette option vous permet de désactiver le widget standard du plugin et donc d'utiliser le widget jeedom ou de créer son propre widget. + 
_(Il est conseillé de laisser cette option décochée, pour disposer de l'ensemble des fonctionnalités du plugin ; surtout avec la complexité des commandes disponible au niveau de ce plugin)._
| Adresse IP du module wifi | Zone de texte | Saisir l'adresse IP de votre module sous la forme "A.B.C.D".
| Ne pas sauvegarder les dernières valeurs | Checkbox + 
_(décoché par défaut)_ | Si décoché, lors d'un changement de mode, les paramètres (température, vitesse, ..) du mode sortant sont sauvegardés; vous permettant lors d'un retour dans ce mode de revenir à vos dernières valeurs. +
Si cette option est cochée, les valeurs par défaut seront ré-appliquées (cf. Annexe "valeurs par défaut").
| Période de synchro des commandes | Liste de choix | Définir la durée entre 2 synchro avec le module wifi. 
Cette option est principalement utile si vous utilisez également la télécommnde de votre clim, elle permet de se mettre "à niveau" par rapport à la configuration actuelle de la clim. +
Si vous n'utiliser pas la télécommande, il est quand même recommandé de mettre une synchro pour vérifier l'état de votre clim et s'assurer que clim et équipement sont en phase. +
Choix possibles : Aucune, 1, 5, 15 minutes ou 1 heure.
| Offset de température (mesure interieure) | Liste de choix | cette option applique un offset à la valeur (info) de la température intérieure remontée par le module. + 
La température intérieure prend en compte cet offset au niveau de la commande info et du widget; sur ce dernier, une flèche vers le bas est affichée à coté de la température lors que l'option est utilisée. +
Choix possibles : Aucun, et de 0.5° à 4.0° par pas de 0.5°.
| Période de synchro température | Liste de choix | Définir la durée entre 2 synchro avec le module wifi pour récupérer les valeurs des sondes de température. +
Choix possibles : Aucune, 1, 2, 3, 5 ou 10 minutes.
| Autoriser "Marche" automatique sur action | Checkbox + 
_(décoché par défaut)_ | Cette option permet d'envoyer lors de mise en fonction de la clim sur lors d'une action (exemple: changement de température). + 
Cette option a un intérêt principalement au niveau des scénarios, elle évite d'avoir à lancer 2 actions successives lorsque la clim est éteinte (ex: ON + température), vous pourrez uniquement demnder la commande température et la clim se mettra en marche également.
*Remarque:* La commande n'a pas d'action si la clim est déjà en marche.
|=======================

*Remarque:* La catégorie n'est pas configurable au niveau de l'équipement, ce dernier est positionné dans la catégorie "Chauffage" directement.

''''
### Description des paramètres des commandes

*A savoir:* Le module Daikin remonte plusieurs informations et commandes, le plugin les prend toutes en compte. +
Toutefois en fonction du modèle de clim, toutes les informations et commandes ne sont pas exploitables. +
Une option (info/commande disponible) est donc mise à disposition de l'utilisateur et laissée à sa main, lui permettant d'indiquer de lui même celles qui peuvent être utilisées ou non. +
Par défaut, lors de la création, certaines valeurs sont arbitrairement mise "OUI", rien ne vous empèche de les mettre à "NON" si vous ne disposez pas de cette information/action (ou inversement). +

#### Les "informations"

Les informations disponibles seront exploitables depuis vos scénarios (si activées). +

_Le tableau ci-dessous ne décrit pas les informations disponibles, mais les options disponibles._ +

image::../images/DaikinOnlineCtrl_configuration05.png[]

[cols="2,8", frame="topbot"]
|=======================
| Info disponible | Rend disponible l'information ou non. 
| Historiser | Permet d'historiser l'information. +
*Remarques:* +
- Température : lorsque la clim est éteinte, la température extérieure n'est plus remontée (pour certain module), la valeur d'absence d'information est alors positionnée à "-0.09". +
Cela permet d'identifier au niveau des courbes, l'absence d'information (la lisibilité est meilleure en mode "escalier"). +
- Durée utilisation : vous pouvez également définir la fréquence de stockage de cette information. +
Choix possibles : 10, 15, 30 minutes ou 1 heure.
| Actions | Le bouton "test" permet de tester le retour d'information. +
Pour les "paramètres" (roue crantée) de la commande : il n'est pas conseillé d'aller modifier des valeurs; par contre il est conservé pour obtenir des informations utiles. +
_(Toute modification est sous votre responsabilité)_ +
|=======================

*Remarque:* Ces commandes peuvent être ordonnée dans le cas d'une utilisation avec un widget standard (hors plugin, option "autre widget" à 0UI).

#### Les "commandes"

Toute commande activée (ou non désactivable) est exploitable dans vos scénarios. La colonne “Options” vous permet quant à elle d’adapter le Widget selon vos besoins (exemple plus bas). +

image::../images/DaikinOnlineCtrl_configuration07.png[]




''''
### Présentation du Widget

_en rédaction_

''''
### Présentation de "l'application" (panel) mobile

_en rédaction_

''''
### Exemple d'utilisation

_en rédaction_

''''
## Annexes

''''
### Annexe 1 : Installation et configuration du module wifi

[cols="2,1,1", role="col-sm-12 table table-bordered"]
|=======================
| *a) Connecter le module Daikin à la climatisation :* +
- couper l'arrivée électrique de la climatisation +
- ouvrir l'unité intérieure Daikin (vous pouvez vous aider de la vidéo pour FTXS / ATXS / CTXS) +
- connecter le module au port S21 de la carte électronique +
- refermer l'unité intérieure et remettre le courant +
|
|
| *b) Configurer le module Daikin en mode AP (Access Point) :* +
Le mode AP permet au module Daikin de créer un réseau Wifi privé sur lequel se connecter depuis un smartphone ou tablette pour configurer les paramètres de son réseau Wifi personnel. Maintenir le bouton ([yellow-background]#MODE#) environ 2s pour passer du mode ([yellow-background]#RUN#) au mode ([yellow-background]#AP#). +
| image:../images/DaikinOnlineCtrl_InstallModule_img1.png[]
| image:../images/DaikinOnlineCtrl_InstallModule_img2.png[]
| *c) Se connecter au module Daikin depuis son smartphone (ou tablette) :* +
Les identifiants nécessaires pour se connecter au module Daikin en mode AP sont fournis sur une petite étiquette autocollante mais aussi sur la tranche du module (identifiants = SSID / Key). +
- ouvrir les paramètres Wifi et se connecter au réseau SSID “DaikinAPxxxxx” (mot de passe = Key) +
 +
*NB:* si le réseau “DaikinAPxxxxx” est invisible, essayer avec un autre smartphone / tablette. +

| image:../images/DaikinOnlineCtrl_InstallModule_img3.png[]
| image:../images/DaikinOnlineCtrl_InstallModule_img4.png[]
| *d) Connecter le module Daikin à votre réseau Wifi :* +
- installer l’application Daikin Online Controller, ouvrir l'application puis accepter le contrat de licence +
- attendre la découverte du module Daikin +
 +
*NB:* si une pastille de couleur apparaît sur l'icône de l'unité découverte, le firmware doit être mis à jour. +
| image:../images/DaikinOnlineCtrl_InstallModule_img5.png[]
| image:../images/DaikinOnlineCtrl_InstallModule_img6.png[]
| - sélectionner l’unité découverte (Unité 1 dans l’exemple) et aller dans le menu ([yellow-background]#Plus#) +
- entrer dans la section ([yellow-background]#Connexion WLAN#) et sélectionner le réseau à rejoindre +
| image:../images/DaikinOnlineCtrl_InstallModule_img7.png[]
| image:../images/DaikinOnlineCtrl_InstallModule_img8.png[]
| - saisir le mot de passe du réseau Wifi à rejoindre et appuyer sur Enregistrer (en haut à droite) +
| image:../images/DaikinOnlineCtrl_InstallModule_img9.png[]
| image:../images/DaikinOnlineCtrl_InstallModule_img10.png[]
| Le module Daikin va se connecter au réseau Wifi et comme l’indique le popup, si la connexion est réussie le voyant RUN va clignoter puis rester fixe. Appuyer alors sur Succès pour que le smartphone / tablette se déconnecte du réseau “DaikinAPxxxxx”. +
Si le voyant RUN clignote encore après un délais de 30s, le module Daikin ne réussi pas à se connecter à votre réseau. Dans quel cas, appuyer sur Échec et contrôler les paramètres Wifi indiqués à l’étape précédente. +
|
|
|=======================

''''
### Annexe 2 : Valeurs par défaut

Si l'option "Ne pas sauvegarder les dernières valeurs" est cochée, les valeurs par défaut sont réappliquées à chaque changement de mode. +

Ces valeurs sont : 

* Température : 19° 
* Vitesse : vitesse 1
* Orientation : arrêté
* Humidité : 0 _(non utilisé)_


''''
### Annexe 3 : En savoir plus sur le module wifi

Voici le lien sur le site Daikin pour ce module wifi : http://www.daikin.be/fr/products/index.jsp?singleprv=BRP069A42&pf=0 +
Et une description des fonctionnalités de l'application : http://www.daikineurope.com/minisite/onlinecontroller/always_in_control/

''''
### Annexe 4 : Compatibilité des splits et des commandes 

_en rédaction_

''''
### Annexe 5 : Les class CSS disponibles et paramètres optionnels

Les class CSS disponibles pour personnaliser le widget du plugin sont : 

[cols="1,2", width="70%", role="col-sm-12 table table-bordered"]

|=======================
| DOC_title | Zone de titre de la tuile
|=======================

Les paramètres optionnels disponibles applicable sur le widget du plugin sont : 

[cols="1,2", width="70%", role="col-sm-12 table table-bordered"]
|=======================
| valeur-off | valeur à afficher lorsque la sonde température/humidité est éteinte (par défaut: off)
|=======================




== FAQ
==== _Le module *BRP069A43* est-il pris en charge par le plugin ?_
Oui, d'après les retours le module *BRP069A43* fonctionne bien avec le plugin Daikin Online Ctrl. 


== Roadmap
- optimisation du cron() pour la vérification de l'état du trigger, à prévoir ! +


<style>
img[src*="#icone"] {width:70px;height:70px;}
</style>
