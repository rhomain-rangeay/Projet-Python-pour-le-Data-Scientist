# Projet Python pour le data scientist - ENSAE 2A

*No covid world*

Ce soir, c'est la fin des exams, et tu es invité à un apéro. Il y aura tout le monde, et tu as bien envie de décompresser. En plus, c'est l'anniversaire de ta meilleure pote, alors évidemment, impossible d'arriver les mains vides. Tu passes au franprix, tu files au rayon bière bien décidé à ne pas y passer 2h. Mais là, c'est le trou noir, l'angoisse de la feuille blanche que tu pensais avoir délaissée ce matin pour un bon boût de temps.

Le problème : tu ne sais pas quoi prendre. Les classiques, tu connais. C'est vu et revu et puis de toutes façons là, tu as envie de nouveauté. Mais bon, le problème avec ce qui reste, c'est que tu ne sais pas trop ce que ça vaut... 

Mais te voilà sauvé ! Car on se fixe l'objectif, à l'issue de ce notebook, de te proposer une bière qui corresponde à celles que tu connais (et que tu aimes évidemment) déjà ! 

Pas d'enflammade, on ne lira pas dans ton cerveau ou toute autre histoire de ce genre. Non, on va plutôt analyser une belle base de données regroupant environ 360 000 bières, d'à peu près partout dans le monde, et surtout environ 10 millions (!) d'avis de consommateurs avisés qui ont dégusté à ta place le précieux nectar. Ces avis vont nous permettre de regrouper les bières similaires entre elles, à l'aide d'un clustering sur ces avis puis d'un algorithme de rule mining. Enfin, une petite fonction va tout rebrasser (pas les bières, enfin si mais en données, sinon ça mousse) et te proposera de manière aléatoire des bières, et dès que tu as trouvé une bière qui te plait, tu le signale et l'algorithme t'en propose une autre similaire à tester ! Pareil, si celle-ci ne te convient pas, tu peux relancer la recherche jusqu'à être comblé !

*On pourra éventuellement ajouter différentes contraintes sur cette sélection : budget, pays de provenance, analyse chimique de la bière... mais cela  dépendra de l'avancée et des ressources disponibles ! Bonne lecture et surtout bonne dégustation !*

## But du projet : 

	- Recommandation de bières selon les préférences d'un consommateur.
	- Classification des bières selon le profil de l'amateur de bières.
	- Prédiction de la qualité d'une bière à partir de se données physico-chimiques.

## Description des notebooks et fichiers :

**Remarque importante** : Les bases de données étant très volumineuses (plus de 25 Mo), il n'a pas été possible de les déposer sur github. Mais toutes les instructions afin de les télécharger vous-même et d'exécuter le code.
	
**Web scrapping beerwulf** : Nous avons effectué du web scrapping depuis le site beerwulf afin d'obtenir une base de données récente comprenant un peu plus d'un millier de bières ainsi qu'un panel d'informations telles que les paramètres physico-chimiques, le prix, l'origine, le style...
	
**data_beerwulf** : 
	
**data_beerwulf_with_id** : 
	
**Préprocessing des données (df_ml et data_beerwulf_with_id)** : Nous y avons effectué le nettoyage de notre autre base de données, plus conséquente et composée de trois tables (bières *beers*, brasseries *breweries* et surtout avis subjectifs des internautes *reviews* sur les bières), la jointure des tables et une sélection des variables auxquelles nous voulions appliquer l'algorithme de clustering. Nous avons donc pu construire une base de données spécifiquement dédiée à la future modélisation, que nous téléchargeons en local. Ensuite, nous avons tenté d'effectuer la jointure avec la base des données beerwulf, sans que nous ne possédions de clé unique spécifique.

**Prédiction de la qualité de la bière** :
	
**Notebook_ML** : C'est sur ce Notebook que nous avons effectué une analyse du modèle de clustering que nous avons appliqué au modèle. Nous avons récupéré la base construite dans *Préprocessing des données* et nous avons cherché à lui appliquer trois algorithme de clustering en modélisation simple : K-means, CAH et DBSCAN. C'est finalement le K-mean qui a été retenu, étant le seul algorithme applicable au volume des données. Nous avons zlors pu établir différents profils de consommateurs à partir des avis subjectifs de la table *reviews*. On exporte les infromations liées au clustering en local à l'issue du notebook (**il faudra adapter la destination du fichier**)

**Data_mining** : Nous avons récupéré les informations de *Notebook_ML* et, après un travail sur la mise en forme des données de façon à transformer les informations éparses d'un dataframe de plus de 750 Mo en une liste de listes, nous avons appliqué aux données un algorithme de rule mining : *APRIORI*. Cela a permis de regrouper entre-elles les bières dites "similaires", et qu'on peut recommander entre-elles à un consommateur le désirant. 
Enfin, un dernier programme permet de faire défiler des bières jusqu'à ce que l'utilisateur en choisisse une qu'il apprécie et se voit proposer une nouvelle bière semblable à découvrir.

