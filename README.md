# London Fire Brigade Project  
Ce projet de recherche vous invite à explorer l'essentiel des temps de réponse et d'intervention de cette brigade des pompiers de Londres. 
À l'aide de données fraîchement mises à jour depuis janvier 2009, nous chercherons à comprendre et améliorer chaque précieuse seconde dans les situations d'urgence. 

**Ryma TAKI**


## Introduction 
La brigade des pompiers de Londres, comme mentionné dans la fiche projet est l’une des plus grandes au monde. 
Dans le cadre de notre projet de recherche, nous devrons estimer et analyser les temps de réponse et d’intervention de la brigade. 
Les sources de données utilisées pour répondre à cette problématique proviennent du site ‘London Datastore’ et sont rafraichies sur une base mensuelle. 
Elles fournissent le détail des incidents traités depuis janvier 2009 et arrêtées à juillet 2023. 

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

**La table contient 1 602 834 entrées.**

  2.	Données sur les mobilisations : Le deuxième jeu de données fournit des informations sur chaque camion de pompiers envoyé sur les lieux d’un incident depuis janvier 2009. Il inclut notamment
      des détails sur l’appareil mobilisé, son lieu de déploiement et les heures d’arrivées sur les lieux de l’incident. Ces données sont tout aussi essentielles pour comprendre et évaluer l’efficacité
    	du déploiement des ressources en fonction de la nature et de la localisation des incidents.
    	
**La table contient : 2 227 677 entrées.**

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
    du jeu de données ne sera pas représentatif et on ne pourra pas remplacer les valeurs manquantes avec cela. Il convient donc de les supprimer du jeu de données. 
3.	Les lignes pour lesquelles il y a des valeurs manquantes seront supprimées (peu nombreuses).
   
Cependant, le fait qu’il y ait des NAs n’est pas la seule raison pour laquelle on se délesterait de certaines variables. En effet, parfois certaines variables sont redondantes. Elles apportent 
le même type d’information donc il convient de s'en débarrasser. Par exemple, il y a beaucoup de variables qui concernent la localisation et avoir un tel niveau de détail n’est pas forcément 
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


La variable  _PumpHoursRoundUp_ qui est le temps passé sur les lieux de l'incident par les pompiers , (60    89   119 ...  8408  5127 20219), indique des heures aberrantes parfois.  En effet, 89 n’est pas 
l’arrondi à l’heure supérieure (comme spécifié dans le dictionnaire des métadonnées). On devrait avoir des multiples de 60 seulement. Celles-ci ont été retirées. 

On constate que la plupart des zones des lieux d’incidents ainsi que la station d’intervention sont les mêmes. Dans le cas où d’autres stations interviennent dans des zones qui ne sont pas les leurs, 
cela correspond aux stations secondaires venues en renfort. Cela conforte notre compréhension des variables.  
Le croisement entre les variables _ResourceMobilisationId_ et _Resource_Code_ qui reprennent respectivement l’identifiant des ressources mobilisées et le code des ressources cependant 
l’espace mémoire de la machine est limité.
 
Le croisement entre les variables _NumStationsWithPumpsAttending_, les heures et dates ainsi que _PumpCount_ nous permet de comprendre la différence entre les deux variables. 
La première représente le nombre de stations qui ont été mobilisées sur l’incident tandis que _PumpCount_ nous renseigne sur le nombre pompes à incendie utilisées. 
Pour aller plus loin dans le croisement de variables, la mesure de corrélation entre celles-ci peut également nous permettre de comprendre les interactions potentielles entre les variables 
et in fine nous mettre sur la piste des variables à privilégier. 
 
_Corrélation entre les variables quantitatives de la table des Incidents_


![image](https://github.com/Ryma8905/Projet-datascientest/assets/156120862/ba2fe2d8-749d-425e-9da8-d64037ebb48a)


On constate une zone de corrélation forte dans le carré bas et à droite entre le nombre de pompes à incendies utilisées, le _PumpHoursRoundUp_ et le _Notional Cost_. 
Ces variables forment un cluster et pourraient par exemple être traitées ensemble. Entre le _PumpHoursRoundUp_ et le _Notional Cost_, la corrélation est proche de 1 ce qui est normal car ils ont une 
relation de type aX. 

Au final, il semble que toutes les variables qui incluent la notion de pompe à incendie présentent une forte corrélation entre elles. 

Par ailleurs, on constate une corrélation nulle dans le reste du carré ce qui indique une absence de relation linéaire entre les variables. On peut donc postuler que ces variables sont indépendantes 
les unes des autres. 


_Corrélation entre les variables quantitatives de la table des Mobilisations_


![image](https://github.com/Ryma8905/Projet-datascientest/assets/156120862/fae93463-73fa-4655-891a-3615e1b4dccf)


Comme remarqué précédemment, il y a une très forte corrélation entre le temps de trajet et le temps d’intervention. On pourra donc s’intéresser de près à tout ce qui pourrait impacter 
le temps de trajet notamment les raisons de retard ou encore si les adresses étaient bonnes ou non. 
Pour aller au-delà de la visualisation en heatmap et nous permettre de valider nos constatations, nous avons choisi de les confirmer avec un graphique pairplot. 
On a là un outil puissant pour explorer et visualiser la répartition des données. On peut alors repérer des tendances, des relations, des distributions, des anomalies et 
d'autres caractéristiques importantes des données là où une analyse de corrélation ne fournit qu'une seule information. Cela en fait un point de départ précieux pour l'analyse exploratoire des données.	 

_Pour information, la ligne Ressource Mobilisation Id ne doit pas être prise en compte car il s’agit de modalités et non de variables quantitatives._



_Pairplot de la table des Incidents_ 


![image](https://github.com/Ryma8905/Projet-datascientest/assets/156120862/133d6be2-c1f6-49da-b128-0b702cd189c3)

Comme précédemment, on observe dans le carré droit en bas une relation linéaire entre les variables. Il s'agit toujours des variables qui incluent la notion de pompe à incendie. 

La relation entre la variable cible et les autres variables du dataset ne semble pas apporter davantage d'information. 

Au final, on constate la même chose qu'avec la matrice corrélation seule. 


_Pairplot de la table des Mobilisations_ 


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


_Répartition du temps moyen d'intervention_

![image](https://github.com/Ryma8905/Projet-datascientest/assets/156120862/76ec3c9b-36cc-4583-b8be-9581fb80496d)


On constate avec ces statistiques très simples que, en moyenne le temps d’intervention est quasi identique d’un mois sur l’autre et varie de 8.2 à  8.5%.
L’analyse du graphique met en exergue une légère différence d’un mois sur l’autre. Un test statistique permettrait d’avoir une assise plus précise quant à ce constat. 
Pour cela, nous allons procéder à un test anova. 
L'ANOVA permet d'analyser si les moyennes de trois groupes ou plus sont égales ou différentes dans le contexte de 
plusieurs groupes ou conditions. C'est un outil précieux dans l'analyse des données pour répondre à la question suivante : "Y a-t-il une différence significative entre les groupes ?".

Les résultats sont les suivants avec une p value à 5%: 

**f statistic: 80.46816007306143 p_value: 1.120431674796777e-182**

_L'ANOVA montre qu'il existe une différence statistiquement significative entre les mois._

Cela signifie que le temps d'intervention varie en fonction du mois de l'année ce qui confirme le constat précédent qui a été orienté par la représentation en histogramme. 
 

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


Lorsque l'on croise le type d'incident avec le temps d'intervention, on obtient le graphe suivant :

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


![image](https://github.com/Ryma8905/Projet-datascientest/assets/156120862/b9ae9a40-d88b-4586-b005-8904822858d0)


Comme observé précédemment, on constate qu’en moyenne la variable  _FirstPumpArriving_AttendanceTime_  est proche  la variable  _AttendanceTimeSeconds_.
Nous allons privilégier l’utilisation de la variable _FirstPumpArriving_AttendanceTime_ afin de procéder à la résolution de la problématique et supprimer la variable proxy issue de la table des Mobilisations. 

Le choix de conserver la variable issue de la table des Incidents est dû au fait qu'elle issue du dataset duquel nous prenons le plus de variables. 


Etant donné que les dataframes contiennent des variables catégorielles notamment celle concernant le type d’intervention, nous devons effectuer un encodage pour la représenter 
en tant que variable numérique avec un encodage one-hot (binaire) afin que le modèles testés puissent prendre en compte les catégories dans les prédictions. 
 
Pour ce qui est des informations sur le mois et l'année d'intervention, on peut également les encoder pour les rendre utilisables. Par exemple, on extrait le mois et l'année de ces variables 
et on les ajoute comme caractéristiques distinctes. 

Au final, on peut supposer a priori (cela sera vérifié ultérieurement) que l'on aura un déficit d’information car nous sommes 
obligés d'amputer la base de beaucoup de variables explicatives car elles ont trop de valeurs manquantes.  


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
-	Nombre de lignes : 2 156 847
-	Nombre de colonnes : 19

Ensuite, afin de pouvoir avoir une répartition géographique des interventions, nous avons éliminé toutes les lignes pour lesquelles la variable latitude n’était pas renseignée. Nous avons utilisé le dataset des incidents comme base de travail seulement filtrée sur les heures non multiples de 60 et avons obtenu les résultats suivants : 
-	Nombre de lignes : 726 790
-	Nombre de colonnes : 38

_*Pour rappel, les variables TravelTimeSeconds et AttendanceTimeSeconds ont été supprimées car elles sont des proxy de la variable à étudier. Les variables HourOfCall_y et CalYear_y qui proviennent de la table des Mobilisations ont également été supprimée car nous avons déjà ces données issues de la table des Incidents_

Nous avons ensuite créé une base de travail en concaténant les deux datasets, à partir de la combinaison cleaning des NAs et heures non multiples de 60. 
La table des Mobilisations contenait des doublons par rapport à la variable _PumpOrder_, i.e. le nombre de camions envoyés sur les lieux de l’incident. Comme beaucoup de champs de cette table n’ont pas été pris en compte, nous ne conservons que le max du nombre de camions envoyés

Base de travail construite à partir du cleaning des NAs et des heures non multiples de 60 et des proxy et de la variable d’heure supplémentaire :
-	Nombre de lignes : 1 237 733
-	Nombre de colonnes : 38
Après la suppression des variables redondantes, il reste 18 colonnes. Mais après dichotomisation et standardisation, on repasse à 222 colonnes.

Il convient de rappeler que les tests faits sur la base contenant ~ 1.2 millions de lignes n’aboutissent pas sur la machine utilisée pour les modèles de régression non linéaire. Une réduction de la base s’avère nécessaire pour ce périmètre. 
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
  
Les régressions Lasso et Ridge permettent de prévenir le surajustement et d’assurer la stabilité du modèle.

-	La régression Lasso : elle intègre une pénalité de norme L1 ce qui peut conduire à une sélection des variables en faisant le split entre les variables qui ont une contribution nulle sur la prédiction du modèle et celles qui ont un impact significatif. 

-	La régression Ridge : elle intègre une pénalité de norme L2 qui a tendance à réduire l’impact des variables les moins importantes plutôt que de les éliminer complètement. Le modèle Ridge est particulièrement utile lorsque les variables explicatives sont fortement corrélées entre elles, car il permet de stabiliser les coefficients et d'éviter une sensibilité excessive aux fluctuations dans les données. 

Les résultats obtenus sont les suivants :

![image](https://github.com/Ryma8905/Projet-datascientest/blob/main/Résultats_modèles/Resultats_modeles_naifs.csv)


**Il faut garder à l’esprit que les régressions linéaires et non linéaires ne sont pas réalisées sur des échantillons de tailles équivalentes.** 
Aucun modèle non linéaire ne semble produire de bons résultats. Surapprentissage, R2 négatifs… 
Pour ce qui est des modèles linéaires, ils semblent tous montrer les mêmes résultats. Le modèle Lasso est celui qui présente le moins de surapprentissage. Les R2 sont très bas mais le but de cette première étape de trouver les variables les plus contributives. Le modèle Lasso, de par la pénalité qu’il utilise nous permet de constater quelles sont les variables qui contribuent le plus au modèle et vont nous permettre in fine d’affiner nos travaux.  

En nous fiant au modèle Lasso simple pour les régresseurs linéaires, on constate qu’en réalité, peu de variables (par rapport au nombre initial) contribuent au modèle : 



![image](https://github.com/Ryma8905/Projet-datascientest/blob/fb1862b0f22f1c2b42decde54fef2cac5cdea03e/R%C3%A9sultats%20mod%C3%A8les/Contributions_variables.csv)


## Réflexion 
Les modèles dits naïfs ont servi de point de départ, offrant une compréhension initiale des relations linéaires et non linéaires entre les variables explicatives et les temps d'intervention. 
Nous allons donc procéder à une optimisation approfondie des hyperparamètres, via le GridsearchCV  pour garantir la performance du modèle avec une réduction drastique des dimensions et ce sur tous les modèles précédemment écartés dans l’optique de trouver les meilleurs modèles pour résoudre notre problématique. La totalité de la base a été utilisée. 



![image](https://github.com/Ryma8905/Projet-datascientest/blob/ea498526e119cc45002d074e0740fe3fe493874b/R%C3%A9sultats_mod%C3%A8les/Gridsearch.png)


On constate que les 3 modèles produisent peu ou prou les mêmes résultats. Les modèles linéaires sont ceux qui fournissent les meilleurs résultats compte tenu des postulats de départ. 
Nous allons donc procéder à une optimisation bayésienne sur ces derniers, avec les variables sélectionnées.  


![image](https://github.com/Ryma8905/Projet-datascientest/blob/655ca786cb919ee027bdc885520f53d0e647f3b7/R%C3%A9sultats_mod%C3%A8les/Optimisation%20bay%C3%A9sienne.png)


Le constat montre que les performances des 3 modèles sont identiques. Une cross validation opérée entre les 3 modèles avec les hyperparamètres alpha optimaux n’a guère permis de faire la différence. 

Régression Linéaire - Scores de validation croisée: [0.11237435 0.09124155 0.07112321 0.08179717 0.08109262]
**Moyenne des scores: 0.08752578036176409**

Lasso - Scores de validation croisée: [0.11235916 0.09123184 0.07113139 0.08180792 0.08109975]
**Moyenne des scores: 0.08752601128969313**

Ridge - Scores de validation croisée: [0.11237435 0.09124155 0.07112321 0.08179717 0.08109262]
**Moyenne des scores: 0.08752578036210472** 

Le seul critère de ségrégation serait celui du temps de traitement. Le modèle de régression linéaire simple est celui qui produit des résultats le plus rapidement. Il convient de rappeler que le dataset de départ a dû être amputé de beaucoup de variables et d’observations. En outre, les variables utilisées dans les modèles ne sont pas très parlantes en termes d’information orientée. 

## Interprétabilité 

Maintenant que le modèle de régression linéaire a été sélectionné, il convient de vérifier dans quelle mesure les variables ont contribué réellement au modèle en utilisant SHAP pour améliorer l’interprétabilité du modèle afin de comprendre comment chaque caractéristique contribue au modèle de manière équitable. 


### Shap 
Il convient de regarder dans quelle mesure chaque ligne de notre set de données contribue à la prédictibilité du modèle. De ce fait, on utilisera la magnitude pour mesurer l'impact global de cette caractéristique sur la sortie du modèle, en tenant compte de toutes les observations dans l'ensemble de données.
Si l’on veut prendre un exemple, la valeur SHAP associée à une modalité particulière d'une variable augmente, cela signifie que la présence ou l'augmentation de cette modalité a une contribution positive à la prédiction du modèle par rapport à la valeur moyenne de la variable cible. En d'autres termes, cette modalité est associée à une augmentation de la variable cible (dans notre cas, le temps d'intervention en secondes).

![image](https://github.com/Ryma8905/Projet-datascientest/blob/aaa2faea02d711c07dbb0220483fe64ce2a1c361/R%C3%A9sultats%20mod%C3%A8les/Resultats_magnitude_Shap.csv)

Mis en parallèle avec le graphique des features importances (plus parlant): 

![image](https://github.com/Ryma8905/Projet-datascientest/blob/ab31f3784a18f9c05f3442ae3ab9d5edacb848d6/R%C3%A9sultats_mod%C3%A8les/feature%20importances.png)

**1. TurnoutTimeSeconds (3 799 423.15)**
  - Avec la magnitude SHAP la plus élevée, cette variable est la plus déterminante pour le modèle. Cela signifie que le temps écoulé depuis l'appel jusqu'à l'arrivée de la brigade des pompiers est le facteur le plus significatif pour prédire le temps d'intervention.

**2. PumpCount (3 745 790.27)**
  - Cette variable a une magnitude SHAP très proche de celle de TurnoutTimeSeconds, ce qui indique qu'elle est également très influente dans la prédiction du temps d'intervention. Le nombre de pompes utilisées pendant l'intervention semble avoir un impact significatif sur la durée totale de l'intervention.
  
**3. NumStationsWithPumpsAttending (2 454 214.28)**
  - Bien que légèrement inférieure en magnitude par rapport à PumpCount, cette variable reste très importante dans la prédiction du temps d'intervention. Elle suggère que le nombre de stations avec des pompes intervenantes est un facteur clé pour prédire la durée de l'intervention.

**4. PumpOrder (2 319 695.67)**
  - Cette variable a une magnitude SHAP élevée, mais légèrement inférieure à celle de NumStationsWithPumpsAttending. Cela implique que l'ordre dans lequel les pompes sont utilisées peut également avoir une influence significative sur le temps d'intervention."),
 **5. Variables ProperCase et PropertyCategory**
  - Ces variables ont des magnitudes SHAP variées mais toutes sont significatives. Cela suggère que la localisation géographique (ProperCase) et la catégorie de propriété (PropertyCategory) jouent un rôle important dans la prédiction du temps d'intervention des pompiers."),
**6. StopCodeDescription**
  - Les différents types d'incidents ont également des magnitudes SHAP élevées, indiquant qu'ils sont des prédicteurs importants du temps d'intervention. Cela signifie que le type d'incident peut avoir une influence significative sur la durée de l'intervention."),
 **7. PumpHoursRoundUp (7 155.64)**
  - Cette variable a la magnitude SHAP la plus faible parmi toutes, mais elle reste significative. Cela pourrait indiquer que le nombre d'heures d'intervention (arrondi) a une influence moindre sur le temps d'intervention par rapport aux autres variables.

    
On peut conclure en disant que la caractéristique qui contribue le plus au modèle qui permet de prédire le temps d’intervention est le temps entre le moment où l’alerte arrive à la caserne et le moment où les pompiers partent. En effet, il semble logique que la caractéristique de temps de réponse influence considérablement le temps d’intervention.

Vient ensuite le nombre de pompes utilisées. En effet, plus il y a de pompes près du lieu d’incident,
plus grandes seront les chances de diminuer le temps d’intervention. 

Dans une moindre mesure, le nombre de stations intervenant contribue également en ce sens que plus de stations seront contactées, plus grandes seront les chances de diminuer le temps d’intervention.

Parmi les quartiers conservés, la plupart sont des quartiers centraux autour de la Tamise à l’exception de 3 qui sont à la périphérie et vastes. Les quartiers les plus centraux sont ceux qui contribuent le plus. On peut penser qu'une localisation de l'incident en centre-ville contribue plus à la prédictabilité de la variable cible que les quartiers périphériques. 


![image](https://github.com/Ryma8905/Projet-datascientest/blob/ab31f3784a18f9c05f3442ae3ab9d5edacb848d6/R%C3%A9sultats_mod%C3%A8les/feature%20importances%202%20.png)


Pour faire écho à ce qui a été dit précédemment sur la variable _TurnOutTime_, on constate à quel point elle peut contribuer aussi bien à la hausse et à la baisse au temps d’intervention. A l’instar de _TurnOutTime_, le graphique montre la grande amplitude d’influence qu’a aussi la variable du nombre de pompes à l’intervention. Elle contribue très positivement et très négativement également. Cela signifie que la variable à expliquer est très sensible à cette dernière et rejoint le point évoqué sur la magnitude. 


Une visualisation des Shap values pour un échantillon d'incidents permet de comprendre plus en détail le phénomène : 

![image](https://github.com/Ryma8905/Projet-datascientest/blob/7203c3b991f10007ec726e43b018aab97936a4cb/R%C3%A9sultats_mod%C3%A8les/shap%20sample.png)


On constate que sur 5 échantillons, la variable _TurnOutTime_ contribue le plus en valeur absolue. Idem pour le nombre de pompes. Cela conforte la conclusion faite au niveau macro. En fait, toutes les autres variables se comportent comme dans le graphique précédent. 



## Conclusion 

Il convient de rappeler avant toute chose que la data quality des datasets pour construire le modèle final n’était pas très riche. En effet, beaucoup de variables redondantes et manquantes ont contribué à appauvrir l’information disponible pour construire un modèle robuste et fiable.

De plus, les dictionnaires de données ne fournissaient pas de définition claire et ferme et il a fallu aller ‘fouiller’, regarder les modalités de chaque variable afin d’essayer de comprendre et d’affiner un peu plus la définition des champs.

La première partie du travail, la data préparation a permis d’émettre dès le début le postulat que le modèle ne serait pas très riche en ce sens que la suppression de beaucoup de champs et de lignes d’observations allaient amoindrir la robustesse du modèle.

La seconde partie de l’étude a consisté à tâtonner avec des modèles naïfs en première intention afin d’avoir des pistes de réflexion et d’améliorer de proche en proche les modèles étudiés.

En effet, les modèles ‘naïfs’ ont permis de voir la contribution des variables et d’éliminer celles qui ne participaient peu ou pas du tout au modèle. Le corollaire de cela est que la taille des datasets utilisés a pu être augmentée et ainsi améliorer la prédictibilité du modèle (toutes proportions gardées).

Un Gridsearch sur des modèles linéaires et non linéaires avec les variables préalablement sélectionnées a permis de conserver deux modèles qui fournissaient la meilleure combinaison en termes de minimisation de l’erreur, d’évitement du surapprentissage et d’augmentation de l’ajustement du modèle aux données.

C’est finalement un modèle linéaire (Lasso) qui a été sélectionné et a montré par le biais des magnitudes de SHAP que les contributions des variables au modèle étaient pour la plupart assez intuitives.

## Pistes de réflexion 

Lors de l'analyse de données, il est courant de rencontrer des ensembles de données incomplets, incohérents ou mal renseignés. Ces données peuvent grandement affecter la performance et la fiabilité des modèles d'apprentissage automatique, rendant ainsi les prédictions peu parlantes ou peu fiables. Face à de telles situations, plusieurs pistes de réflexion peuvent être explorées pour améliorer la qualité des données et, par conséquent, des modèles.

En tant que producteur de données, la qualité de l'information que vous fournissez est essentielle pour garantir la pertinence et la fiabilité de vos services. Face à des données de mauvaise qualité, plusieurs pistes de réflexion peuvent être envisagées :

**1. Évaluation et Transparence** : Fournir une évaluation transparente de la qualité des données, en identifiant les lacunes et les erreurs, afin de maintenir la confiance des utilisateurs.

**2. Amélioration des Processus de Collecte** : Réviser et améliorer les processus de collecte des données pour minimiser les erreurs et garantir leur exactitude dès le départ.

**3. Formation et Sensibilisation** : Sensibiliser le personnel aux enjeux de qualité des données et fournir une formation appropriée sur les bonnes pratiques de collecte et de gestion des données.

**4. Implémentation de Contrôles Qualité** : Mettre en place des contrôles qualité rigoureux tout au long du processus de collecte et de traitement des données pour détecter et corriger les erreurs rapidement.

**5. Collaboration avec les Utilisateurs** : Impliquer activement les utilisateurs dans l'identification et la résolution des problèmes de qualité des données, en recueillant leurs commentaires et leurs suggestions d'amélioration.

**6. Fourniture des Métadonnées** : Mettre à disposition des utilisateurs un dictionnaire de données clair et intelligible.
