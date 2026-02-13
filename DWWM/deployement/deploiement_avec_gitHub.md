# Déploiement avec GitHub

- pipeline (ci/cd) => *git local* vers *GitHub* puis avec un *hébergeur*, on déploie le projet
- envoyer sur GitHub puis choisir un hébergement ([railway](https://railway.com/?referralCode=fZIRHs&gad_source=1&gad_campaignid=23516255646&gclid=CjwKCAiAkbbMBhB2EiwANbxtbZ8q5tsMRb0HbxvdJ-n7uFnsrGZVuDrPxRyh7JrEQsTYtZlPUpz3MxoCvl4QAvD_BwE), [render](https://render.com/) etc...) qui sont des sites américain gratuit et rattachable avec GitHub 
- Il faut *créer* un fichier pour build le projet 
- l'hébergement crée automatiquement le déploiement avec la pipeline
- vérifier sur l'hébergeur les paramètres et choisir de déployer en Europe
- L'hébergeur a tout pour configurer en seulement qques clic!
- "crash car il manque l'environnement" => regarder les logs
- choisir d'utiliser les variables d'environnements
- crée un *dockerfile*  (copier la documentation) : permet de dire a l'hébergeur quoi utiliser
- utiliser le package.json et modifier le "start" de "script" en désigant directement le "node src/app.js"
- */app.js*  => en dessous de const app =express(), rajouter
```js
if (process.env.NODE_ENV === "production"){
	app.set("trust proxy", 1);
}   //OBLIGATOIR en production
```
- commander : git add; git commit; git push
- allez sur l'hébergeur et vérifier les logs et enlever les variables d'environnement inutile  du .env de l'hébergeur
- choisir la base de donnée dans l'hébergeur (postgre service)
- allez dans setting et générer un domaine quand le build et fini 