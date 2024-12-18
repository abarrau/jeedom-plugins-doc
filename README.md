## Doc des plugins pour Jeedom abarrau/olindote

### -- INFORMATION IMPORTANTE au 18/12/24 : 
* Les différentes évolutions du core de jeedom impactent fortement le développement des plugins.
* Après avoir analysé le travail à faire pour me mettre à niveau, une grosse partie du code iCalendar et DaikinOnlineCtrl se trouve au niveau de l'appli coté utilisateur (donc Javascript/JQuery).
* J'ai cherché du temps que je n'ai pas trouvé sur l'année 2024 (entre le pro et le perso), pour mettre à niveau mes 3 plugins, et je ne vois pas de perspective pour 2025.
* J'ai donc décidé de ne plus faire de montée de version du core Jeedom sur mon propre environnement.
* C'est donc avec regrêt que mes 3 plugins ne seront plus mis à jour et donc plus compatibles avec Jeedom 4.4.x (dernière version testée 4.4.1).
* Je suis désolé de cette situation et sachez que j'en suis également pénalisé ; merci pour votre confiance sur ces dernières années. Aurélien - 18/12/24

### -- Documentation (FR uniquement) : 
* olindoteTools (class) : https://abarrau.github.io/jeedom-plugins-doc/class-olindoteTools/
* iCalendar : https://abarrau.github.io/jeedom-plugins-doc/iCalendar/
* DaikinOnlineCtrl : https://abarrau.github.io/jeedom-plugins-doc/DaikinOnlineCtrl/
* ttsWebServer : https://abarrau.github.io/jeedom-plugins-doc/ttsWebServer/

### -- ChangeLog : 
Les informations de changelog sont disponibles via la documentation.

### -- Remontée de dysfonctionnement : 
* Ouverture de cas (menu "Issues") : https://github.com/abarrau/jeedom-plugins-doc/issues
* A lire en priorité : 
  * Lors de l'ouverture d'un dysfonctionnement, indiquer dans le titre le plugin concerné (exemple : [icalendar] xxxx) 
  * Toute analyse ne sera réalisée que si les informations sont clairement détaillées, avec présence de log : 
    * du plugin concerné (plusieurs fichiers possibles), le **http.error**
    * si le problème se présente sur des cas de cron : **cron_execution**
    * pour DaikinOnlineCtrl et drawMap : **listener_execution**
    * une capture écran du problème
    * une **description complète du cas**
  * si ces informations ne sont pas communiquées, le dysfonctionnement sera clos. 

Par ailleurs, je m'excuse d'avance, si l'avancée des corrections ne va pas à la vitesse que vous souhaitez.
