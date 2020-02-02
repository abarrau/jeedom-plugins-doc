# Changelog

#### v1.3.1 (26-29/01/2020-BETA & STABLE-02/02/2020) :
- <span style="color:red;">Arrêt des commandes Squeezebox du plugin ttsWebServer; PREVOIR la migration vers les commandes Squeezebox directement intégrée au plugin Squeezebox.</span>
- correction: limitation des noms de commandes à 120 caractères
- correction: compatibilité debian 10 (avconv <> ffmpeg)
- _class olindoteTools: 1.12_

#### v1.2.2 (26/08/2019-BETA & STABLE-03/09/2019) :
- correction: compatibilité PHP 7.3 (object > jeeObject)
- evolution: ajout du bouton "rafraichir" sur la page "info" de l'équipement

#### v1.2.1 (24/08/2019-BETA) :
- correction: récupération des logs depuis l'équipement Android distant
- adaptation: compatibilité Jeedom V4.x
- intégration: mise à jour de la class olindoteTools (1.10)
- évolution: nouvelle version de l'APK (1.5): 
  - compatibilité Android SDK:27+ (ano NetworkOnMainThreadException)
  - suppression des retours à la ligne dans les retours en format json (remplacé par %%NR%%)

#### v1.2.0 (24/06/2019-BETA & STABLE) :
- correction: anomalie du "fonction add() on null" (lié à jeedom 3.3.x)
- correction: anomalie de diffusion sur Enceinte "Sonos"
- adaptation: version minimum jeedom = 3.0
- intégration: séparation de la class olindoteTools (1.09)
- adaptation: suppression de la gestion par adresse Mac (uniquement l'adresse IP)
- évolution: nouvelle version de l'APK (1.4): 
  - refonte pas d'accueil ;
  - page de réécoute des fichiers audio en cache et affichage des délais de traitement
  - changement de la gestion de génération d'un fichier TTS (trigger android et non délais d'attente)

#### v1.1.0 (12/08/2017) :
- évolution: ajout des commandes "batterie", "statut" et "relance WS" sur les équipements locaux (tablette)
- évolution: ajout de l'option "visibilité" sur les commandes sur l'équipement master (Server TTS WS)
- évolution: ajout de la suppression des fichiers où la date d'utilisation est "plus ancienne que ..."
- évolution: ajout de la commande "suppresion masse" depuis la page bibliothèque
- évolution: ajout du paramètre "format" dans la fonction getAudioFile() pour les plugins Tiers et intégration du codec opus(ogg)
(- évolution: sauvegarde du répertoire du plugin (fonctionnalité en réflexion))

#### v1.0.1 (18/07/2017) :
- évolution: ajout des fonctions pour plugin tiers (getAudioFile() et getVoicesList(), cf. API sur github)
- évolution: ajout de la recherche de fichiers orphelins

#### v1.0.0 (22/05/2017) :
- documentation: création de la document
- adaptation: suppression du bouton "dupliquer" (un équipement)
- correction: corrections diverses pour permettre l'utilisation du WS TTS pour Windows (projet transverse)

#### v0.2.1 (19/05/2017) :
- correction: ajout du "succeeded" pour les retours (NC) pour la découverte
- évolution (jeedom): suppression des includes dans le info.json et ajout des class includes dans le fichier de class
- évolution: permet de débrider l'affichage des boutons (ajouter/découverte)
- correction: update d'un message dans la bibliothèque

#### v0.2.0 (16/05/2017) :
- correction: diffuser quand même le message s'il existe en bdd et qu'il n'y a aucun player disponible
- évolution: nouvelle version de l'APK (1.1): 
  - arrêt de la saisie locale d'un texte ;
  - nouvelle gestion de la partie TTS (uniquement synthetizeToFile(), avec gestion d'un player de fichier) ; 
  - intégration de l'utilisateur du moteur TTS, avec changement de moteur à la volé ; 
- évolution: intégration de la gestion des moteurs, avec configuration au niveau de l'équipement ; 
- évolution: remonté d'informations sur l'équipement distant (version Apk, état du service, moteur actif/défaut, type d'équipement) ; 
- évolution: purge quotidienne des répertoires temporaires (désactivable en configuration) ; 
- évolution: vérification de l'existance des fichiers (désactivable en configuration), avec remonté de l'état dans la bibliothèque ; 
- évolution: configuration de la fréquence de remonté des logs

#### v0.1.1 (30/04/2017) :
- correction: htaccess pour répertoire plugin_info
- correction: ajout de l'installation des dépendances pendant l'installation

#### v0.1.0 (30/04/2017) :
- évolution: ajout des players : squeezebox, sonoaudio
- évolution: gestion des maintenances (suppression des fichiers tmp en nocture, synchronisation des commandes)
- évolution: découverte des équipements pas le réseau (arp-scan)
- évolution: mise en place de la page d'accueil "équippement"
- évolution: gestion des configurations (timeout requête et fréquence des logs)
- évolution: reformate le message à diffuser pour avoir un format précis, pour les nombres à virgules (exemple : 21.3 degrés >> 21 degrés 3).

#### v0.0.2 (18/04/2017) :
- version initiale: player local et sonos ; archivage: local (box) et distant (nas)
- version initiale: bibliothèque des messages
