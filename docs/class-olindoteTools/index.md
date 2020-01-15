# Class "olindoteTools", pour Jeedom

Tous savoir sur les évolutions de la class [ChangeLog](https://abarrau.github.io/jeedom-plugins-doc/class-olindoteTools/changelog)

En cas d'erreur et pour suivre [l'installation](https://abarrau.github.io/jeedom-plugins-doc/class-olindoteTools/install)

__Remarque__: cette class est destinée à l'utilisation des plugins développés par abarrau, toute utilisation par un autre développeur ne sera pas sous la responsablité d'abarrau.

### Pourquoi la class "olindoteTools" ?
- La class olindoteTools existe depuis le début des plugins développés par abarrau, mais était liée à chaque plugin.   
- En multipliant la réalisation des plugins et avec les modifications permanentes coté coeur/noyau Jeedom, la centralisation de certaines fonctionnalitées facilites les mises à jour. 
- Par ailleurs, lors de nouvelles adaptations (changement d'ergonomie, ajout de fonction), celles-ci étant centralisée au niveau de la class, tous les plugins peuvent en bénéficier. 

### A quoi sert la class "olindoteTools" ?
- La class "olindoteTools" est développée par abarrau, et permet de factoriser les actions d'affichage et/ou de traitement récurrents. 
- Chaque plugin développé par abarrau fait référence à cette class obligatoire.
- De plus des fonctionnalités complémentaires sont ajoutées au plugin : 
	- Versionning du plugin (incluant un versionning de la class également) ; 
	- Backup des versions du plugin (en cours de réalisation) ; 
	- Facilitation de remontée de bug (en cours de réalisation) ; 

### Le "suivi" des installations / mises à jour des plugins développés par abarrau 
- Aucune vision n'est pas à mis disposition des développeurs, pour avoir une estimation du parc d'utilisation de leur plugin (à par pour les plugins payants, où l'on peut estimer le nombre de plugin acheté). 
- L'option "Données d'install./update du plugin" disponible au niveau des paramètres du plugin, permet (une fois coché) d'informer abarrau du parc des plugin développés par abarrau, installés sur votre système. 
	- elle est appelée lors d'une installation, mise à jour ou suppression d'un plugin. 
	- **REMARQUE : vous pouvez à tout moment désactiver cette fonctionnalité en décochant la case.**
		- la class quant à elle continuera de fonctionner sans problème. 
- Cette fonctionnalité d'échange aucune donnée personne, les éléments échangés sont : 
	- id utilisateur (générée lors de l'installation de la class sur le système) ; 
	- version de la class installée
	- liste des plugins développés par abarrau (ainsi que leur version)
- La mise en place de cette fonctionnalité a plusieurs objectifs pour le développeur :
	- de savoir si le plugin est toujours utilisé (pertinant) ; 
	- connaitre l'obsolècence du parc (version) ; 
	- prendre des decisions sur l'intérêt du plugin en fonction des 2 points précédents. 

### Documentation des zones d'information "olindoteTools"
- 3 zones d'informations sont affichées en bas de page de la page de gestion des plugins développés par abarrau.
- découvrez la [documentation sur ces zones d'informations](https://abarrau.github.io/jeedom-plugins-doc/class-olindoteTools/zonesinfo). 
