# London Fire Brigade Project  
Ce projet de recherche vous invite à explorer l'essentiel des temps de réponse et d'intervention de cette brigade des pompiers de Londres. 
À l'aide de données fraîchement mises à jour depuis janvier 2009, nous chercherons à comprendre et améliorer chaque précieuse seconde dans les situations d'urgence. 

**Ryma TAKI**


## Introduction 
La brigade des pompiers de Londres, comme mentionné dans la fiche projet est l’une des plus grandes au monde. 
Dans le cadre de notre projet de recherche, nous devrons estimer et analyser les temps de réponse et d’intervention de la brigade. 
Les sources de données utilisées pour répondre à cette problématique proviennent du site ‘London Datastore’ et sont rafraichies sur une base mensuelle. 
Elles fournissent le détail des incidents traités depuis janvier 2009. 

## Objectif 
L’objectif premier de cette étude est de comprendre et d’améliorer le temps de réponse et de mobilisation de la Brigade des Pompiers de Londres. Ces données revêtent une
importance capitale en ce sens que chaque instant compte dans des situations d’urgence telles que des incendies, des accidents de la route, domestiques mais également des interventions de sauvetage. 

## Collecte des données 
Deux sets de données sont mis à notre disposition : 

  1.	Données sur les incidents : Ces données contiennent des détails sur chaque incident traité par la Brigade depuis janvier 2009. Elles incluent des informations importantes telles que la date,
      le lieu de l’incident et le type d’incident traité. Cette base de données constituera la pierre angulaire de notre analyse car elle nous permet de comprendre la nature des situations auxquelles
    	les pompiers de Londres sont confrontés.  
      Pour information, il y a une colonne supplémentaire dans la table des Incidents (39 colonnes) vs les métadonnées (38 noms de variables). 
      La dernière colonne a donc été supprimée car elle ne semblait correspondre à rien dans les métadonnées.  

**La table contient 2 227 677 entrées.**

  2.	Données sur les mobilisations : Le deuxième jeu de données fournit des informations sur chaque camion de pompiers envoyé sur les lieux d’un incident depuis janvier 2009. Il inclut notamment
      des détails sur l’appareil mobilisé, son lieu de déploiement et les heures d’arrivées sur les lieux de l’incident. Ces données sont tout aussi essentielles pour comprendre et évaluer l’efficacité
    	du déploiement des ressources en fonction de la nature et de la localisation des incidents.
    	
**La table contient : 1 602 834 entrées.**

## Exploration des données 
### Analyse des champs 
#### Dictionnaire des incidents 



![image](https://github.com/Ryma8905/Projet-datascientest/assets/156120862/1e5c80e3-0b95-47df-a714-277fadb08b08)



#### Dictionnaire des mobilisations 




![image](https://github.com/Ryma8905/Projet-datascientest/assets/156120862/bc52cada-7f70-43e8-ac4c-f74bb2cf7d93)





### Analyse des valeurs manquantes 

#### Incidents 
Le pourcentage global des valeurs manquantes pour les incidents est de 12.57% et est  un peu plus bas pour les mobilisations avec 9.66%. Une vision plus détaillée, au niveau variable est nécessaire.

_Groupe des variables avec un pourcentage de NA inférieur à 1%_


![image](https://github.com/Ryma8905/Projet-datascientest/assets/156120862/d8df3152-2eb4-410d-95bf-b1883931c8b1)



_Groupe des variables avec pourcentage de NA inférieur compris entre 1 et 15%_


![image](https://github.com/Ryma8905/Projet-datascientest/assets/156120862/80deb49a-838b-44ef-aaee-564958e90f96)

[1] Il s'agit de la variable cible. 


_Groupe des variables avec pourcentage de NA supérieur à 40%_ 


![image](https://github.com/Ryma8905/Projet-datascientest/assets/156120862/5f26081b-65fe-48c9-b031-81ebccc910f2)


#### Mobilisations 
La répartition des NAs dans le dataset « Mobilisations » laisse apparaitre une polarisation en ce sens que l’on a soit de très petites valeurs de NA,
entre 0 et 2 %, soit de très grandes valeurs, supérieures à 50%. 

_Groupe des variables avec pourcentage de NA compris entre 0 et 2%_  



![image](https://github.com/Ryma8905/Projet-datascientest/assets/156120862/112fa06a-d1f4-4d51-9bb4-eab45bbb1fa1)



_Groupe des variables avec pourcentage de NA supérieur à 50%_



![image](https://github.com/Ryma8905/Projet-datascientest/assets/156120862/55c86fc6-d7db-43ab-904a-1b1ad4587cc8)


### Conclusion et règles de gestion des NAs

1.	On constate que la variable Easting_m a environ 50% de valeurs manquantes et la variable Easting_rounded qui est construite sur la première n’a quant à elle aucune valeur manquante.
    Cela semble incohérent si l’on se fie au dictionnaire des données. 
2.	En ce qui concerne les variables pour lesquelles il y a trop de valeurs manquantes (> 40%), celles-ci sont inexploitables. Calculer une moyenne ou un mode sur la moitié (voire moins)
    du jeu de données ne sera pas représentatif et on ne pourra pas remplacer les valeurs manquantes avec cela. On pensera dans un premier temps à les supprimer du jeu de données. 
3.	Les lignes pour lesquelles il y a peu de valeurs manquantes seront supprimées.
   
Cependant, le fait qu’il y ait des NAs n’est pas la seule raison pour laquelle on se délesterait de certaines variables. En effet, parfois certaines variables sont redondantes. Elles apportent 
le même type d’information donc il convient de supprimer certaines. Par exemple, il y a beaucoup de variables qui concernent la localisation et avoir un tel niveau de détail n’est pas forcément 
nécessaire. Les zones ou districts sont suffisants. 

Voici donc un tableau récapitulatif qui reprend la liste des variables dont on se sépare et en détaille les raisons : 



![image](https://github.com/Ryma8905/Projet-datascientest/assets/156120862/3d071272-f276-4ec2-bb1a-f58b6242f63b)


### Analyse des données 
#### Analyse des variables qualitatives 

_Statistiques descriptives de la table des incidents_ 
 
![image](https://github.com/Ryma8905/Projet-datascientest/assets/156120862/882a28d5-a723-44db-92b6-71a8ff9c5e28)


On constate  qu’en moyenne,  les pompiers mettent 5.25 minutes à arriver sur les lieux de l’incident et qu’il faut que 1.3 stations envoient un contingent et que cela représente 1.5 camions. 
La médiane du temps d’intervention reste proche de la moyenne ce qui suggère mois d’asymétrie des données. La moyenne étant une mesure de centralité qui est sensible aux valeurs extrêmes et 
la médiane étant plus robuste aux valeurs extrêmes, leur proximité suggère que les valeurs aberrantes n’ont pas un impact significatif sur la mesure de la centralité en ce qui concerne le 
temps d’arrivée. 
Les quantiles de la durée d’intervention sont quant à eux tous égaux à 1h ce qui suggère une uniformité pour la durée d’intervention. 


_Statistiques descriptives de la table des mobilisations_



![image](https://github.com/Ryma8905/Projet-datascientest/assets/156120862/4f508686-fa68-4aab-8b1e-47164b8343a0)


On constate que la moyenne du temps d’intervention de la table des « Mobilisations » est sensiblement proche de celle de la table des « Incidents ». Il y va de même pour la médiane. 
Les valeurs de la table des Mobilisations semblent juste un peu au-dessus de la celle des Incidents. 	
On constate également que Attendance time  = Turnout time + Travel time à savoir Temps d’intervention = Temps de trajet + Temps de sortie de la station. 
La variable qui contribue le plus au temps d’intervention semble être le temps de trajet. 
Les distributions des variables communes aux deux tables semblent similaires. 
En effet, si l’on met côte à côte les histogrammes des distributions des temps d’arrivées, on constate visuellement que les distributions se ressemblent. 


![image](https://github.com/Ryma8905/Projet-datascientest/assets/156120862/068f8aca-9fc9-4246-b485-5b1fc72b38cb)


La variable  _PumpHoursRoundUp_ qui est le temps passé sur les lieux de l'incident par les pompiers , (   60    89   119 ...  8408  5127 20219), indique des heures aberrantes parfois.  En effet, 89 n’est pas 
l’arrondi à l’heure supérieure. On devrait avoir des multiples de 60 seulement. Celles-ci ont été retirées. 

On constate que la plupart des zones des lieux d’incidents ainsi que la station d’intervention sont les mêmes. Dans le cas où d’autres stations interviennent dans des zones qui ne sont pas les leurs, 
cela correspond aux stations secondaires venues en renfort. Cela conforte notre compréhension des variables.  
Le croisement entre les variables _ResourceMobilisationId_ et _Resource_Code_ qui reprennent respectivement l’identifiant des ressources mobilisées et le code des ressources cependant 
l’espace mémoire de la machine est limité.
 
Le croisement entre les variables _NumStationsWithPumpsAttending_, les heures et dates ainsi que _PumpCount_ nous permet de comprendre la différence entre les deux variables. 
La première représente le nombre de stations qui sont intervenues sur l’incident tandis que _PumpCount_ nous renseigne sur le nombre de camions de pompiers effectivement sur place. 
Pour aller plus loin dans le croisement de variables, la mesure de corrélation entre celles-ci peut également nous permettre de comprendre les interactions potentielles entre les variables 
et in fine nous mettre sur la piste des variables à privilégier. 
 
_Corrélation entre les variables quantitatives de la table des Incidents_


![image](https://github.com/Ryma8905/Projet-datascientest/assets/156120862/ba2fe2d8-749d-425e-9da8-d64037ebb48a)


On constate une zone de corrélation forte dans le carré bas et à droite entre le nombre de camions en intervention, le nombre total de camions, le _PumpHoursRoundUp_ et le _Notional Cost_. 
Ces variables forment un cluster et pourraient par exemple être traitées ensemble. Entre le _PumpHoursRoundUp_ et le _Notional Cost_, la corrélation est proche de 1 ce qui est normal car ils ont une 
relation de type aX. 
Il semble y avoir une corrélation nulle dans le reste du carré ce qui indique une absence de relation linéaire entre les variables. On peut donc postuler que ces variables sont indépendantes 
les unes des autres. La question se pose maintenant sur la sélection des variables, i.e. si nous allons choisir seulement les variables qui ont une corrélation significative avec la variable cible. 


_Corrélation entre les variables quantitatives de la table des Mobilisations_


![image](https://github.com/Ryma8905/Projet-datascientest/assets/156120862/fae93463-73fa-4655-891a-3615e1b4dccf)


Comme remarqué précédemment, il y a une très forte corrélation entre le temps de trajet et le temps d’intervention. On pourra donc s’intéresser de près à tout ce qui pourrait impacter 
le temps de trajet notamment les raisons de retard ou encore si les adresses étaient bonnes ou non. 
Pour aller au-delà de la visualisation en heatmap et nous permettre de valider nos constatations, nous avons choisi de les confirmer avec un graphique pairplot. 
On a là un outil puissant pour explorer et visualiser les données multidimensionnelles. On peut alors repérer des tendances, des relations, des distributions, des anomalies et 
d'autres caractéristiques importantes des données, ce qui en fait un point de départ précieux pour l'analyse exploratoire des données.	 

_Pour information, la ligne Ressource Mobilisation Id ne doit pas être prise en compte car il s’agit de modalités et non de variables quantitatives._



_Pairplot avec kde de la table des Incidents_ 


![image](https://github.com/Ryma8905/Projet-datascientest/assets/156120862/133d6be2-c1f6-49da-b128-0b702cd189c3)


Aucune des variables ne présente de leptukurtose  => il y a certes des variables pour lesquelles on observe des pics droits, mais il n y a pas de valeurs extrêmes. De la même façon, on ne peut affirmer 
que les données sont platykurtiques  car les formes des cloches ne sont pas moins aplaties que celle d’une variable normale et les valeurs ne sont pas forcément plus dispersées.
Pour les restes des variables en dehors des variables de temps, on observe à chaque fois des concentrations vers le coin gauche bas du graphique. 
Au final, on constate la même chose que précédemment concernant les relations linéaires dans le carré inférieur droit de la matrice. 


_Pairplot avec kde de la table des Mobilisations_ 


![image](https://github.com/Ryma8905/Projet-datascientest/assets/156120862/3e077656-000d-4973-831f-84e90fd609b8)


Le pairplot confirme les observations faites précédemment et évoque des corrélations faibles soit positives (triangle vers le haut) soit négatives (triangle vers le bas). 


### Visualisation des variables de temps
#### Par année 

_Répartition des incidents par année dans la table des Incidents_ 


![image](https://github.com/Ryma8905/Projet-datascientest/assets/156120862/df537eab-b65f-484c-97c8-38b3c44429a1)


_Répartition des incidents par année dans la table des Mobilisations_


![image](https://github.com/Ryma8905/Projet-datascientest/assets/156120862/d194d81d-5bf9-4791-af24-14e0916d1bd4)


On observe le même pattern entre les deux tables bien que les effectifs soient différents. 


#### Par mois 

_Répartition du temps moyen d'intervention pie chart_


![image](https://github.com/Ryma8905/Projet-datascientest/assets/156120862/0277b159-b552-41c9-a6ec-ce03326d6244)


_Répartition du temps moyen d'intervention histogramme_

![image](https://github.com/Ryma8905/Projet-datascientest/assets/156120862/76ec3c9b-36cc-4583-b8be-9581fb80496d)


On constate avec ces statistiques très simples que, en moyenne le temps d’intervention est quasi identique d’un mois sur l’autre et varie de 8.2 à  8.5%. 
S’il n y avait pas eu les légendes, nous aurions pu croire que les éléments du pie chart étaient identiques. Une représentation en histogramme permet de mieux visualiser 
les différences d’où l’importance de choisir la représentation graphique adéquate. 
L’analyse des deux graphiques met en exergue une légère différence d’un mois sur l’autre. Un test statistique permettrait d’avoir une assise plus précise quant à ce constat. 
Pour cela, nous allons procéder à un test anova. 
L'ANOVA (Analyse de la variance) est une technique statistique utilisée pour analyser si les moyennes de trois groupes ou plus sont égales ou différentes dans le contexte de 
plusieurs groupes ou conditions. C'est un outil précieux dans l'analyse des données pour répondre à des questions telles que "Y a-t-il une différence significative entre les groupes ?" 
ou "Quel groupe est significativement différent des autres ?". 

Les résultats sont les suivants avec une p value à 5%: 

**f statistic: 80.46816007306143 p_value: 1.120431674796777e-182**

_L'ANOVA montre qu'il existe une différence statistiquement significative entre les mois._

Cela signifie que le temps d'intervention varie en fonction du mois de l'année ce qui confirme le constat précédent qui a été orienté par la représentation en histogramme. 
Cela montre à quel point deux tests statistiques qui mènent aux mêmes conclusions à savoir qu’il y a des différences significatives entre les groupes peuvent avoir des représentations 
graphiques soit qui contredisent le test, soit qui le confirment. 

#### Par jour de la semaine 

_Répartition du temps moyen d'intervention par jour de la semaine_

La même conclusion est faite en ce qui concerne les jours de la semaine :


![image](https://github.com/Ryma8905/Projet-datascientest/assets/156120862/1b455a66-53f7-4674-bc32-68562017e7ec)


**f statistic: 93.45732788231139 p_value: 7.238724984128987e-118**
_L'ANOVA montre qu'il existe une différence statistiquement significative entre les jours._
Cela signifie que le temps d'intervention varie en fonction du jour de la semaine.


#### Par heure 

_Histogramme des nombres d'intervention par heure de la journée_


![image](https://github.com/Ryma8905/Projet-datascientest/assets/156120862/a29e6e05-6174-4d1f-85c5-e72fc02c385e)


**f statistic: 423.5404032545424 p_value: 0.0**
_L'ANOVA montre qu'il existe une différence statistiquement significative entre les heures._
Cela signifie que le temps d'intervention varie en fonction de l'heure de la journée. 
On constate de visu, que le plus gros contingent d’appels a lieu de la fin de matinée jusqu’en fin de soirée. 


### Stationnarité 

Il est intéressant de tester la stationnarité de la base. Cependant, il est important de noter que la stationnarité n'est pas toujours nécessaire, en particulier pour des 
analyses exploratoires ou des séries de données très courtes. Dans certains cas, des séries temporelles non stationnaires peuvent encore fournir des informations précieuses. 
La vérification de la stationnarité dépend du contexte et des objectifs de l'analyse. Nous testons la stationnarité en avance de phase et cela sera analysé dans la deuxième partie du rapport. 
Dans un premier temps, un ADF a été fait sur une base journalière. Les ressources mémoire étant limitées, le test n’a pas pu aboutir. Plusieurs options s’offraient à nous : 
1.	Échantillonnage de données : cela permet de réduire la consommation de mémoire, mais l'échantillonnage peut introduire une certaine perte d'information.
2.	Réduction de la fréquence : Si la série de données est journalière et que la mémoire est un problème, on agrége par mois. Cela réduit la taille des données à analyser.
3.	Utilisation d'une infrastructure avec plus de mémoire
4.	Optimisation des données : On peut essayer d'optimiser la série de données en réduisant le nombre de colonnes ou en supprimant les données inutiles, le cas échéant.
5.	Traitement en blocs : Plutôt que de charger l'ensemble de la série en mémoire, on pourrait envisager de diviser la série en blocs plus petits et d'effectuer le test ADF sur
    ces blocs de manière itérative.
  	
Nous avons choisi l’option 2 et avons obtenu les résultats suivants sur une fréquence mensuelle:

Statistique ADF : -3.2185825321090786
p-value : 0.018933933594991802

Les séries stationnaires sont plus faciles à modéliser, car leurs propriétés statistiques restent constantes dans le temps. En effet, les propriétés statistiques, telles que la moyenne, 
la variance et la corrélation, si elles restent constantes dans le temps permet que les conclusions des analyses statistiques demeurent valides à travers différentes périodes de temps. 
En éliminant la tendance temporelle et la saisonnalité, la stationnarité permet de réduire le bruit dans les données. 
De plus, cela facilite l'identification de relations et de modèles sous-jacents. De nombreux tests statistiques, y compris les tests d'hypothèse et les tests de causalité, supposent que 
les données sont stationnaires. Si la stationnarité n'est pas vérifiée, les résultats de ces tests peuvent être biaisés ou incorrects.


### Analyse des types d’incidents, des temps d’intervention et de la localisation
#### Visualisation des types d’incidents 


![image](https://github.com/Ryma8905/Projet-datascientest/assets/156120862/b210b3c9-dac3-4894-9b84-7b7206d1a944)


On constate que les alarmes incendie automatiques constituent le plus gros contingent de cause de recours aux pompiers. Viennent ensuite les services spéciaux puis les fausses alertes 
mais dans une bonne intention, puis le feu secondaire et enfin le feu primaire* et la fausse alerte dans un but malveillant. 
Au final, tout comme précédemment, la répartition reste la même d’une année sur l’autre. Bien que les effectifs changent, les répartitions restent peu ou prou identiques. 

_*Primary fires are generally more serious fires that harm people or cause damage to property and meet at least one of the following conditions: 
• any fire that occurred in a (non-derelict) building, vehicle or (some) outdoor structures 
• any fire involving fatalities, casualties or rescues 
• any fire attended by five or more pumping appliances.
Secondary fires are generally small outdoor fires, not involving people or property. These include refuse fires, grassland fires and fires in derelict buildings or vehicles, unless 
these fires involved casualties or rescues, or five or more pumping appliances attended, in which case they become primary fires. Source : Fire Statistics definitions – GOV.UK_


#### Croisement entre type d’incident et temps d’intervention 


![image](https://github.com/Ryma8905/Projet-datascientest/assets/156120862/462a2c09-5cec-4f32-a715-aec06fcc4db4)


On a grosso modo un temps d’intervention moyen identique excepté pour le Special Operations Room. 
Un test anova peut nous permettre de valider ou d’invalider statistiquement notre constat. 

Les résultats sont les suivants avec une p value à 5%: 
f statistic: 2045.138681298415 p_value: 0.0

_L'ANOVA montre qu'il existe une différence statistiquement significative entre les types d’incidents._
Cela signifie que le temps d'intervention varie en fonction du type d’incident.


#### Croisement entre la localisation et temps d’intervention 

La longitude étant une variable manquante prépondérante, on ne peut utiliser les coordonnées GPS afin de pouvoir avoir une représentation en carte afin de voir les quartiers de 
Londres où le temps d’intervention est le plus élevé et pouvoir caractériser les zones de la ville. 
Pour ce faire, nous sommes obligés de supprimer toutes les lignes avec des coordonnées GPS manquantes. Les statistiques descriptives de ce subset montrent le résultat suivant : 
On constate comme pour les 2 précédents tableaux que la moyenne de du temps d’arrivée tourne toujours autour de 5 minutes. 


_Statistiques descriptives de la variable cible de la table des Incidents nettoyée des coordonnées GPS manquantes_


![image](https://github.com/Ryma8905/Projet-datascientest/assets/156120862/73ab56d7-087e-4d50-9310-957fe11e62ab)


De ce fait, il convient d’utiliser cette information pour créer les classes de la carte : 


![image](https://github.com/Ryma8905/Projet-datascientest/assets/156120862/e3832014-619a-4600-82b7-03ec2f6d790e)


La répartition des points suit la distribution du tableau des statistiques descriptives. 



## Création de la base de travail 

Il semble nécessaire de regrouper toutes les données dans un même dataset. On procède pour cela à un « inner join » des données par l’identifiant d’incident afin d’avoir une exhaustivité de l’information.   
Afin de disposer de toutes les informations dans une même base de travail, nous allons procéder à la jointure des 2 datasets. 



![image](https://github.com/Ryma8905/Projet-datascientest/assets/156120862/b9ae9a40-d88b-4586-b005-8904822858d0)


Comme observé précédemment, on constate qu’en moyenne la variable  _FirstPumpArriving_AttendanceTime_  est proche  la variable  _AttendanceTimeSeconds_.
Nous allons privilégier l’utilisation de la variable _FirstPumpArriving_AttendanceTime_ afin de procéder à la résolution de la problématique. Nous verrons plus tard s’il y a lieu de tester 
la variable issue de la table des Mobilisations. 
Nous procéderons de la même façon pour le subset qui contient les coordonnées GPS. 
Pour aller plus loin, étant donné que les dataframes contiennent des variables catégorielles notamment celle concernant le type d’intervention, on doit effectuer un encodage pour la représenter 
en tant que variable numérique avec un encodage one-hot (binaire) afin que le modèle d’apprentissage automatique puisse prendre en compte les catégories dans les prédictions. 
A mon sens il ne semble pas nécessaire de standardiser les coordonnées GPS étant donné qu’elles sont toutes localisées à Londres et sont dans une plage de valeur réduite. 
Pour ce qui est des informations sur le mois et l'année d'intervention, on peut également les encoder pour les rendre utilisables. Par exemple, on extrait le mois et l'année de ces variables 
et on les ajoute comme caractéristiques distinctes. On peut également utiliser des techniques de codage cyclique pour les mois dans le cas où on voudrait exploiter la saisonnalité.
Au final, on peut supposer a priori (cela sera vérifié ultérieurement) que quelle que soit la base que l’on crée, on aura un déficit d’information car : 
-	L’option 1 prévoit une base avec pratiquement toutes les observations mais amputée des variables explicatives qui ont trop de valeurs manquantes. 
-	L’option 2 prévoit une base avec toutes les variables explicatives mais amputée des lignes qui ont des valeurs manquantes.


## Hypothèses de modélisation 
L'objectif de cette deuxième partie de rapport est d'offrir une analyse approfondie des résultats obtenus lors de la modélisation des temps d'intervention de la brigade des pompiers. Notre approche a englobé un processus rigoureux, débutant par un préprocessing des données et s'étendant jusqu'à l'utilisation de modèles sophistiqués de machine learning. Chaque étape a été étudiée pour garantir la robustesse et la fiabilité des résultats.

Au début du processus de modélisation, sur les conseils du référent Datascientest, nous avons opté pour une approche prudente en testant des modèles naïfs afin d'établir une première compréhension du phénomène étudié. Ces modèles bien que délibérément simplistes, ont joué un rôle crucial en offrant une première perspective sur la dynamique des systèmes sous-jacents. Cette démarche visait à explorer différentes pistes et à identifier les variables clés* qui pourraient influencer le temps d’intervention des brigades de pompiers de Londres. Les modèles naïfs ont ainsi servi de boussole initiale, nous orientant vers les aspects les plus significatifs à approfondir et à intégrer dans des modèles plus sophistiqués par la suite. Cette phase exploratoire a contribué à jeter les bases d'une modélisation plus élaborée, guidant la sélection des variables à privilégier et permettant une meilleure compréhension des mécanismes sous-jacents.
Les étapes pour nous conduire à la sélection du meilleur modèle sont les suivantes : 
-	Entrainement de modèles naïfs pour ne conserver que les variables qui contribuent le plus au modèle 
-	Réduction de la base aux variables utiles 
-	Gridsearch CV sur plusieurs modèles linéaires et non linéaires sur le dataset nouvellement créé
-	Sélection des meilleurs modèles 
-	Optimisation bayésienne sur les modèles sélectionnés à l’étape précédente. 

### Préparation et rappels 
Pour rappel, un premier cleaning des NAs et des heures qui ne sont pas des multiples de 60 (d’après la notice de lecture fournie) des deux datasets a produit les résultats suivants : 
Incidents
-	Nombre de lignes : 1 287 593
-	Nombre de colonnes : 21
Mobilisations 
-	Nombre de lignes : 2 227 677
-	Nombre de colonnes : 19
Ensuite, afin de pouvoir avoir une répartition géographique des interventions, nous avons éliminé toutes les lignes pour lesquelles la variable latitude n’était pas renseignée. Nous avons utilisé le dataset des incidents comme base de travail seulement filtré sur les heures non multiples de 60 et avons obtenu les résultats suivants : 
-	Nombre de lignes : 726 790
-	Nombre de colonnes : 38

_*Pour rappel, les variables TravelTimeSeconds et AttendanceTimeSeconds ont été supprimées car elles sont des proxy de la variable à étudier. Les variables HourOfCall_y et CalYear_y qui proviennent de la table des Mobilisations ont également été supprimée car nous avons déjà ces données issues de la table des Incidents_

Nous avons ensuite créé une base de travail en concaténant les deux datasets, à partir de la combinaison cleaning des NAs et heures non multiples de 60. 
La table des Mobilisations contenait des doublons par rapport à la variable PumpOrder, i.e. le nombre de camions envoyés sur les lieux de l’incident. Comme beaucoup de champs de cette table n’ont pas été pris en compte, nous ne conservons que le max du nombre de camions envoyés

Base de travail construite à partir du cleaning des NAs et des heures non multiples de 60 et des proxy et de la variable d’heure supplémentaire :
-	Nombre de lignes : 1 237 733
-	Nombre de colonnes : 38
Après la suppression des variables redondantes, il reste 18 colonnes. Mais après dichotomisation et standardisation, on repasse à 222 colonnes.

Cependant, les tests faits sur la base contenant ~ 1.2 millions de lignes n’aboutissent pas sur la machine utilisée pour les modèles de régression non linéaire. Une réduction de la base s’avère nécessaire pour ce périmètre. 
Dans un premier temps, nous faisons un échantillon aléatoire permettant de réduire la base à 1 million de lignes sans succès. On passe à 500k en vain. Malheureusement, la puissance de la machine utilisée n’a permis de sortir des résultats que pour 10k lignes pour les modèles non linéaires. 
Au-delà de ces échantillons, la machine mouline indéfiniment. Nous n’ignorons pas qu’il y a un biais concernant la comparaison des performances des modèles linéaires et non linéaires mais les ressources machines nous limitent dans nos recherches. 


### Modèles étudiés 
Les premiers modèles simples étudiés sont les suivants : 
Nous avons pris d’un part des modèles non linéaires du fait des résultats produits lors de la data préparation. On choisit un nombre de permutations égal à 10 pour garder une robustesse des estimations pour voir des conclusions plus fiables.

-	KNN : pour ce modèle, afin de connaître les contributions des variables, nous avons utilisé une permutation afin d’évaluer leur importance en mesurant comment le score du modèle change lorsque les valeurs d'une variable sont aléatoirement permutées. Cela implique de permuter les valeurs de chaque variable de manière aléatoire, recalculer les prédictions du modèle et mesurer comment cela affecte les performances du modèle (par exemple, le score R²). La différence entre les performances avant et après la permutation est utilisée comme mesure de l'importance de la variable. 
-	Random Forest : même méthode 
-	Decision tree : même méthode 
-	Gradient Boosting : même méthode

Nous n’avons pas pris de modèle SVM car trop coûteux en termes de ressource machine. Le modèle n'a jamais pu tourner.  

Pour ce qui est des régressions linéaires, nous pourrions utiliser la même méthode. Cependant, les coefficients du modèle sont utilisés comme mesure de l’importance des variables. Ils indiquent déjà la contribution de chaque variable à la prédiction de la variable cible. 

-	La régression linéaire : régression linéaire simple
-	
Les régressions Lasso et Ridge permettent de prévenir le surajustement et d’assurer la stabilité du modèle.

-	La régression Lasso : elle intègre une pénalité de norme L1 ce qui peut conduire à une sélection des variables en faisant le split entre les variables qui ont une contribution nulle sur la prédiction du modèle et celles qui ont un impact significatif. 

-	La régression Ridge : elle intègre une pénalité de norme L2 qui a tendance à réduire l’impact des variables les moins importantes plutôt que de les éliminer complètement. Le modèle Ridge est particulièrement utile lorsque les variables explicatives sont fortement corrélées entre elles, car il permet de stabiliser les coefficients et d'éviter une sensibilité excessive aux fluctuations dans les données. Etant donné les résultats obtenus en partie , nous supposons à l’avance que ce modèle ne sera pas d’une grande efficacité. 

Les résultats obtenus sont les suivants : 


