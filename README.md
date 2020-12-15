# Projet Python pour le data scientist - ENSAE 2A
Romain Lefranc, Simon Mariani

*------------------------------------------------------ No covid world -------------------------------------------------------------------*

Ce soir, tu es invité.e à un apéro pour fêter la fin des examens. Beaucoup de personnes seront présentes et tu as bien envie de décompresser. En plus, c'est l'anniversaire de ta meilleure amie, alors évidemment, impossible d'arriver les mains vides. Les festivités commencent dans 30 minutes. Tu te rends au Franprix d'un pas pressé et tu vas tout droit au rayon bières, bien décidé.e à choisir vite. Mais là, c'est le trou noir, l'angoisse de la feuille blanche que tu pensais avoir délaissée ce matin pour quelques temps.

Le problème : tu ne sais pas quoi prendre... classique ! C'est vu et revu et d'ailleurs, tu as envie de nouveautés ce soir. Par contre, tu ne sais pas trop ce que valent toutes les bières proposées... 

Mais te voilà sauvé.e ! À l'issue de ce notebook, nous nous fixons l'objectif de te proposer une bière qui correspond à celles que tu connais (et que tu aimes évidemment) déjà ! 

Pas d'enflammade, on ne lira pas dans ton cerveau ou toute autre histoire de ce genre. Non, nous allons plutôt analyser une belle base de données regroupant environ 360 000 bières provenant des quatre coins du monde, et surtout environ 10 millions (!) d'avis de consommateurs avisés qui ont dégusté à ta place le précieux nectar. Ces avis vont nous permettre de regrouper les bières similaires entre elles, à l'aide d'un clustering sur ces avis puis d'un algorithme de rule mining. Enfin, une petite fonction va tout rebrasser (pas les bières, enfin si, mais les données, sinon ça mousse) et te proposera de manière aléatoire des bières, et dès que tu as trouvé une bière qui te plait, tu le signales et l'algorithme t'en propose une autre similaire à tester ! De même, si celle-ci ne te convient pas, tu peux relancer la recherche jusqu'à être comblé.e !

*-------------------------------------------------- Even if covid world ------------------------------------------------------------------*

Nous sommes déjà en décembre, les fêtes de fin d'année approchent à grand pas, et tu n'as pas encore trouvé de cadeaux à offrir à ta famille. Ton père a un penchant pour le houblon et tu l'as déjà entendu dire qu'il se lassait des bières "mainstream" vendues dans les grandes surfaces ? Ses remarques te mettent la puce à l'oreille pour trouver une idée de cadeau : tu te doutes qu'il apprécierait un coffret de bières de bonne qualité à déguster. Néanmoins, tu ne sais même pas que le malt est une céréale, et pas seulement une île... 

Tu n'as pas envie qu'un expert (ou bien un algorithme de rule mining !) te propose des bières qui correspondent au goût de ton père comme précédemment, tu veux lui offrir des bières de bonne qualité. Par exemple des bières remarquables par l'harmonie entre son amertume et l'intensité de ses arômes fruités. Tu as reçu le catalogue du nouveau brasseur du coin dans ta boîte aux lettres  et tu te demandes si ses offres pourraient faire plaisir à ton père. Bien évidemment, toutes les bières de son prospectus semblent de qualité, mais tu aimerais avoir un avis tranché sur la question. Nous te proposons donc de regarder les caractéristiques physiques et chimiques des bières pour savoir déterminer sa qualité de façon objective. 

*Bonne lecture et surtout bonne dégustation !*

## But du projet : 

- Classification et recommandation de bières selon les préférences d'amateur de bières.
- Prédiction de la qualité d'une bière à partir de se données physico-chimiques.

Un des challenges de notre projet est de trouver des bases de données à exploiter. Les sites d'e-commerce qui vendent des bières sont nombreux, mais les sites Open Data des bières sont rarissimes. Notre projet s'appuie donc sur les données de deux sites : 
- d'une part, les données du site www.beeradvocate.com : elles regroupent les données de bières et de leur brasseries, ainsi que des avis laissés par des consommateurs sur leur degustation.  
- d'autre part, le site de e-commerce www.beerwulf.com : ce site renseigne très précisément les caractéristiques physico-chimiques des bières vendues. Nous avons donc recouru au web-scraping pour constituer un nouveau dataset qui servira à prédire la qualité d'une bière. 

Tous les notebooks présents suivent un ordre logique : le web-scraping, puis le preprocessing des données avec des statistqiues descriptives, et enfin l'implémentation des modèles. 

## Description des notebooks et fichiers :

**Remarque importante** : Les bases de données étant très volumineuses (plus de 25 Mo), il n'a pas été possible de les déposer sur github. Mais toutes les instructions afin de les télécharger soi-même et d'exécuter le code sont détaillées.
	
**0. Web scraping beerwulf** : Nous avons effectué du web scraping depuis le site beerwulf afin d'obtenir une base de données récente comprenant un peu plus d'un millier de bières ainsi qu'un panel d'informations telles que les paramètres physico-chimiques, le prix, l'origine, le style...
	
**1. Préprocessing des données** : 
- Nous y avons effectué le nettoyage de notre autre base de données, plus conséquente et composée de trois tables (bières *beers*, brasseries *breweries* et surtout avis subjectifs des internautes *reviews* sur les bières). Nous avons ensuite réalisé la jointure des tables et une sélection des variables auxquelles nous voulions appliquer l'algorithme de clustering. Ce notebook construit ainsi une base de données spécifiquement dédiée aux algorithmes de recommandation des bières, que nous téléchargeons en local. 
- Dans un deuxième temps, nous avons regroupé les avis subjecifs et la base de données scrappées. Cette partie détaille les étapes pour trouver la correspondance entre ces deux bases qui n'ont pas clé de jointure. Nous disposons ainsi d'un deuxième dataset qui sera utilisée pour les modèles prédictifs de la qualité des bières. 
	
**2. Clustering des avis** : C'est sur ce Notebook que nous avons effectué une analyse du modèle de clustering que nous avons appliqué au modèle. Nous avons récupéré la base construite dans *Préprocessing des données* et nous avons cherché à lui appliquer trois algorithme de clustering en modélisation simple : K-means, CAH et DBSCAN. C'est finalement le K-mean qui a été retenu, étant le seul algorithme applicable au volume des données. Nous avons alors pu établir différents profils de consommateurs à partir des avis subjectifs de la table *reviews*. On exporte les informations liées au clustering en local à l'issue du notebook (**il faudra adapter la destination du fichier**).

**2bis. Data_mining** : Nous avons récupéré les informations de *Notebook_ML* et, après un travail sur la mise en forme des données de façon à transformer les informations éparses d'un dataframe de plus de 750 Mo en une liste de listes, nous avons appliqué aux données un algorithme de rule mining : *APRIORI*. Cela a permis de regrouper entre-elles les bières dites "similaires", et qu'on peut recommander entre-elles à un consommateur le désirant. 
Enfin, un dernier programme permet de faire défiler des bières jusqu'à ce que l'utilisateur en choisisse une qu'il apprécie et se voit proposer une nouvelle bière semblable à découvrir.

**3. Prédiction de la qualité de la bière** : implémentation de modèles de régression pour déterminer la qualité d'une bière à partir de ses cracatéristiques physico-chimiques. Ce notebook vise à tester plusieurs modèles supervisés (*Régression linéaire*, *Random Forest* et *Decision Tree*), puis de les évaluer afin de retenir le plus performant. Dans un premier temps, nous nous focalisons uniquement sur les caractéristiques physiques et chimiques des bières, puis nous ajoutons le style de la bière dans la régression pour tenter d'améliorer les résulats dans un deuxième temps. In fine, la modélisation avec l'algorithme *Random Forest* s'avère être le plus performant.


# Conclusion :

Les modèles ont pu satisfaire nos attentes et relever les challenges que nous nous étions fixés. Nous sommes satisfaits d'avoir pu transformer un problème quotidien en un problème de machine learning et de constater que les résultats sont très satisfaisants. Ce projet a été très formateur : 
- nous maîtrisons désormais le web scraping pour des sites codés en HTML ou bien en JavaScript, 
- nous avons gagné en aisance pour manipuler les données avec la librairie pandas ou encore pour visualiser les données avec la librairie seaborn.
- nous nous sommes familiarisés avec des modèles de machine learning disponibles grâce à la librairie scikit-learn. Plus singulièrement, nous avons été amenés à utiliser des modèles d'apprentissages supervisés et non supervisés pour répondre à notre problématique.
- nous essayons au mieux de prendre du recul sur la validité des données et d'avoir un avis critique sur les résultats obtenus.

# Prolongement et limites du projet

Si le temps et les ressources le permettaient, nous aimerions améliorer nos algorithmes en ajoutant des contraintes qui rendraient le résultat d'autant plus satisfaisant et poussé. 

Par exemple, nous ne prenons pas en compte le budget d'un consommateur particulier qui souhaite acheter plusieurs bières (qu'elles lui soient recommandées ou bien de bonne qualité !). 

De même, nous n'avons pris en compte qu'un nombre de features restreint, et il serait intéressant d'en ajouter afin de pouvoir recommander à un consommateur une bière qu'il puisse réellement trouver sur l'étalage en face de lui (prise en compte du pays d'origine, de la popularité de la brasserie...) ; voire de proposer des filtres sur la recommandation souhaitée (pourcentage alcoolique souhaité, style de la bière...).

De plus, pour la partie dite de "Data Mining", nous n'avons pas pu utiliser la totalité de la base de données à la fois pour effectuer de la recommandation : celle-ci s'effectue par échantillon de 1000 données en raison de la capacité réduite de nos ordinateurs portables (la liste de listes que l'on rentre dans l'algorithme *apriori* ne peut pas être trop lourde pour un ordinateur de 8 GO de RAM). Et bien qu'il soit possible de relancer un échantillonage si le précédent ne donnait pas satisfaction, il serait intéressant de voir une recommandation effective sur les 400 000 bières collectées.

Pour la partie recommandation, il pourrait également être intéressant de recueillir la satisfaction du consommateur par rapport à la bière recommandée, puis d'utiliser cet historique global afin d'apporter de l'information supplémentaire lors de futures recommandation (l'algorithme apprendrait au fur et à mesure du temps).

Enfin, il serait évidemment optimal de pouvoir travailler sur la forme et la production de ce notebook afin de rendre son exécution digeste pour un consommateur ordinaire, à travers une application ou un site web par exemple. 

Néanmoins, les amateurs de bières peuvent déjà tester ces algorithmes pour trouver une nouvelle bière à déguster. 
