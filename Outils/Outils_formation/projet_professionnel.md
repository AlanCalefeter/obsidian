
# **Conseils pour le titre**

- Présentation 35min pas 15min .
	- présentation application pour combler
	- appuyer sur le stage 
- Belle modélisation ( MCD , MLD ) clé étrangère, clé primaire
- Requête SQL => requête select from when (mes attributs)
- Savoir ce qu'est une jointure
- Les agressions SQL, les scripts dangereux attaque standard
	- expliquer comment faire sans framework (exploiter les failles !!)
							- Qui est attaqué et pourquoi + comment faire ?
- Pourquoi HTTPS ? chiffrer les données + utiliser un certificat 
- Logique BACK END  =>Développeur (web)
- Rapport pas 5 pages. Exprimer de façon claire
- Présenter notre site ( copie d'écran si il fonctionne pas )

# Conseils d'un jury 

- => Professionnels du métier
	- juge la capacité à faire ce métier ( grille avec capacités )
- Landing Page = Tout le FRONT END !! 
- git , github
- Figma
- mobile first => 78% des gens consultent sur tel
- Pas jugé sur la qualité du site
- 75% de la notation sur la présentation 
- 40 min d'entretient technique sur la présentation
- code à la main sur "comment récupérer des noms"
- "si j'ai pas de framework comment je fais"
- Connaître tous les acronyme ( "HTTP WPS SIO HTML CI/CD DEV OPS CSS DTO NPM DAO  [[vocabulaire-formation]])
- "Comment gérer une injection SQL ?"

# **les 8 compétences attendues** : 

- ###  1 - *Installer* et *configurer* son environnement de travail en fonction du projet (web ou web mobile)

- ###  2 - *Maquetter* des interfaces utilisateurs (web ou web mobile)

- ###  3 - Réaliser des *interfaces utilisateurs* statiques

- ###  4 - *Développer* la partie *dynamique* des *interfaces* utilisateurs (web et web mobile)

--- 

- ###  5 - Mettre en place une *base de données relationnelle* 
	- SQDB : PostegreSQL + installation/maj
			- suppression du dossier data 
			- placer le dossier binaire zip dans le dossier bin
	- Logiciel graphique "DataBase Client, DBVER"
		- extension de VScode
	- Modélisation d'une base de données
		- ERD ou E/A : Relation
		-  MCD : Relation entre les tables (cardinalités avec contraintes + dictionnaire de données)
		-  MLD : Ajoute la logique et les clés étrangères ( foreign key en bleu sur looping)
		- MPD (Modèle Physique de Données) : Création physique des tables (sur VScode)
		-  
- ###  6 - Développer des *composants d'accès* aux données *SQL* et *noSQL*
	- Se connecter à la base de données 
	- MPD : Modele physique 
	-  Afficher le SQL natif
	- Expliquer comment on l'a fait

- ###  7 - Développer des *composants* métier *côté serveur*

- ###  8 - Documenter le *déploiement d'une app* dynamique ( web ou web mobile )