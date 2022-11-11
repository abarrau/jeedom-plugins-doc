# Description
Ce plugin iCalendar vous permet de récupérer les événements d'un agenda gérant le format de fichier iCalendar, dans un fichier .ics : 
* soit en téléchargement d'un fichier ics (google, zimbra, outlook, ...)
* soit en Caldav (lecture seule pour l'instant avec cache local sur la période de synchro)

L’utilisateur dispose de 3 modes de fonctionnement :
* tester la présence de l’évènement et l’état de celui-ci via une condition dans un scénario (utilisation de l’opérateur "matches" pour savoir si une chaîne de caractères en contient une autre).
* définir au niveau de l'événement des "scénarios" ou "actions" qui pourront être automatiquement lancés par Jeedom, en début ou en fin d'événement.
* reconnaissance d'une "interaction" sur le contenu du titre ; après, à vous de définir les actions produites par l'interaction.

<span style='color:red;'>**Point d'attention (Suivi de ce plugin au 18/01/20) :**</span>
* iCalendar n'offrira plus d'évolution fonctionnelle majeure ; toutefois, il sera maintenu pour le garder compatible avec les évolutions du core de Jeedom.
* la version courante (1.5.2) est optimisée pour être compatible v4, mais pas spécialement pour la v3 (tout problème d'ergonimie sous v3, ne sera plus pris en compte).

<span style='color:red;'>**Configuration obligatoire (au 27/10/2022) :**</span>
* Pour les scénarios déclenchés par une commande iCalendar, il est essentiel que le scénario soit passé en "synchrone" (en mode asynchrone, le scénario ne se lance pas). 
* La correction sur la class scénario est pris en compte coté Jeedom (https://github.com/jeedom/core/pull/2113), en attendant le passage en stable, le pré-requis ci-dessus est obligatoire.  


# Configuration
Ce plugin permet de retourner les évènements de votre agenda iCalendar, il suffit pour cela de créer un équipement et de lui ajouter autant de "commandes" que vous avez d'agendas à traiter. Même s’il y beaucoups de paramètres, la configuration du plugin est simple : les paramètres par défaut peuvent être conservés, ce qui facilite la création. <br/>
Vous pouvez l’utiliser pour l'affichage d'agendas tout simplement ou pour récupérer des agendas vous permettant de réaliser des actions dans votre installation Jeedom.

## # Installation et configuration du plugin

Après téléchargement du plugin, vous devez l'activer pour profiter de ses fonctionnalités. <br/>
Des paramètres de configuration vous sont proposés, mais les valeurs par défaut peuvent être conservées. <br/>

![Install](https://abarrau.github.io/jeedom-plugins-doc/iCalendar/images/iCalendar_install.png)

| Paramètre | Type | Description|
|--|--|--|
| TimeOut de syncrho | Zone de liste | Cette option vous permet de définir le temps que vous souhaitez laisser au plugin pour récupérer les données issues du calendrier distant. <br/> Théoriquement, cette action est assez rapide, mais ce paramètre est disponible en cas de besoin. <br/> Les valeurs possibles sont : 5 sec / 15 sec / 30 sec.|
| Pannel: vue par défaut | Zone de liste | Lorsque vous allez sur l'écran "Panel", cette option précise la vue qui sera affichée par défaut pour l'utilisateur. <br/> Les valeurs possibles sont : <br/> - Calendrier: jours <br/>- Calendrier: 4 jours <br/>- Calendrier: semaine <br/>- Calendrier: mois <br/>- Actions: planning |
| Afficher le panel desktop | Checkbox | Si coché, le panel "calendrier" sera affiché. |

Une fois l'activation réalisée depuis la page des "équipements", vous pourrez ajouter de nouveaux calendriers iCalendar. 

![Page Equipement](https://abarrau.github.io/jeedom-plugins-doc/iCalendar/images/iCalendar_pageequipement.png)

**Remarque :** Le bouton "Aide à la saisie d'actions au sein d'un événement" vous permet d'assister à la création du format à placer dans le champ description de votre événement. <br/>
Pour rappel, le lancement automatique d'actions par le plugin n'est possible que si l'option "Autoriser les actions/scénarios" est validée au niveau de votre commande agenda. (cf. Annexe 1 : "Aide à la saisie d'un évènement dans votre agenda").

<span style="color:blue;">NOTES :</span>
* En cliquant sur l’icone tableau à coté de la zone recherche, vous permet de passer d’un affichage “icone” à un affichage sous forme de “tableau”.

![Page Equipement tableau](https://abarrau.github.io/jeedom-plugins-doc/iCalendar/images/iCalendar_pageequipementtableau.png)


## # Description des paramètres de l'équipement
 
Un bouton "dupliquer", permet de dupliquer l'équipement et les commandes associées. +

#### -- L'onglet "Equipement" présente les informations standard de Jeedom : 

![Config. Equipement](https://abarrau.github.io/jeedom-plugins-doc/iCalendar/images/iCalendar_screenshot2.jpg)

| Paramètre | Type | Description |
|--|--|--|
| Nom de l’équipement | Zone de texte | Nom donné à votre équipement agenda iCalendar, il s'affiche sur le widget. <br> _**Remarque :**_ <br/>- il est possible de le masquer si vous cochez l'option "Ne pas afficher le nom" dans la configuration de la commande; <br/>- ce nom contient également un lien depuis le dashboard permettant de revenir directement à la configuration. |
| Objet parent 	| Liste de choix | Associe l'équipement agenda iCalendar à un objet (permettant de définir sa position sur le dashboard)
| Activer	| Checkbox <br/>_(décoché par défaut)_ | Si coché, active l'équipement. <br/> _**Remarque :**_ Si l'option est décochée, l'équipement est désactivé et aucune requête ne sera demandée, échangée avec votre agenda externe; l'équipement est _"en attente"_. |
| Visible	| Checkbox <br/>_(décoché par défaut)_ | Si l'option est cochée, affiche l'équipement. <br/>*Remarque :* Si l'option est décochée, l'équipement fonctionne normalement; les requêtes continuent d'être envoyées vers votre agenda externe, mais il ne s'affiche pas sur votre dashboard. |
| Catégorie	| Checkbox <br/>_(multichoix)_ | Définit la catégorie à laquelle est rattaché l'agenda. |

**Options de sauvegarde**

| Paramètre | Type | Description |
|--|--|--|
| Forcer  la synchronisation | Checkbox | Permet de réaliser une synchronisation des données de votre agenda, au moment de l'enregistrement de l'équipement. |


#### -- L'onglet "Paramètres complémentaires" : 

![Config](https://abarrau.github.io/jeedom-plugins-doc/iCalendar/images/iCalendar_config01.png)

**Paramètres graphique**

| Paramètre | Type | Description |
|--|--|--|
| Autre Widget	| Checkbox<br/>_(décoché par défaut)_ | Cette option vous permet de désactiver le widget standard du plugin et donc d'utiliser le widget Jeedom ou de créer son propre widget.<br/>_(Il est conseillé de laisser cette option décochée, pour disposer de l'ensemble des fonctionnalités du plugin)._ |
| Ne pas afficher la date | Checkbox<br/>_(décoché par défaut)_ | Si l'option est cochée, la date est masquée sur le widget; le texte "aujourd'hui : JJ MOIS AAAA (SW)" n'est pas affiché pour le Dashboard et les vues.<br/>Au niveau de la version mobile, le logo avec la date du jour n'est pas affiché.  |
| (multi journée) Format d'affichage | Zone de liste | Définit le format d'affichage des calendriers (si plusieurs journées sélectionnées).<br/>- "1 journée avec jour de navigation": permet d'afficher la journée courante ; pour voir les évènements des autres journées, cliquez sur la date.<br/>- "tout affiché": permet d'afficher tous les évènements pour l'ensemble des jours sélectionnés. | 
| (multi agenda) Format d'affichage | Zone de liste | Définit le format d'affichage des calendiers, soit en mode vertical (standard) ou en mode horizontal.<br/>_**Remarque:**_ Ne s'applique que pour la version Dashboard; la version mobile est toujours verticale. |
| Redessiner la tuille automatiquement | Checkbox | Permet de redimensionner automatiquement la tuile au niveau du dashboard desktop ou mobile, si le nombre d'évènements change.<br/>Cela évite que la liste sorte en dehors de la tuile. |

**Paramètres événements**

| Paramètre | Type | Description |
|--|--|--|
| Ajouter Message sur "action" | Checkbox<br/>_(décoché par défaut)_ | Cette option permet d'ajouter un message à la boîte des messages Jeedom, dans le cas où le plugin a déclenché une action, un scénario ou une interaction.<br/>_**Remarque:**_ Pour cela, il faut avoir autorisé les actions/scénarios ou interactions au niveau de votre commande agenda.<br/>Cette option ne fonctionne pas dans le cas d'une utilisation par déclenchement de scénario sur mise à jour de la commande. |
| Autorise "Rattrapage" / Période | Checkbox<br/>_(décoché par défaut)_<br/>Liste de choix | L'activation de cette option permet de pouvoir lancer des actions/scénarios/interactions, mmême si l'heure exacte de l'événement est dépassé.<br/>Le plugin dispose alors d'une fenêtre de temps pour déclencher ces actions, si elles n'ont pas été faites dans les temps.<br/>_**Remarque:**_ Ce paramètre est surtout utile aux petites configurations (RPI1) qui pouvaient par moment se retrouver en dehors de la minute de début ou de fin de l'événement et l'action ne se lançait pas.<br/>_(exemple: événement débute à 8h30, hors à 30, il y a beaucoup de crons de lancés. On pouvait constater que le cron minute était en fait traité à 31 ; l'instant T ne correspondant plus à l'heure de début de l'événement, les actions/scénarios associés étaient ignorés)_ <br/> Cette option peut aussi être utile en cas de coupure de courant courte, vous pourrez rattraper des actions non exécutées. <br/><br/> Les périodes disponibles sont : <br/>- les 2 dernières minutes <br/>- les 5 dernières minutes <br/>- les 15 dernières minutes <br/>- l'heure précédente <br/>_**Remarque:**_ ces 4 périodes sont glissantes par rapport à l'instant T. |

**Paramètres traitement**

| Paramètre | Type | Description |
|--|--|--|
| Log séparée par Agenda | Checkbox | Permet de séparer les fichiers de logs des agendas (pour une meilleure lecture en mode débug). |


## # Description des paramètres des agendas

Les agendas peuvent être triés par ordre d'affichage, en cliquant sur l'icône "double flêches" en haut à gauche et en déplaçant le tableau de haut en bas. <br/>

![Param](https://abarrau.github.io/jeedom-plugins-doc/iCalendar/images/iCalendar_screenshot3.jpg)

**Nom et URL**

| Paramètre | Type | Description |
|--|--|--|
| Nom | Zone de texte | Permet de donner un nom au calendrier ; cette valeur s'affiche dans la zone de titre du calendier sur le widget. 
| Nom ics | Zone de texte | Nom récupéré au niveau du fichier ICS ; valeur non modifiable. |
| Type d'agenda | Zone de liste | Vous permet de définir le type d'agenda que vous configurez et la méthode de récupération de l'ICS. Les choix possibles sont : <br/>- `récupération d'un fichier ics` : correspond au téléchargement d'un fichier issu d'un serveur tiers ; <br/>- `lecture d'un agenda CalDav` : permet de récupérer le contenu d'un agenda CalDav et d'avoir un fichier ics local ; |
| URL de l'agenda | Zone de texte | Définit l'URL du fichier ics. Pour retrouver l'URL, voir l'Annexe 3.
| Utilisateur | Zone de texte | (s'affiche uniquement en "caldav") <br/> Permet de définir le nom de l'utilisateur du serveur CalDav. |
| Mot de passe | Zone de texte | (s'affiche uniquement en "caldav") <br/> Permet de définir le mot de passe de l'utilisateur du serveur CalDav. |
| Nom agenda | Zone de texte | (s'affiche uniquement en "caldav") <br/>Caldav offrant la possibilité d'avoir plusieurs agendas actifs, vous pouvez spécifier ici le nom de l'agenda à récupérer. <br/>Ce champ n'est pas obligatoire; s'il est non renseigné, le plugin prendra le 1er agenda retourné par le serveur Caldav ("personnal" généralement). <br/>_**Remarque:**_ un bouton d'aide vous permet de visualiser la liste des agendas disponibles et de copier le nom de l'agenda souhaité. |

**Données d'utilisation**

| Paramètre | Type | Description |
|--|--|--|
| Format données | Zone de liste <br/>_("événement sur la journée" par défaut)_ | Définit le "format" à afficher au niveau du widget et contenu dans la commande ; 3 valeurs sont disponibles (cf. Annexe 4) : <br/>- `événement sur la journée` : affiche et traite tous les évènements de la journée (passés, en cours, à venir) ; <br/>- `événement heure à venir` : affiche et traite les événements courants, + ceux de l'heure à venir (même s'ils n'ont pas démarré) ; <br/>- `événement courant` : affiche et traite les événements en cours uniquement ; |
| Titre uniquement | Checkbox <br/>_(décoché par défaut)_ | Cette option n'est disponible que si "format de données" = " événement courant". <br/> Le contenu de la commande agenda est alors la plus simpliste possible, elle ne présente que les titres ; tous les paramètres annexes (id, état) à l'événement ne sont pas disponibles. <br/> **Remarque: Si vous utilisez cette option, l'option "Autoriser les scénarios/actions" sera INVALIDEE techniquement.** |
| Période à traiter | Zone de liste <br/>_("jour courant" par défaut)_ | Définit le nombre de jours à traiter : <br/> - `jour courant` : gère les données de la journée courante au niveau de la commande "J0" ; <br/> - `+ lendemain` : gère les données de la journée courante et celles du lendemain (J0+J1) ; <br/> - `+ 2jours` : gère les données de la journée courante et celles des 2 jours suivants (J0+J1+J2) ; <br/> - `1 semaine` : gère les données de la journée courante et celles des 6 jours suivants (J0 à J6) ; <br/> _**Remarque:**_ n'est disponible que si "format de données" = "événement sur la journée". <br/> Dans le cas où vous êtes dans une configuration supérieure à la journée courante, une icône orange apparait à coté du titre; en cliquant dessus, la liste des commandes associées aux autres journées apparait en dessous du tableau. |
| Valeur par défaut | Zone de texte | Valeur affichée par défaut, lorsqu'il n'y a aucun évènement dans le planning. <br/>_**Remarque:**_ Si rien n'est indiqué, la valeur "Aucun" est retournée. |
| Indicateurs début/fin | Checkbox <br/>_(décoché par défaut)_ | Permet de définir si les indicateurs de début/de fin d'évènement sont utilisés, aussi bien à l'affichage et aussi pour l'execution d'une action/scénario; <br/> - Si coché : les indicateurs "Début" (<span style="background-color:yellow;">#;DA;#</span>) et "Fin" (<span style="background-color:yellow;">#;FA;#</span>) d'activité sont utilisés en complément de l'indicateur "Actif" <br/> - Si décoché : seul l'indicateur d'état "Actif" est utilisé (<span style="background-color:yellow;">#;A;#</span>). |
| Autoriser les scénarios/actions | Checkbox <br/>_(décoché par défaut)_ | Cette option permet au plugin de lancer automatiquement les scénarios ou actions, si la description de l'événement respecte correctement le format attendu pour cette action (cf. Annexe 1 : "Aide à la saisie d'un évènement"). |
| Autoriser les interactions | Checkbox <br/> _(décoché par défaut)_ | Cette option permet au plugin de lancer une recherche d'interaction sur la base du titre de l'événement. <br/> _**Remarque:**_ cette option ne s'active uniquement que sur les événements qui n'ont pas d'action/scénarios configurés dans leurs descriptions. |
| Historiser les actions | Checkbox <br/>_(décoché par défaut)_ | A chaque action/scénario/interaction lancé par le plugin, l'action produite est tracée (pour ne pas être relancée plus tard). <br/> Cette option permet de conserver ces actions traitées au-delà de la journée courante. |
| Fréquence synchro | Liste de choix <br/> _(30 min, par défaut)_ | L'utilisateur peut configurer la période de rafraîchissement du fichier cache (minimum 30 min) ; (cf. tableau Annexe 2). |

**Option graphique**

| Paramètre | Type | Description |
|--|--|--|
| Afficher calendrier | Checkbox <br/> _(coché par défaut)_ | Paramètre graphique ; permet de définir si le calendrier doit être affiché dans le widget. <br/> _**Remarque :**_ ce paramètre n'est que graphique, il n'impacte pas les données (celles-ci continuent d'être traitées, même si l'option est désactivée). |
| Afficher heure | Checkbox <br/>_(coché par défaut)_ | Paramètre graphique ; permet de définir si les heures de début et de fin sont affichées dans le widget. <br/> _**Remarque :**_ ce paramètre n'est que graphique, il n'impacte pas les données (l'heure continue d'être présente dans la donnée, même si l'option est désactivée). |
| Afficher heure event de 24h | Checkbox <br/> _(coché par défaut)_ | Paramètre graphique ; permet de définir si les heures de début et de fin sont affichées pour les évènements durant toute la journée (24 h) dans le widget. <br/>Le paramètre n'est pas affiché si l'option "Afficher heure" est décochée. <br/>_**Remarque :**_ ce paramètre n'est que graphique, il n'impacte pas les données (celles-ci continuent d'être traitées, même si l'option est désactivée). |
| Afficher l'emplacement | Checkbox <br/> _(coché par défaut)_ | Paramètre graphique ; permet d'afficher l'information de lieu disponible au niveau de l'événement. <br/>_**Remarque:**_ Cette information n'est disponible qu'à l'affichage pour l'instant; vous pouvez aussi la récupérer au niveau d'un scénario via la fonction "getLocation". |
| Période à afficher | Zone de liste | Définit le nombre de jours à afficher sur le widget : <br/> - `jour courant` : affiche les données de la journée courante; <br/> - `+ lendemain` : affiche les données de la journée courante et celles du lendemain; <br/> - `+ 2jours` : affiche les données de la journée courante et celles des 2 jours suivants; <br/> - `1 semaine` : affiche les données de la journée courante et celles des 6 jours suivants; <br/>_**Remarque:**_ le nombre de jours proposés dépend de la valeur sélectionnée au niveau de l'option "Période à traiter". |
| Ne pas afficher le nombre d'évènements | Checkbox | Permet de masquer le nombre d'évènements affichés à côté du nom du calendrier. |

**Actions et Informations de synchro**

| Paramètre | Description |
|--|--|
| Paramètre (roue crantée) | Permet de définir les options "Jeedom" de la commande. |
| Tester | Permet de tester la commande (affiche le contenu de la commande). <br/> _**Remarque :**_ la donnée s'affiche uniquement après un 1er rafraîchissement. |
| Supprimer | Permet de supprimer la commande et les commandes rattachées (si agenda sur plusieurs jours).
| Date du fichier | indique la date du dernier téléchargement et sauvegarde en cache du fichier ics. <br/> _**Remarque:**_ lors d'une synchronisation, le fichier peut ne pas être sauvegardé en cache, si les 2 fichiers sont identiques. <br/> Un bouton "télécharger", vous permet de récupérer le fichier actuellement en cache pour une lecture locale sur votre poste de travail. |
| Date synchro précédente | indique la date de la dernière synchronisation entre Jeedom et votre agenda ics. |
| Date synchro suivante | indique la date de la prochaine synchronisation entre Jeedom et votre agenda ics. <br/> _**Remarque:**_ si la valeur est "STOP", cela signifie que votre équipement est désactivé. |


### -- Exemple d'un écran listant les noms des agendas CalDav 

![CalDav](https://abarrau.github.io/jeedom-plugins-doc/iCalendar/images/iCalendar_caldav1.png)
<br/>


## # Présentation du Widget

Le widget se présente sous la forme suivante, si aucun style n'est appliqué :

![widget1](https://abarrau.github.io/jeedom-plugins-doc/iCalendar/images/iCalendar_screenshot1.jpg) 
<br/><br/>
![widget2](https://abarrau.github.io/jeedom-plugins-doc/iCalendar/images/iCalendar_screenshot6.jpg) &nbsp;&nbsp;
![widget3](https://abarrau.github.io/jeedom-plugins-doc/iCalendar/images/iCalendar_affichagetoutesjournees.png)


**Au niveau d'un calendrier :**
* Le nombre d'événements est affiché à côté du titre du calendrier ;
	* En passant la souris sur le titre de l'agenda : affiche le type d'affichage, ainsi que les dates de collecte et de valeur ;
* Les évènements passés sont grisés ; 
* Les évènements en cours sont repérés par une icône "Actif" (mais aussi 1ère minute et dernière minute, si l'option est active) ; 
* Les évènements à venir sont représentés sans indicateur ; 
* Les évènements identifiés avec des actions de type (Scénarios ou Actions) sont représentés par : (seulement si l'option "Autoriser les scénarios/actions" est activée) : 
	* Une icône "roues crantées" indique que l'événement déclenche des scénarios ou des actions ; 
		* en cliquant dessus, la liste des scénarios ou des actions configurés en début ou fin d'événement est affichée ; <br/> En cliquant une seconde fois, ou sur une autre roue la fenêtre d'information actuelle se masque ;
		* en cliquant sur le nom du scénario ou de l'action, la page de configuration s'ouvre ; 
		* une icône verte apparait à côté de l'action/scénario pour indiquer qu'il/elle a bien été exécuté(e) ; <br/> En passant la souris sur l'icône, il est possible de voir la date de traitement.
	* Une icône "bulle de BD" indique que l'événement peut déclencher une interaction ; 

La seconde image montre comment il est possible de personnaliser le widget en utilisant les class (cf. Annexe 6).

### -- Autres fonctionnalités :

* Le widget peut être redimensionné en largeur et hauteur, du moment que les tailles souhaitées soient supérieures à l'espace minimum prévu pour l'affichage des données. 
En cas de dimensionnement inférieur, un message d'erreur est affiché. 

* Vous pouvez également ré-ordonner les agendas directement via le widget (maintenez la souris enfoncée sur la zone de titre de l'agenda, et déplacez vers le haut ou le bas). 



## # Présentation du panel : avec liste des actions historisées et visualisation de l'agenda

Vous pouvez atteindre ce menu en sélectionnant le menu "Accueil", puis "iCalendar".

**Visualisation de l'agenda :**

![agenda](https://abarrau.github.io/jeedom-plugins-doc/iCalendar/images/iCalendar_screenshot8.jpg) 

Après avoir sélectionné un agenda, vous pouvez cliquer sur le type d'affichage souhaité "Calendrier" (bouton en haut à gauche).
Vous pouvez alors parcourir votre agenda comme si vous étiez sur la version "distante" (Google, etc...).
La période d'affichage est toutefois restreinte ; elle respecte la plage suivante : les 3 mois précédant la date du jour et les 6 mois suivants.

_**Remarque:**_ Cette période n'est pas paramétrable pour l'instant; elle est juste rappelée en haut à droite de l'écran.
Dans le cas de petites configurations, le temps d'affichage de cet écran peut être long la 1ère fois de la journée, un cache est ensuite utilisé tout au long de la journée.

En cliquant sur un événement, une fenêtre apparaît, permettant d'avoir des détails complémentaires.

![agenda](https://abarrau.github.io/jeedom-plugins-doc/iCalendar/images/iCalendar_screenshot10.jpg) 


**Actions historisées :**

![action](https://abarrau.github.io/jeedom-plugins-doc/iCalendar/images/iCalendar_screenshot9.jpg) 

Si vous avez activé "Historiser les actions", vous pourrez retrouver dans cet écran les actions/scénarios/interactions pour lesquel(le)s une tentative d'exécution a été traitée. 
En haut à droite, vous pouvez définir la période de visualisation ; par défaut, les derniers jours. 

La liste présente par jour, le nom du scénario ou de l'action traitée, avec son heure de traitement.
La dernière colonne permet d'avoir des informations sur l'événement associé / ayant demandé le lancement de cette action ou ce scénario.
Dans le cas d'une interaction, l'information affichée correspond à la "réponse" retournée par l'interaction (mais en aucun cas son nom) ; si aucune réponse n'a été faite, il est indiqué "Non reconnu".

En dessous de la date, vous pouvez supprimer les données historisées pour cette journée. 



## # Utilisation des données

* Par configuration d'un événement avec valeur des "scénario/action" dans la description de l'événement :
Les scénarios et les actions/commandes (si leur id est valide et actif) sont lancés automatiquement à l'heure souhaitée. 

* Par déclencheur dans un scénario :
Dans une condition IF, il faut rechercher la présence du nom de l'évènement ; on peut aussi le faire précéder de l'état. 
La recherche se fait en utilisant l'argument de comparaison "contient" ("matches", cf. documentation scénario).

| Nom uniquement | recherche de la présence d'un nom : cmd_iCal matches "/mon event/" <br/> _exemple : \#[MA_CMD]# matches "/déjeuner/"_ |
| Etat actif  | recherche d'un état actif pour un événement précis : cmd_iCal matches "/A;mon event/" <br/> _exemple : \#[MA_CMD]# matches "/A;Volet RDC/"_ <br/> _**Remarque :**_ ce test contient aussi les états des 1ères et dernière minutes ; pour ne pas en tenir compte, il faut écrire : <br/> _\#[MA_CMD]# matches "/;A;Volet RDC/"_ |
| Etat actif : 1ère minute | recherche de la 1ère minute d'un état actif pour un événement précis : cmd_iCal matches "/;DA;mon event/" <br/> _exemple : \#[MA_CMD]# matches "/;DA;Volet RDC/"_ |
| Etat actif : dernière minute | recherche de la dernière minute d'un état actif pour un événement précis : cmd_iCal matches "/;FA;mon event/" <br/> _exemple : \#[MA_CMD]# matches "/;FA;Volet RDC/"_ <br/> _**Remarque :**_ La borne de fin sera configurée 1 minute avant l'heure configurée (exemple pour 18h, l'indicateur sera affiché à 17h59); sauf pour 23h59. |

En fonction de la version de Jeedom, l'utilisation des doubles côtes `"`, autour du nom de la commande peut être nécessaire.

L'utilisation de l'état n'a un intérêt que si le paramètre "Format donnée" utilisé est : "événement heure à venir" ou "événement sur la journée".

_**REMARQUE:**_ Lorsque l'agenda ne traite qu'un seul événément, l'utilisation du format "événement courant" avec "titre uniquement" n'est pas la seule solution. 
Vous pouvez très bien utiliser également les formats "heure à venir" et "journée", en précisant le contenu exact de l'événement. 
Soit un `\#[MA_CMD]#="Congé"` en "événement courant", équivaut à `\#[MA_CMD]# matches "/;A;Congé;/"` dans un autre format (respectez bien l'utilisation des `;`).



## # Cron et Rafraîchissement de données

**-- Récupération des données :** 
Les données récupérées correspondent à une journée complète, mais sont récupérées en fonction du paramétrage défini (minimum 30 minutes); elles sont enregistrées par le cache utilisé par le plugin.
Si vous faites des modifications dans votre agenda ics, celles-ci ne seront visibles qu'au moment d'une période de rafraîchissement.
<br/>

**-- Cron :** 
Le système vérifie toutes les minutes en cache s'il y a des évènements, et précise l'état de l'évènement (en fonction du format choisi).
Il est donc possible de configurer/programmer des évènements à la minute près.

En l'absence d'accès internet, le cache disponible est sur l'ensemble de l'agenda configuré (et non uniquement sur la journée courante).


## # "Santé" des échanges réseaux

Afin de vous permettre d'avoir une vision sur la validité des synchronisations, une information est remontée au niveau de la page "Santé".
Dans la session "iCalendar", vous pouvez voir pour chacun de vos agendas, l'état des 15 dernières synchronisations réalisées :
* Si la synchronisation s'est correctement déroulée, un `o` est affiché.
* Si la synchronisation a rencontré un problème réseau (non accès à l'URL), une `X` est affichée.

![sante](https://abarrau.github.io/jeedom-plugins-doc/iCalendar/images/iCalendar_screenshot7.jpg) 

L'ordre de lecture de ces états est le suivant : le 1er de la liste correspond au test de synchronisation, le dernier en date ; la dernière information de la liste correspond à l'état le plus ancien connu.
Ces états sont renseignés à chaque synchronisation (soit à chaque période définie dans votre configuration de l'équipement, ou au moment de l'enregistrement de l'équipement si vous avez forcé la synchronisation).


## # Annexes

#### --- _Annexe 1 : Aide à la saisie d'un évènement "Action" (scénario ou commande action) dans votre agenda_

Ce paragraphe vous explique comment configurer un évènement agenda pour permettre de lancer automatiquement les scénarios ou des commandes actions. 
Pour que le plugin reconnaisse que l'évènement est de type "Action", il doit se présenter sous une forme particulière au niveau du champ "description" de l'événement.

**-- Cas du format "Scénario" :** 

Le format attendu doit être du type : `période (DA ou FA)|sc=id du sénario|nom de la variable=valeur de la variable`.
_exemple : `DA|sc=3|varVolet=ON`_ , pour action à la 1ère minute (DA), lancement du scénario id="3", et passage de variable au scénario (variable "varVolet", avec la valeur "ON").

Il est aussi possible d'activer ou désactiver un scénario par ce procédé ; ces valeurs sont présentes en fin de liste des choix "nom de la variable".
En saisie manuelle, mettre : "#active" pour activer le scénario ou "#desactive" pour désactiver le scénario.
Par contre, ne pas mettre de valeur de variable pour que cette action soit prise en compte.
_exemple : `DA|sc=3|#active`_
_**Remarque:**_ ces 2 actions ne permettent pas de lancer le scénario, mais juste d'agir dessus.

![aide](https://abarrau.github.io/jeedom-plugins-doc/iCalendar/images/iCalendar_screenshot4.jpg) 

| Champs | Description |
|--|--|
| Type d'action | Définit le type d'action à produire (commande action ou scénario), ici "Scénario" |
| 1ère minute : nom du scénario | Sélectionner le scénario à exécuter depuis l'évènement à la 1ère minute. |
| 1ère minute : nom de la variable | Sélectionner le nom de la variable à utiliser pour un traitement au niveau du scénario ; cette variable sera utilisée pour faire transiter les informations définies au moment de la 1ère minute. <br/> _Valeur non obligatoire, si vous n'avez pas besoin de passer de paramètre_  <br/> _**Remarque :**_ la variable doit être créée avant l'utilisation de l'aide (pour apparaître dans la liste des variables). |
| 1ère minute : valeur de la variable | Valeur à passer à la variable lors du démarrage de l'événement (1ère minute), lors de l'état <span style="background-color:yellow;">#;DA;#</span>. <br/> _Valeur non obligatoire. Exemple : ON_ |
| dernière minute : nom du scénario | Sélectionner le scénario à exécuter depuis l'évènement à la dernière minute. |
| dernière minute : nom de la variable | Sélectionner le nom de la variable à utiliser pour un traitement au niveau du scénario ; cette variable sera utilisée pour faire transiter les informations définies au moment de la dernière minute. <br/> _Valeur non obligatoire, si vous n'avez pas besoin de passer de paramètre_  <br/> _**Remarque :**_ la variable doit être créée avant l'utilisation de l'aide (pour apparaître dans la liste des variables). |
| dernière minute : valeur de la variable | Valeur à passer à la variable à la fin de l'événement (dernière minute), lors de l'état <span style="background-color:yellow;">#;FA;#</span>. <br/> _Valeur non obligatoire. Exemple : ON_ |
| _valeur générée_ | Après avoir cliqué sur le bouton "Générer", cette zone représente la syntaxe générée en fonction des valeurs définies ci-dessus. <br/> Il est possible de lancer plusieurs sénarios à la 1ère minute ou dernière minute. <br/> Un bouton RAZ permet de remettre à vide la zone. |

**-- Cas du format "Action" :** 

Le format attendu doit être du type : `période (DA ou FA)|act=commande(id ou nom)|option de commande=valeur`.
_exemple : `FA|act=[obj][equipment][cmd]|slider=4`_ , pour action à la dernière minute (FA), lancement d'une commande action "cmd" de l'équipement "equipement", et passage de la valeur 4 (commande de type "slider"). 

_**Remarque :**_ les options de commande sont dépendantes de la commande utilisée et donc ne sont pas obligatoires. 

![aide](https://abarrau.github.io/jeedom-plugins-doc/iCalendar/images/iCalendar_screenshot5.jpg) 

| Champs | Description |
|--|--|
| Type d'action | Définit le type d'action à produire (commande action ou scénario), ici "Action" |
| Format de la commande | Définit si la valeur de l'ID est positionnée ou le format de commande Jeedom (soit [obj][equip][cmd]). _**Remarque:**_ avec l'id, vous n'êtes pas dépendant du nom de la commande ou de l'équipement. Toute modification sur ce dernier n'aura pas d'impact sur le traitement/l'action de la commande. |
| 1ère minute : commande action | Sélectionner le nom de la commande à utiliser à la 1ère minute. <br/> Si cette commande utilise des options (slider, titre/message), vous pourrez alors les compléter. |
| dernière minute : commande action | Sélectionner le nom de la commande à utiliser à la dernière minute. <br/> Si cette commande utilise des options (slider, titre/message), vous pourrez alors les compléter. |

**-- Opération à réaliser :**

* Une fois les informations renseignées, cliquez sur le bouton "Générer". 
* La zone grise est complétée, copiez là (ctrl + C).
* Collez (ctlr + V) l'information dans le champs DESCRIPTION d'un évènement de votre agenda.


#### --- _Annexe 2 : Fréquence de rafraîchissement_
	

| Valeur | Heure du rafraîchissement |
|--|--|
| 30 min. | Aux minutes : 00, 30, de chaque heure. |
| 1 h. | A la minute : 00, de chaque heure. |
| 3 h. | A : minuit (00h), 3h, 6h, 9h, 12h, 15h, 18h, 21h. |
| 6 h. | A : minuit (00h), 6h, 12h, 18h. |
| 12 h. | A : minuit (00h) et midi (12h) |
| 24 h. | Unique à minuit (00h) |

_**Remarque :** en dehors de ces horaires, aucun rafraîchissement n'est réalisé._


#### --- _Annexe 3 : URL privée des agendas Google_

Une fois connecté à l'agenda Google, vous pouvez récupérer l'*URL PRIVEE* de votre agenda comme ceci.
* Cliquez sur le nom de l'agenda que vous souhaitez récupérer sous Jeedom et choisir le menu "Paramètres de l'agenda" ;
* Allez à la session "Adresse URL Privée" et cliquer sur "ICS" ;
* La popup s'ouvre et présente l'URL à copier dans Jeedom ;


#### --- _Annexe 4 : Format des données (widget et structure des commandes)_

Lorsque la synchronisation est réalisée, le plugin va positionner au niveau de la commande agenda les informations des événements de votre calendrier pour la journée courante.

Il existe 2 formats : 

* version "simple" (diponible pour "événement courant", avec titre uniquement à OUI) : 
	* chaque évènement est séparé par des "\|\|" ; 
	* la donnée ne contient que les titres des événements, aucune autre information "technique" n'est présente dans la commande ; 

* version standard/complète (pour tout autre paramétrage) : 
	* chaque évènement est séparé par des "\|\|" ; 
	* les données au sein d'un évènement sont séparés par des ";" (point-virgule) ;
	* les données disponibles sont : 
		* `heure_début;heure_fin;statut;titre de l'événement;uid;doAct/doInter;date_update;location`
		* où heure_début, et heure_fin sont des bornes de l'événement pour la journée courante ; 
		* statut : définit l'état de l'événement à l'instant T; pouvant prendre les valeurs : vide (à venir), DA (1ère minute), A (actif) ,FA (dernière minute), P (passé) ; 
		* uid : est l'idée technique de l'événement (utilisée pour la liaison avec des données techniques en cache) ; 
		* doAct/doInter : définit si cet événement présente des commandes actions ou scénarios à exécuter en début ou fin d'événement ; ou une interaction en début d'événement.
		* date_update : correspond au timestamp update de l'événement ;
		* location : correspond au lieu de l'événement s'il est défini dans votre agenda.

**Remarque :**

Le plugin sait gérer différents formats d'évènements : 
* heure au sein d'une journée (ex : 23/02 de 10h à 11h) ;
* journée complète (ex : 23/02, généralement décrit 23/02 0h à 24/02 0h) : sera transformé en 23/02 0h-23h59 au niveau de la commande et du widget
* plusieurs journées (ex : 23-25/02) : sera transformé en fonction du jour : 23/02 0h-23h59 , 24/02 0h-23h59, 25/02 0h-23h59
* plusieurs journées avec horaire (ex : 23/02 à 10h et 25/02 à 14h) : sera transformé en fonction du jour : 23/02 10h-23h59, 24/02 0h-23h59, 25/02 0h-14h


#### --- _Annexe 5 : Données des évènements au niveau des scénarios via "fonctions"_

Pour rappel, une commande agenda retourne des données brutes respectant les formats de données décrits au niveau de l'annexe précédente.
Toutefois, une commande complémentaire est disponible au niveau de chaque "agenda", nommé `_nom de la commande agenda_ (ExecuteFunction-_idCommande_)`.
Cette commande disponible au niveau des scénarios est de type "message" et est composé d'un nom de fonction (titre) et d'argements (message).
Après avoir sélectionné cette commande dans une action de scénario, tapez la lettre "g" dans la zone "fonction", les fonctions disponibles apparaitront (avec en mémo, un rappel de l'utilisation au niveau des arguments).

_L'événement recherché ne peut être que sur la journée courante et doit être en cours ou à venir._ Les événements passés ne peuvent plus être analysés.

_Le titre passé en argument doit être exact_ également (exemple : absence) ; la fonction "contient" n'est pas encore mise en place.
Si plusieurs titres correspondent, le 1er est retourné.


| Fonction | Description | Arguments |
|--|--|--|
| getTimeStart | donne l'heure de début de l'événement choisi | 1/ `#title=xxx#` : le titre de l'événenement à rechercher, le texte doit être exact ; _exemple : title=Volet RDC_ <br/> 2/ `#date=xxx#` : format de retour pour la date (conforme à la configuration au niveau de Jeedom) les possibilités de format sont équivalentes à celles de php). ; _exemple : date=H:i:s ou date=d/m H:i_ ; par défaut, valeur retournée est au format timestamp. <br/>  3/ `#jour=xxx#` : jour à analyser (J1,J2, ...); par défaut, valeur retournée pour J0 |
| getTimeEnd | donne l'heure de fin de l'événement choisi | 1/ `#title=xxx#` : le titre de l'événenement à rechercher, le texte doit être exact ; _exemple : title=Volet RDC_ <br/> 2/ `#date=xxx#` : format de retour pour la date (conforme à la configuration au niveau de Jeedom) les possibilités de format sont équivalentes à celles de php). ; _exemple : date=H:i:s ou date=d/m H:i_ ; par défaut, valeur retournée est au format timestamp. <br/> 3/ `#jour=xxx#` : jour à analyser (J1,J2, ...); par défaut, valeur retournée pour J0 |
| getUid | donne l'id technique de l'événement choisi | 1/ `#title=xxx#` : le titre de l'événenement à rechercher, le texte doit être exact ; _exemple : title=Volet RDC_ <br/> 2/ `#jour=xxx#` : jour à analyser (J1,J2, ...); par défaut, valeur retournée pour J0 |
| getTitle | donne le titre de l'événement choisi en fonction d'un id | 1/ `#uid=xxx#` : l'id (uid) de l'événenement à rechercher, le texte doit être exact ; _exemple : uid=23424houi877sdf@google.com_ <br/> 2/ `#jour=xxx#` : jour à analyser (J1,J2, ...); par défaut, valeur retournée pour J0 |
| getLocation | donne le lieu de l'événement choisi en fonction d'un id ou d'un titre | 1/ `#title=xxx#` : le titre de l'événenement à rechercher, le texte doit être exact ; _exemple : title=Volet RDC_ <br/> 2/ `#jour=xxx#` : jour à analyser (J1,J2, ...); par défaut, valeur retournée pour J0; <br/> (un id peut aussi être passé en paramètre; exemple: uid=23424houi877sdf@google.com) |
| getDaySimple | retourne une trame simplifiée de tous les événements de la journée courante (quelque soit le statut de l'événement). <br/> Le contenu est : l'heure de début, l'heure de fin et le titre. | 1/ `#jour=xxx#` : jour à analyser (J1,J2, ...); par défaut, valeur retournée pour J0 |
| getDayTitleOnly | retourne une trame simplifiée avec tous les événéments de la journée courante (quelque soit le statut de l'événement). <br/> Le contenu est : uniquement le titre. <br/> _**Remarque:**_ cette fonction correspond à la même chose que l'option "titre uniquement", mais ici valable sur toute la journée. | 1/ `#jour=xxx#` : jour à analyser (J1,J2, ...); par défaut, valeur retournée pour J0 |
| getDayActifOnly | retourne une trame simplifiée avec uniquement les événéments actifs de la journée courante. <br/> Le contenu est : l'heure de début, l'heure de fin et le titre. <br/> _**Remarque:**_ cette fonction correspond à la même chose que l'option format donnée = "événement courant". | aucun (zone laissée vide) |
| getDayActifAndTitleOnly | retourne une trame simplifiée avec uniquement les événements actifs de la journée courante. <br/> Le contenu est : uniquement le titre. <br/> _**Remarque:**_ cette fonction correspond à la même chose que l'option format donnée = "événement courant" et "titre uniquement". | aucun (zone laissée vide); |

_**Remarque:**_ L'ordre des arguments n'a pas d'importance; par contre, chaque argument doit être disposé sur une ligne différente et respecter le format défini. 

Les commandes actions ne retournent pas de valeur, le résultat de la fonction sera donc placé dans une variable de scénario, prenant la forme : `nomDeLaFonction_IdCommandeAgenda` (exemple: getTimeStart_13456).
Pour éviter toute erreur, cet id est rappelé dans le nom de la commande fonction.

Par ailleurs, le traitement étant asynchrone, tout au long du traitement de la commande/fonction la variable de retour est positionnée à "-99".
Dès lors que cette variable passe à une autre valeur, cela signifie que la fonction a terminé son traitement.

Si la fonction n'a rien trouvé ou a rencontré une erreur, la valeur de retour de non traitement est "-1".

**Remarque pour les fonction "getDay...":** 

1/ pour l'utilisation de ces fonctions, il est conseillé d'être dans un format de données différent de "événement courant". 
En effet, ce format étant déjà très limité, ces fonctions spécifiques de formatage de la trame pourraient ne pas s'appliquer.<br/>
Si ce cas s'applique, le retour prendra la valeur "-1" et un message d'erreur sera précisé dans le log.<br/>
2/ le séparateur entre les événements est un double pipe "&#124;&#124;". <br/>
Si vous souhaitez utiliser un autre séparateur pour de l'affichage dans  un mail par exemple, vous pouvez faire un changement de caractère comme suite (ici retour à la ligne) : <br/>
`str_replace("&#124;&#124;", "\n", variable(getDaySimple_123))`

 
**Processus d'utilisation dans un scénario :**

* 1/ Sélectionner votre commande agenda permettant d'exécuter des fonctions au niveau d'une zone "action".
* 2/ Dans la zone "fonction", taper "get" et sélectionner dans la liste la fonction souhaitée (cf. ci-dessus).
* 3/ Ajouter une commande action avec la fonction "wait" ; <br/>
**Remarque:** les temps de réponse des fonctions sont relativement rapides, mais il est préférable d'avoir une tempo pour s'assurer que la valeur retournée est bien celle attendue, pour la suite du scénario. 
La saisie doit être du type : `variable(getTimeEnd_12345) != -99` , (avec un timeout de 5sec par exemple).
* 4/ une fois cette condition passée, vous pouvez utiliser votre variable dans la suite du scénario. <br/>
**Remarque:** Il est conseillé de faire d'abord un test sur la pertinence de votre variable : autre que "-1".


![scenario](https://abarrau.github.io/jeedom-plugins-doc/iCalendar/images/iCalendar_scenarioFonction.png) 


#### --- _Annexe 6 : Les classes CSS disponibles_

Vous pouvez utiliser 3 paramètres au niveau des options de la tuile de l'agenda pour gérer les couleurs : 

| bgTitleColor | Couleur de fond de la zone de titre (nom de l'agenda, et zone actions) |
| bgItemColor | Couleur de fond de la zone de liste (événements et actions) |

Mais pour les utilisateurs qui veulent aller plus loin dans la configuration, voici les classes CSS disponibles pour personnaliser le widget du plugin : 

| iCalendar_title | Zone de titre de la tuile |
| iCalendar_date | Zone de date de la tuile |
| iCalendar_calTitle | Zone de titre de l'agenda |
| iCalendar_items | Zone d'information principale |
| iCalendar_itemActif | évènement "Actif" (en cours) |
| iCalendar_itemInactif | évènement "Inactif" (passé ou à venir) |
| iCalendar_zoneListAct | Sur fenêtre affichant la liste des actions / scénarios |
| iCalendar_titleListAct | Zone de titre de la liste des actions / scénarios |

**Remarque :** avec tous les changements d'ergonomie apportée avec la V4, ces class peuvent ne plus fonctionner correctement. Il est donc préférable d'utiliser les fonctions proposées par Jeedom. 

# FAQ

#### --- _Peut-on visualiser les futurs évènements ?_
Avec les valeurs "événement heure à venir" et "événement sur la journée" du paramètre "format donnée" : oui d'un point de vue affichage sur le widget. <br/>
Par contre, le traitement de futurs évènements n'est pas possible (ils ne sont présents qu'en terme d'affichage), sauf si vous parsez les informations. 

#### --- _J'ai modifié mon agenda et l'évènement n'apparaît pas..._
Le rafraîchissement du cache est réalisé en fonction du paramétrage que vous avez configuré (minimum 30 min). 
Toutes modifications sur l'agenda n'apparaîtront sur le plugin iCalendar qu'aux heures fixes liées à la configuration définie (cf. doc). <br/>
Mais il est possible de forcer cette synchronisation au moment de l'enregistrement de l'agenda (équipement).

#### --- _Quelle période de l'agenda est affichée dans le widget ?_
La récupération des données et l'affichage dans le widget ne traitent que des données de la journée courante.
Si l'évènement fait plus d'une journée, les heures de début et de fin sont présentées uniquement pour la journée en cours. 
_(exemple si l'évènement est configurée sur jour1 10h - jour2 10h; le jour 1, il sera affiché: 10h-23h59 et jour2: 0h-10h)_ 
Même pour une configuration en "heure suivante", les informations seront affichées uniquement jusqu'à 23h59.

#### --- _Les bornes sont-elles incluses ?_
L'heure de début est incluse : la 1ère minute est "active" et remonte l'information <span style="background-color:yellow;">#;DA;#</span> (exemple: 10h-18h: 10h00 contient <span style="background-color:yellow;">#;DA;#</span>) <br/>
L'heure de fin n'est pas incluse dans la période d'activité, c'est la dernière minute précédente qui présente l'information <span style="background-color:yellow;">#;FA;#</span> ; sauf pour 23h59. <br/>
* _exemple 1:_ 10h-18h: 17h59 contient <span style="background-color:yellow;">#;FA;#</span>, à 18h00 l'évènement est terminé et non actif, <span style="background-color:yellow;">#;A;#</span> n'est plus présent. <br/>
* _exemple 2:_ 19h-0h: l'heure de fin est convertie en 23h59 et contient [yellow-background]#;FA;#</span>, à 0h l'évènement est terminé et non actif, [yellow-background]#;A;#</span>n'est plus présent.

#### --- _Sur la version mobile, je ne vois pas les évènements passés en affichage journée..._
Sur la version mobile, seuls les évènements en cours et à venir sont affichés. Même en mode journée, les évènements passés ne sont plus affichés (contrairement à l'affichage dashboard).

#### --- _J'ai des messages d'erreur du type "La commande action : [objet][equipement][cmd], est inconnue pour l événement suivant : mon titre événement. Revoir la configuration de votre événement" qui s'affiche au niveau de la messagerie Jeedom ?_
L'id ou le nom de la commande, ou l'id du scénario que vous déclaré en tant qu'action dans votre événement n'existe pas (ou plus) dans Jeedom. <br/> 
Vous devez vérifier si vous n'avez pas modifié cette commande/scénario et faire la modification dans votre événement au niveau de votre agenda.

#### --- _Existe-il un agenda des jours fériés ?_
Oui il existe un agenda google qui liste les jours fériés, l'URL est la suivante (ici pour la France) : 
[https://calendar.google.com/calendar/ical/fr.french%23holiday%40group.v.calendar.google.com/public/basic.ics](https://calendar.google.com/calendar/ical/fr.french%23holiday%40group.v.calendar.google.com/public/basic.ics) <br/>
**Remarque :** par contre, ce calendrier présente aussi des évènements (comme la fête des mères) qui ne sont pas des jours fériés ... :(


#### --- (?) _Mes scénarios réagissent à des évènements passés ou futurs (mode prochaine heure ou journée)_
Dans l'analyse de la trame, il faut vérifier que vous êtes sur un évènement actif; en vérifiant que <span style="background-color:yellow;">#;A;#</span> est présent. _(exemple : "..." matches "/;A;mon event/")_.
Voir la documentation pour plus d'explications.


## ?? Pourquoi ce plugin ??

A l'origine, Google permettait d'échanger les données au format csv ; je participais au développement du plugin officiel gCalendar. <br/>
Lorsque Google a arrêté cette fonction au profit du format iCal (ics), Jeedom a arrêté le plugin gCalendar. J'ai donc créé le plugin iCalendar en remplacement. 

Son objectif était d'automatiser des actions en les configurants dans un calendrier accessibles à tous au sein d'une famille (via google). 

Bonne utilisation ....
