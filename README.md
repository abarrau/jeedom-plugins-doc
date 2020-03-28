## Doc des plugins pour Jeedom abarrau/olindote

### -- Documentation (FR uniquement) : 
* olindoteTools (class) : https://abarrau.github.io/jeedom-plugins-doc/class-olindoteTools/
* iCalendar : https://abarrau.github.io/jeedom-plugins-doc/iCalendar/
* DaikinOnlineCtrl : https://abarrau.github.io/jeedom-plugins-doc/DaikinOnlineCtrl/
* ttsWebServer : https://abarrau.github.io/jeedom-plugins-doc/ttsWebServer/
* drawMaps : https://abarrau.github.io/jeedom-plugins-doc/drawMaps/

### -- ChangeLog : 
Les informations de changelog sont disponibles via la documentation.

### -- Remontée de dysfonctionnement : 
* Ouverture de cas (menu "Issues") : https://github.com/abarrau/jeedom-plugins-doc/issues
* A lire en priorité : 
  * Lors de l'ouverture d'un dysfonctionnement, indiquer dans le titre le plugin concerné (exemple : [icalendar] xxxx) 
  * Toute analyse ne sera réalisé que si les informations sont clairement détaillées, avec présence de log : 
    * du plugin concerné (plusieurs fichiers possibles), le **http.error**
    * si le problème se présente sur des cas de cron : **cron_execution**
    * pour DaikinOnlineCtrl et drawMap : **listener_execution**
    * une capture écran du problème
    * une **description complète du cas**
  * si ces informations ne sont pas communiquées, le dysfonctionnement sera clos. 

Par ailleurs, je m'excuse d'avance, si l'avancé des corrections ne va pas à la vitesse que vous souhaitez.
