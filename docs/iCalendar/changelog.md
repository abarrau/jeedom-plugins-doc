# Changelog

#### v1.5.1 (17/01/2020=BETA - STABLE=?) :
- adaptation: compatibilité jeedom 4.x et php 7 (correction #21,#20)
- correction/adaptation: diverses corrections (page panel: affichage du détail des évènements, liste des actions)
- class olindoteTools: 1.11

#### v1.4.0 (07/03/2019 - STABLE=11/03/2019) :
- correction: anomalie du "fonction add() on null" (lié à jeedom 3.3.x)
- intégration: séparation de la class olindoteTools (1.07)
- correction/adaptation: diverses corrections et adaptations en lien avec la class olindoteTools.

#### v1.3.0 (14/10/2017) : 
- correction: sur la gestion des fichiers temporaires pour l'affichage du calendrier (ano de KiwiHC16)
- correction: affichage en "double" d'un évènement récurant déplacé
- correction: gestion des fonctions complémentaires par le scénario
- évolution: permettre aux fonctions complémentaires d'utiliser des J+x (et pas uniquement le J courant)
- adaptation: toutes les variables de config passent avec un prefixe "olindote::"
- adaptation: arrêt des messages d'erreur en cas de "resize" du widget
- adaptation: mise à niveau du javascript de la page équipement (suppression des appels depuis le "$('body').")
- adaptation: met à jour systématiquement le widget
- mise à niveau: suppression des corrections datant de plus d'un an (v0.1.00, v0.1.02, v1.0.01)
- correction: correction orthographique de la documentation (merci noodom)

#### v1.2.0 (19/06/2017) : 
- correction: sur la "santé" des requêtes pour les calendriers "caldav" (ano #2 de KiwiHC16)
- adaptation: prise en compte des évolutions de jeedom (json)
- évolution: page "santé", en plus des états, l'heure de l'action est disponible (en passant la souris dessus)
- évolution: ajout de l'option d'affichage "multi date"
- évolution: intégration de la class "olindote" 
- évolution: séparer les log par calendrier (plus facile a débuguer en mode "debug")
- mise à niveau de la documentation

#### v1.1.00 (18/10/2016) : 
- adaptation: mise à niveau compatibilité jeedom : gestion des paramètres d'affichage de la tuile 
- adaptation: mise à niveau compatibilité jeedom : onglet sur le paramétrage des équipements et suppression bootstrap swtich)
- évolution: autoriser le redimensionnement automatique de la tuile au cas où les événements dépassent la hauteur de la tuile
- évolution: passage en 3.0.1 pour la librairie du calendier (panel)
- correction: affichage du calendrier sur le mobile
- correction: problème de d'indicateur de fin d'événement "FA" (cf. correction "rafdulaf")

#### v1.0.05 (xx/03/2016) : 
- correction: modification d'un événement au sein d'un événement récurant
- correction: lancement des actions par l'événement
- correction: gestion des téléchargements de fichier via HTTPS
- correction: dernière journée d'un événement récurant non visible 
- adaptation: option "autoriser action/scénario" redescendue au niveau de la commande
- adaptation: corrections liées à la v2 (nodejs, table cache)
- refonte: gestion des actions (géré par l'heure, et non plus par les DA/FA; évite les pertes d'événements sur les configurations lentes (mini))
- refonte: de la page de configuration des commandes
- évolution: lecture des agendas "CalDav" (avec cache sur la période de synchro)
- évolution: ajout d'un panel, permettant l'affichage du calendrier et le suivi des actions
- évolution: gestion d'un mode "rattrapage" pour les actions des événements non traités à l'heure dite
- évolution: affichage d'une information dans message lorsqu'une action est réalisée
- évolution: affichage du lieu de l'événement
- évolution: permet d'activer/desactiver un scénario ou action par l'action sur événement
- évolution: affichage des agendas en ligne sur le dashbord
- suppression: arrêt de la gestion des anciennes trames (via le titre)

#### v0.1.03 (30/12/2015) : 
- correction : gestion du bouton "ajouté" (régression lors de la création d'un nouvel équipement) ;
- correction : journée sur l'année suivante vue comme "passée" ;

#### v0.1.02 (29/12/2015) : 
- correction : gestion du rafraîchissement du widget en cas de changement de nom de l'agenda ;
- évolution : ajout du bouton dupliqué au niveau de l'équipement ;
- évolution : ajout d'une commande "fonction" permettant de remonter des informations sur un événement donné au sein des scénarios (cf. doc).

#### v0.1.01 (25/12/2015) : 
- correction : gestion des jours récurants dans lesquels 1 jour est supprimé (exclusion) ; 
- correction : gestion des journées complètes (minuit-minuit) ; 
- correction : de l'affichage de l'information sur la suppression des trame action dans le titre ; 
- correction : sur la récupération du titre de l'agenda dans le fichier ics ; 
- correction : gestion des urls en "webcals", remplacée par des "http" ;
- correction//évolution : ajout d'une option (titre uniquement) pour gérer la trame "simple" dans la commande ; (très attendu, car format abandonné en 0.1.00 et bcq de personnes l'utilisaient encore). 
- évolution : gestion de l'agenda sur 1 semaine : 1 commande par jour. (plusieurs options disponibles : jour courant, j+1, J+2 ou 1 semaine). 
- évolution : gestion 3 options graphiques au niveau de la tuile de l'équipement (cf. doc)

#### v0.1.00 (9/12/2015) : 
- correction: gestion du timezone
- correction: erreur DEND non définie
- évolution: widget dashboard et mobile
- évolution: changement de la gestion des événements "action" par le champs description, à la place de titre 
- évolution: lancement automatique d'actions en début et fin d'événement (en plus des scénarios)
- documentation: création de la documentation

#### v0.0.2 (16/11/2015) : 
- correction: gestion de la class commune avec le plugin "Info du jour"
- correction: gestion de la suppression des fichiers cache du répertoire temporaire lors de la désinstallion du plugin (si le répertoire n'est pas vide)
