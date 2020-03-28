# Description

Ce plugin permet de piloter les climatiseurs Daikin par l'intermédiaire du module Wifi "Online Controller".

<span style='color:red;'>**Point d'attention (Suivi de ce plugin au 08/02/20) :**</span>
* DaikinOnlineCtrl n'offrira plus d'évolution fonctionnelle majeure (sauf si proposé par d'autre utilisateur) ; toutefois, il sera maintenu pour le garder compatible avec les évolutions du core de Jeedom.
* la version courante (1.3.0) est optimisée pour être compatible v4, mais pas spécialement pour la v3 (tout problème d'ergonimie sous v3, ne sera plus pris en compte; exemple perte d'icone ...)

# Configuration

## # PRE-REQUIS : 

Vous devez avoir installé et configuré le module wifi Daikin Online Controller pour pouvoir utiliser ce plugin. <br/>
Sans ce boitier, le plugin ne pourra pas agir sur la clim directement. Il n'est pas prévue pour fonctionner avec des modules infra-rouge (par exemple). <br/>
Vous pouvez vous reporter à l'annexe 1 qui explique comment installer et configurer ce module wifi.

## # Installation et configuration du plugin

Après téléchargement du plugin, vous devez l'activer pour profiter de ces fonctionnalités.

![Configuration](https://abarrau.github.io/jeedom-plugins-doc/DaikinOnlineCtrl/images/DaikinOnlineCtrl_screenshot2.jpg)	
	
Le module wifi Daikin ne permet actuellement pas d’exploiter les modes **powerfull** et **oeil intelligent**. <br/>
Le plugin Daikin Online Ctrl simule donc ces 2 modes tout en vous permettant d’affiner leurs réglages.

**Santé des modules :**
Il peut arriver qu’un module wifi ne soit plus exploitable (retour d’erreur à chaque commande) mais toujours joignable pour permettre au plugin, via sa fonction de soin automatique, de lui envoyer un ordre de redémarrage.


**Powerful**

| Paramètre	| Type | Description |
|--|--|--|
| Durée | Liste de choix | Permet de définir la durée de cette action. Au bout de ce temps, l'équipement revient aux valeurs initiales. <br/> Choix possibles : 5, 10, 15 ou 20 minutes. |
| Degrés supplémentaires | Liste de choix | Définit le nombre de degrés à ajouter à la consigne ou la sonde durant ce temps de powerful. <br/> Choix possibles : 3, 4, 5 ou 6 degrés. |
| Température de référence | Liste de choix | Définit à partir de quelle valeur les degrés supplémentaires sont ajoutées pour définir la nouvelle valeur de consigne. <br/> Choix possibles : sonde ou consigne. |
| Force l'arrêt | Action | Permet d'arrêter le mode powerful sur tous les modules. <br/> Ce mode étant simulé, si une difficulté est rencontré durant son utilisation, cette action permet de revenir à un mode "normal" ; par contre les valeurs initiales ne sont pas repositionnées automatiquement et vous devrez le faire manuellement. 

**Oeil intelligent**

| Autorise la fonction | Checkbox <br/> _(décoché par défaut)_ | Définie si cette fonction "virtuelle" peut être utilisée au niveau du plugin. Si oui, les options complémentaires ci-dessous sont proposées. |
| Durée absence | Liste de choix | Permet de définir la durée de cette action. Au bout de ce temps, l'équipement abaisse la température en fonction de la valeur configurée ci-dessous. <br/> Choix possibles : 5, 10, 15 ou 20 minutes. |
| Abaisse la température | Liste de choix | Définit le nombre de degrés en moins à appliquer à la consigne durant une absence détectée. <br/> Choix possibles : 2, 3, 4 ou 5 degrés. |

**Santé des modules**

| Soigne les modules | Checkbox <br/> _(décoché par défaut)_ | Si l'option est activitée et qu'un module est détecté "en erreur", un ordre de redémarrage est envoyé au module. <br/>_**Remarque:**_ cette fonction n'est possible que si c'est le module qui indique son état d'erreur (err=255); il n'y a pas d'autre cas du demande se redémarrage. |

<br/>
Le plugin propose également l'accès à une "réplique" de l'application mobile de Daikin. Pour y accéder, autoriser le "panel mobile".


## # Description des paramètres de l'équipement

La page du plugin Daikin regroupe l’ensemble des modules configurés :

![Equipement](https://abarrau.github.io/jeedom-plugins-doc/DaikinOnlineCtrl/images/DaikinOnlineCtrl_equipement.png)	

<span style="color:blue;">NOTES :</span>
* En cliquant sur l’icone tableau à coté de la zone recherche, vous permet de passer d’un affichage “icone” à un affichage sous forme de “tableau”.

![Equipement tableau](https://abarrau.github.io/jeedom-plugins-doc/DaikinOnlineCtrl/images/DaikinOnlineCtrl_equipementtableau.png)

Cliquez sur “Ajouter” pour ajouter un module. Renseignez ensuite les _paramètres de bases_. <br/> L’aide contextuelle apporte tous les détails nécessaires à la configuration du module.

#### -- Onglet "Equipement"

![Equipement tableau](https://abarrau.github.io/jeedom-plugins-doc/DaikinOnlineCtrl/images/DaikinOnlineCtrl_screenshot3.jpg)

| Paramètre	| Type | Description |
|--|--|--|
| Nom de l’équipement | Zone de texte | Nom donné à votre équipement, il s'affiche sur le widget. <br/> _**Remarque :**_ <br/> - il est possible de le masquer si vous cocher l'option "Ne pas afficher le nom" dans la configuration de la commande; <br/> - ce nom contient également un lien depuis le dashboard permettant de revenir directement à la configuration. |
| Objet parent 	| Liste de choix | Associe l'équipement à un objet (permettant de définir sa position sur le dashboard) |
| Activer	| Checkbox <br/> _(décoché par défaut)_ | Si coché, active l'équipement. <br/> _**Remarque :**_ Si l'option est décochée, l'équipement est désactivé et aucune requête ne sera échangé avec le module ; l'équipement est _"en attente"_. |
| Visible	| Checkbox <br/> _(décoché par défaut)_ | Si l'option est cochée, affiche l'équipement. <br/> _**Remarque :**_ Si l'option est décochée, l'équipement fonctionne normalement; les requêtes continues d'être envoyées, mais il ne s'affiche pas sur votre dashboard. |

**Compléments Plugin (ergonomie)**

| Autre Widget	| Checkbox <br/> _(décoché par défaut)_ | Cette option vous permet de désactiver le widget standard du plugin et donc d'utiliser le widget jeedom ou de créer son propre widget. <br/> _(Il est conseillé de laisser cette option décochée, pour disposer de l'ensemble des fonctionnalités du plugin ; surtout avec la complexité des commandes disponible au niveau de ce plugin)._ |
| Lien vers "panel" depuis widget mobile | Checkbox | Permet d'afficher un bouton sur le widget en vue "mobile", pour renvoyer ver "la réplique de l'application Daikin" (panel). |
| Ne pas remonter les erreurs dans la console des messages Jeedom | Checkbox | permet de désaciriver la remonté d'informaton dans la console des messages Jeedom. Les "erreurs/warning" seront visibles uniquement dans les logs ou santé du plugin. <br> _**Remarque:**_ Ce cas est interressant si vous rencontrez régulièrement des "pertes réseaux" du module. |

#### -- Onglet "Paramètres"

![Paramètres](https://abarrau.github.io/jeedom-plugins-doc/DaikinOnlineCtrl/images/DaikinOnlineCtrl_parametre.png)	

| Paramètre	| Type | Description |
|--|--|--|
| Adresse IP du module wifi | Zone de texte | Saisir l'adresse IP de votre module sous la forme "A.B.C.D". |
| Ne pas sauvegarder les dernières valeurs | Checkbox _(décoché par défaut)_ | Si décoché, lors d'un changement de mode, les paramètres (température, vitesse, ..) du mode sortant sont sauvegardés; vous permettant lors d'un retour dans ce mode de revenir à vos dernières valeurs. <br/> Si cette option est cochée, les valeurs par défaut seront ré-appliquées (cf. Annexe "valeurs par défaut"). |
| Période de synchro des commandes | Liste de choix | Définir la durée entre 2 synchro avec le module wifi. <br/>Cette option est principalement utile si vous utilisez également la télécommnde de votre clim, elle permet de se mettre "à niveau" par rapport à la configuration actuelle de la clim. <br/> Si vous n'utiliser pas la télécommande, il est quand même recommandé de mettre une synchro pour vérifier l'état de votre clim et s'assurer que clim et équipement sont en phase. <br/>Choix possibles : Aucune, 1, 5, 15 minutes ou 1 heure. |
| Offset de température (mesure interieure) | Liste de choix | cette option applique un offset à la valeur (info) de la température intérieure remontée par le module. <br/> La température intérieure prend en compte cet offset au niveau de la commande info et du widget; sur ce dernier, une flèche vers le bas est affichée à coté de la température lors que l'option est utilisée. <br/> Choix possibles : Aucun, et de 0.5° à 4.0° par pas de 0.5°. |
| Période de synchro température | Liste de choix | Définir la durée entre 2 synchro avec le module wifi pour récupérer les valeurs des sondes de température. <br/> Choix possibles : Aucune, 1, 2, 3, 5 ou 10 minutes. |
| Autoriser "Marche" automatique sur action | Checkbox <br/> _(décoché par défaut)_ | Cette option permet d'envoyer lors de mise en fonction de la clim sur lors d'une action (exemple: changement de température). <br/> Cette option a un intérêt principalement au niveau des scénarios, elle évite d'avoir à lancer 2 actions successives lorsque la clim est éteinte (ex: ON + température), vous pourrez uniquement demnder la commande température et la clim se mettra en marche également. <br/>_**Remarque:**_ La commande n'a pas d'action si la clim est déjà en marche. |

**Remarque:** La catégorie n'est pas configurable au niveau de l'équipement, ce dernier est positionné dans la catégorie "Chauffage" directement.

#### -- Onglet "Commandes"

**Paramétrage des informations**

_**A savoir:**_ Le module Daikin remonte plusieurs informations et commandes, le plugin les prend toutes en compte. <br/>Toutefois en fonction du modèle de clim, toutes les informations et commandes ne sont pas exploitables. <br/>Une option (info/commande disponible) est donc mise à disposition de l'utilisateur et laissée à sa main, lui permettant d'indiquer de lui même celles qui peuvent être utilisées ou non. <br/>Par défaut, lors de la création, certaines valeurs sont arbitrairement mise "OUI", rien ne vous empèche de les mettre à "NON" si vous ne disposez pas de cette information/action (ou inversement).

![Configuration](https://abarrau.github.io/jeedom-plugins-doc/DaikinOnlineCtrl/images/DaikinOnlineCtrl_configuration05.png)

| Info disponible | Rend disponible l'information ou non. |
| Historiser | Permet d'historiser l'information. <br/>_**Remarques:**_<br/>- Température : lorsque la clim est éteinte, la température extérieure n'est plus remontée (pour certain module), la valeur d'absence d'information est alors positionnée à "-0.09". <br/> Cela permet d'identifier au niveau des courbes, l'absence d'information (la lisibilité est meilleure en mode "escalier"). <br/>- Durée utilisation : vous pouvez également définir la fréquence de stockage de cette information. <br/> Choix possibles : 10, 15, 30 minutes ou 1 heure. |
| Actions | Le bouton "test" permet de tester le retour d'information. <br/> Pour les "paramètres" (roue crantée) de la commande : il n'est pas conseillé d'aller modifier des valeurs; par contre il est conservé pour obtenir des informations utiles. <br/> _(Toute modification est sous votre responsabilité)_ |

_**Remarque:**_ Ces commandes peuvent être ordonnée dans le cas d'une utilisation avec un widget standard (hors plugin, option "autre widget" à 0UI).

**Paramétrage des commandes**

Toute commande activée (ou non désactivable) est exploitable dans vos scénarios. La colonne “Options” vous permet quant à elle d’adapter le Widget selon vos besoins (exemple plus bas).

![Config7](https://abarrau.github.io/jeedom-plugins-doc/DaikinOnlineCtrl/images/DaikinOnlineCtrl_configuration07.png)

**Paramétrage des mémoires programmées**

Vous pouvez créer des commandes "mémoires", avec les paramétrages par défaut qui vous convient. 

Pour cela, cliquer sur le bouton "Ajouter une mémoire" et renseigner les valeurs souhaitez pour : le mode, la température, le débit d'air, la direction. <br/>
_**Remarque:**_ Le nom court doit être de 2 caractères de préférence. 

![ConfigMemory](https://abarrau.github.io/jeedom-plugins-doc/DaikinOnlineCtrl/images/DaikinOnlineCtrl_configurationmemory.png)

Pour le paramètre température, une option "sélectionner une commande" est disponible. Elle permet d'utiliser une commande externe pour définir le choix de la température. <br/>
_**Remarque:**_ La valeur de cette commande externe doit être en accord avec les min/max autorisés avec le mode sélectionné. Cette valeur est obligatoirement un entier.

![ConfigMemory](https://abarrau.github.io/jeedom-plugins-doc/DaikinOnlineCtrl/images/DaikinOnlineCtrl_selectcmdtemp.png)


## # Présentation de "l'application" (panel) mobile

Cette application est à l'image de l'application officiel Daikin. Le comportement des commandes est identique. 

## # Annexes

#### --- _Annexe 1 : Installation et configuration du module wifi_

| **a) Connecter le module Daikin à la climatisation :** <br/> - couper l'arrivée électrique de la climatisation <br/> - ouvrir l'unité intérieure Daikin (vous pouvez vous aider de la vidéo pour FTXS / ATXS / CTXS) <br/> - connecter le module au port S21 de la carte électronique <br/> - refermer l'unité intérieure et remettre le courant | | |
| **b) Configurer le module Daikin en mode AP (Access Point) :** <br/> Le mode AP permet au module Daikin de créer un réseau Wifi privé sur lequel se connecter depuis un smartphone ou tablette pour configurer les paramètres de son réseau Wifi personnel. Maintenir le bouton (<span style="background-color:yellow;">#MODE#</span>) environ 2s pour passer du mode (<span style="background-color:yellow;">#RUN#</span>) au mode (<span style="background-color:yellow;">#AP#</span>). | ![Module1](https://abarrau.github.io/jeedom-plugins-doc/DaikinOnlineCtrl/images/DaikinOnlineCtrl_InstallModule_img1.png) | ![Module2](https://abarrau.github.io/jeedom-plugins-doc/DaikinOnlineCtrl/images/DaikinOnlineCtrl_InstallModule_img2.png) |
| **c) Se connecter au module Daikin depuis son smartphone (ou tablette) :** <br/> Les identifiants nécessaires pour se connecter au module Daikin en mode AP sont fournis sur une petite étiquette autocollante mais aussi sur la tranche du module (identifiants = SSID / Key). <br/> - ouvrir les paramètres Wifi et se connecter au réseau SSID “DaikinAPxxxxx” (mot de passe = Key) <br/><br/>**NB:** si le réseau “DaikinAPxxxxx” est invisible, essayer avec un autre smartphone / tablette. | ![Module3](https://abarrau.github.io/jeedom-plugins-doc/DaikinOnlineCtrl/images/DaikinOnlineCtrl_InstallModule_img3.png) | ![Module4](https://abarrau.github.io/jeedom-plugins-doc/DaikinOnlineCtrl/images/DaikinOnlineCtrl_InstallModule_img4.png) |
| **d) Connecter le module Daikin à votre réseau Wifi :** <br/> - installer l’application Daikin Online Controller, ouvrir l'application puis accepter le contrat de licence <br/> - attendre la découverte du module Daikin <br/><br/> **NB:** si une pastille de couleur apparaît sur l'icône de l'unité découverte, le firmware doit être mis à jour. | ![Module5](https://abarrau.github.io/jeedom-plugins-doc/DaikinOnlineCtrl/images/DaikinOnlineCtrl_InstallModule_img5.png) | ![Module6](https://abarrau.github.io/jeedom-plugins-doc/DaikinOnlineCtrl/images/DaikinOnlineCtrl_InstallModule_img6.png) |
| - sélectionner l’unité découverte (Unité 1 dans l’exemple) et aller dans le menu (<span style="background-color:yellow;">#Plus#</span>) <br/>- entrer dans la section (<span style="background-color:yellow;">#Connexion WLAN#</span>) et sélectionner le réseau à rejoindre | ![Module7](https://abarrau.github.io/jeedom-plugins-doc/DaikinOnlineCtrl/images/DaikinOnlineCtrl_InstallModule_img7.png) | ![Module8](https://abarrau.github.io/jeedom-plugins-doc/DaikinOnlineCtrl/images/DaikinOnlineCtrl_InstallModule_img8.png) |
| - saisir le mot de passe du réseau Wifi à rejoindre et appuyer sur Enregistrer (en haut à droite) | ![Module9](https://abarrau.github.io/jeedom-plugins-doc/DaikinOnlineCtrl/images/DaikinOnlineCtrl_InstallModule_img9.png) | ![Module10](https://abarrau.github.io/jeedom-plugins-doc/DaikinOnlineCtrl/images/DaikinOnlineCtrl_InstallModule_img10.png) |
| Le module Daikin va se connecter au réseau Wifi et comme l’indique le popup, si la connexion est réussie le voyant RUN va clignoter puis rester fixe. Appuyer alors sur Succès pour que le smartphone / tablette se déconnecte du réseau “DaikinAPxxxxx”. <br/> Si le voyant RUN clignote encore après un délais de 30s, le module Daikin ne réussi pas à se connecter à votre réseau. Dans quel cas, appuyer sur Échec et contrôler les paramètres Wifi indiqués à l’étape précédente. |

#### --- _Annexe 2 : Valeurs par défaut_

Si l'option "Ne pas sauvegarder les dernières valeurs" est cochée, les valeurs par défaut sont réappliquées à chaque changement de mode.

Ces valeurs sont : 

* Température : 19° 
* Vitesse : vitesse 1
* Orientation : arrêté
* Humidité : 0 _(non utilisé)_

#### --- _Annexe 3 : En savoir plus sur le module wifi_

Voici le lien sur le site Daikin pour ce module wifi : http://www.daikin.be/fr/products/index.jsp?singleprv=BRP069A42&pf=0

Et une description des fonctionnalités de l'application : http://www.daikineurope.com/minisite/onlinecontroller/always_in_control/


#### --- _Annexe 4 : Compatibilité des splits et des commandes_

Cette liste n'est pas exaustive, n'hésitez pas à remonter vos remarques [ici](https://github.com/abarrau/jeedom-plugins-doc/issues)

| Modèle | Version logicielle | Commentaire |
| BRP069A42 | App Daikin 2.4.1 | direction horizontale non dispo |
| BRP069A43 | | |
| BRP069B41 | 1.2.48 | directions verticale et horizontale inopérantes |


#### --- _Annexe 5 : Les class CSS disponibles et paramètres optionnels_

Les class CSS disponibles pour personnaliser le widget du plugin sont : 

| DOC_title | Zone de titre de la tuile |

Les paramètres optionnels disponibles applicable sur le widget du plugin sont : 

| valeur-off | valeur à afficher lorsque la sonde température/humidité est éteinte (par défaut: off) |

**Remarque :** avec tous les changements d'ergonomie apportée avec la V4, ces class peuvent ne plus fonctionner correctement. Il est donc préférable d'utiliser les fonctions proposées par Jeedom. 



## ?? Pourquoi ce plugin ??

C'est le 1er défit lancé par Masterfion qui venait de s'équiper de clim Daikin, et j'allais de mon coté m'en équiper également .... alors je me suis lancé à l'aveugle dans mon 1er plugin en 2015.<br/>
Beaucoup d'heure de travail, mais le plugin est toujours là, c'est ce qui compte :) 

Bonne utilisation ....
