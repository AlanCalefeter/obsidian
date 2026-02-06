# 📝 HTML

HTML est un **langage universel** conçu pour distribuer l’information à l’échelle mondiale.

## ✨ Rôle du balisage HTML (HyperText Markup Language)

HTML permet de :

- Publier des documents en ligne (texte, tableaux, listes, images…)
- Créer des **liens hypertextes** en un clic
- Concevoir des **formulaires** pour des transactions ou services distants
- Intégrer des feuilles de calcul, vidéos, sons ou autres applications dans un document

## 🎯 Objectif de HTML

Représenter l’information.  
Les balises HTML sont interprétées par la plupart des navigateurs (Edge, Firefox, Safari…) et permettent l'affichage du contenu demandé.

---

# 🔵 HTML5 (depuis 2009)

## 📘 Les règles à respecter

1. Fermer toutes les balises  
2. Utiliser des balises et attributs en **minuscules**  
3. Mettre les valeurs d’attributs entre guillemets `""`  
4. Donner une valeur explicite à tous les attributs  
5. Utiliser les balises pour la **structure**, pas la présentation  
6. Utiliser des **feuilles de style (CSS)** pour la mise en forme

---

Une balise possède un nom qui permet de décrire son contenu  
→ langage sémantique

Une balise possède des attributs = paramètre sup à appliquer à la balise  
→ attribut : nom à qui on donne une valeur (une chaîne entre guillemets)  
→ balise + attribut (obligatoire ou facultatif)

★ id + class → attribut valeur libre

Le nombre d’attribut peut être variable

Certaines balises peuvent être imbriquées → ensemble hiérarchique  
= balise dans une balise (balise enfant)

---

# Structure d’un doc HTML  
Ordre à respecter :

→ la version HTML de la page : `<!DOCTYPE html>`  

→ un élément HTML qui comprend :

- une section en tête déclarative (encadrée par balise `<head>`)
- un corps qui comporte le contenu (encadré par `<body>`)

`<head>` et `<body>` peuvent elles-mêmes contenir des balises endossées  

→ Dans `<html>`, ne pas oublier l’attribut lang.

---

# En-tête du document `<head></head>`

→ titre, des mots-clés (pour références) et d’autres données qui ne sont pas considérées comme faisant partie du contenu du doc.

→ métadonnées `<meta>` (donne des indications sur la page, sans que ce soit visible)

Certaines balises de métadonnées sont obligatoires (`<meta charset="utf-8">`)  
facultatives et obsolètes  

`<meta charset="UTF-8">` → spécifie aux navigateurs l’encodage de la page web, la valeur standard est UTF-8.

cela évite des problèmes de caractères spéciaux ou d’accents mal affichés
-> Après la balise <head> -> avant <title>

La balise <link>
-> définit la relation entre doc et ressource externe (CSS, icône)
-> Utilisée pour définir un lien vers feuille de style ou ordre navigateur
(ex : accéder à la page dans une autre langue)
-> principalement utilisée pour CSS : <link href="style.css" rel="stylesheet">
<link rel="icon" type="image/png" href="favicon.png">
-> indique une icône de favori (« favicon ») pour un site.

Le corps du document : <body> </body>
-> textes, tableaux, images etc. -> visible par les internautes
-> éléments (balises) pour structurer la page (colonnes, blocs, paragraphes, menu…)
-> éléments de formatage (mise en forme, gras, italique, citations, métas…)

Commentaires :
-> l’internaute ne voit pas les commentaires
-> affiché dans le code source donc → Sécurité
-> pour voir le code source d’une page ctrl + U

#html #css #cours #frontend 