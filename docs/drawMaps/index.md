# Description

Ce plugin vous permet de dessiner des plans en 2D (maison, espace, ...). 

Les plans générés peuvent être ensuite utilisés de 2 manières différentes : 
* soit un plan "brut" (mur, ouvrant, ..) : 
	* ce plan peut être utilisé dans un design, où vous pouvez ensuite placer vos équipements 
	* ce plan brut sert également de réféence pour les plans dynamiques
* soit un plan "dynamique" :
	* sur la base d'un plan brut, les équipements jeedom sont associés aux objets ouvrants pour dynamiser le plan

Les objets disponibles (en juin 2019) : 
* Ouvrants : 
  * porte : passage, ouverture simple, coulissant simple et double
  * fenêtre : ouverture, 1 vanteau, 2 vanteaux, coulissante simple
   * volet (disponible sur les objets fenêtres) : roulant, standard (2 batants)
* Fixes : 
  * escalier droit


*Remarque :* pour la création des plans, ce plugin utilise une base de développement réalisé par un projet tiers (infos : [https://github.com/ekymoz/homeRoughEditor](https://github.com/ekymoz/homeRoughEditor))

## # Installation et configuration du plugin

Après téléchargement du plugin, vous devez l'activer pour profiter de ces fonctionnalités.
La mise à niveau / installation des "Dépendances" est essentielle pour disposer de toutes les fonctionnalités du plugin. 

