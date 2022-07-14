# Changelog

#### v1.4.1 (16/04/2022=BETA - STABLE=14/07) :
- correction (discution issue #66): problème de clic sur le 1er onglet du widget
- adaptation : mise à jour de tous les generic_type des commandes >> ATTENTION: si vous aviez fait des mises à jour, elles seront écrasées
- _class olindoteTools: 1.15_

#### v1.4.0 (26/03/2022=BETA) :
- correction (issue #83): bug erreur "internal 500" et mise à jour de la led depuis la page de config
- evolution (issue #67): permettre l'utilisation des commandes depuis le widget, lorsque clim éteinte
- evolution (issue #68): permettre l'affichage de consigne décimale
- correction (issue #66): mise à jour des icones pour être compatible v4
- suppression des fichiers de mise à jour (1.2.0 à 1.3.2)
- adaptation: version minimum jeedom = 4.0
- _class olindoteTools: 1.14_

#### v1.3.3 (28-31/03/2020=BETA - STABLE=4/04) :
- evolution: pour les mémoires, sélection d'une commande via variable (issue #55)
- correction: remonté des consommations, passage à heure fixe (issue #50)
- adaptation: affichage des catégories sur la page équipement
- correction: gestion de l'oeil (température positive en mode rafraichissement)


#### v1.3.1 (08-09/02/2020=BETA) :
- adaptation: compatibilité jeedom 4.x et php 7 et Debian10 (issue #49,#48)
- correction: /BUG en v1.3.0/ problème du json error 200 sur la page equipement
- _class olindoteTools: 1.12_
- _remise en forme de la doc au template olindote_

#### v1.2.3 (12/04/2019=BETA - STABLE=16/04) :
- correction: affichage du plugin sur panel l'appli web mobile (issue #41)

#### v1.2.2 (11/04/2019) :
- correction: paramètre d'affichage (makkil, issue #46)
- évolution: ajout des commandes info de conso d'énergie chaud/froid (T0urista, issue#6)
- adaptation: paramétrage d'affichage des éléments commande "info" (température, humidité, durée, énergie)
- adaptation: mise à jour class olindoteTools (1.08)

#### v1.2.1 (02/03/2019 - STABLE=05/03) :
- correction: installation/update
- adaptation: version minimum jeedom = 3.0

#### v1.2.0 (26/02/2019) :
- correction: anomalie du "fonction add() on null" (lié à jeedom 3.3.x)
- intégration: séparation de la class olindoteTools (1.05)
- correction/adaptation: diverses corrections et adaptations en lien avec la class olindoteTools.
- adaptation: refont de la doc au nouveau format jeedom (markdon)

#### v1.1.0 (03/07/2017) :
- correction: problème de l'icone qui n'apparait pas
- correction: divers problème lié au passage en v3.1 du core

#### v1.0.02 (29/10/2016) :
- correction: problème d'affichage sur les vues et design
- adaptation: sur le panel mobile, clic d'affichage de la configuration sur toute la ligne
- adaptation: revue de la gestion des widget en cache (utilisation uniquement de la fonction refreshWidget())

#### v1.0.01 (28/10/2016) :
- évolution: mise à niveau du plugin suite aux évolutions du code jeedom (2.4) 
  - prise en compte de la gestion des paramètres d'affichage des widgets
  - nouvelle ergonomie des écrans de paramétrage des équipements
- évolution: création du template "mobile"
- évolution: création du panel "mobile" (réplique application android Daikin)
- évolution: configuration des commandes pour l'affichage dans l'application "mobile" (penser à activer le plugin "Daikin Online Ctrl" dans le plugin "App mobile")
- évolution: ajout de la fonction "dupliquer" d'un équipement
- correction: lors de la création des commandes "oeil intelligent"
- correction: bouton on/off

#### v0.1.14 (24/10/2015) :
- correction: gestion activation/desactivation de l'oeil intelligent, lorsqu'il y a utilisation de la télécommande

#### v0.1.13 (22/10/2015) :
- correction : reprise des textes sur la partie "problèmes réseaux et non accessibilité du module" ;
- évolution : affichage de la courbe historique sur les 2 sondes de température depuis le widget ;
- évolution : mise en marche automatique de la clim si lancement d'une commande "consigne", "powerful" ou "mémoire" depuis l'appel via un scénario ;
- évolution : "oeil intelligent"/présence : version simulée ; utilisation d'une commande extérieure jeedom ;
- ajout : des ° +3,5 et +4 pour l'offset sur l'indicateur de la sonde intérieur ;

#### v0.1.12 (12/10/2015) :
- évolution : ergonomie des boutons du widget (même ergonomie que jeedom) ; 
- évolution : ajout du mode powerful ; paramètre configurable (durée, température offset, température référence)
- évolution : mise en place d'une action "soignée les modules" (action testée toutes les 30mins ; si état est "err=255" > reboot du module)
- évolution : ajout de l'état des 20 dernières requêtes vers le module sur la page "santé" + affichage de l'erreur sur le widget

#### v0.1.11 (08/08/2015) :
- correction : fonction cron(), suite à évolution du cron jeedom en 1.203.0.47
- correction : affichage du mode "auto" qui disparaissait sur le widget; 
- évolution : possibilité d'historiser le temps d'utilisation;
- évolution : meilleure gestion des options des commandes sur la page de config;
- évolution : simulation de la fonction powerfull (EN BETA ; désactivée au niveau widget, ne pas utiliser via les scénario sans accord)
- doc : mise à jour de la partie "association module wifi"
