## Cas d'ERREUR : Class 'olindoteTools' not found

![unknow class](https://abarrau.github.io/jeedom-class-olindoteTools-doc/assets/images/oT_errorClass.png)

Lors de l'affichage de la page d'un plugin développé par abarrau, si cette erreur s'affiche, cela signifie que la class "olindoteTools" n'est pas correctement installée. 
Vous pouvez également vérifier si ce type d'erreur apparait dans la log _"olindoteTools"_.

```
[2019-02-27 21:58:40][WARNING] : [olindoteToolsAutoload()] ERROR: file does not exist (/var/www/html/plugins/DaikinOnlineCtrl/3rdparty/olindote/Tools/../../../../../data/custom/php/olindote/olindoteTools.class.php). TRY TO INSTALL AGAIN THE CLASS.
[2019-02-27 21:58:40][ERROR] : [ERROR][installation olindoteTools class]: la class olindoteTools n'est pas installée. Installez la, via les dépendances du plugin.
```

## Procédure d'installation de la class 'olindoteTools'

Se rendre sur la page de gestion du plugin : 
- Le statut devrait être dans l'état `KO` ;
- lancer les dépendances : cliquez sur le bouton orange `relancer`.

![dependancy](https://abarrau.github.io/jeedom-class-olindoteTools-doc/assets/images/oT_dependance.png)


