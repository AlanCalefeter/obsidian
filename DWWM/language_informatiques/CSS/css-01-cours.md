
# 🎨 Cours de CSS (pour Obsidian)

## 1️⃣ Qu’est-ce que le CSS ?

**CSS (Cascading Style Sheets)** permet de :

- mettre en forme le HTML
    
- gérer les couleurs, tailles, positions
    
- créer des mises en page responsives
    
- améliorer l’expérience utilisateur
    

👉 **HTML = structure**  #html 
👉 **CSS = apparence** #css 

---

## 2️⃣ Comment utiliser le CSS

### 2.1 CSS externe (recommandé)

`<link rel="stylesheet" href="style.css">`

### 2.2 CSS interne

`<style>   body {     background-color: white;   } </style>`

### 2.3 CSS en ligne (à éviter)

`<p style="color: red;">Texte</p>`

---

## 3️⃣ Syntaxe de base

`selecteur {   propriete: valeur; }`

Exemple :

`p {   color: blue;   font-size: 16px; }`

---

## 4️⃣ Sélecteurs CSS

### 4.1 Sélecteurs simples

`p { } h1 { }`

### 4.2 Classe

`.card {   border: 1px solid black; }`

`<div class="card"></div>`

### 4.3 Identifiant (id)

`#main {   width: 100%; }`

`<div id="main"></div>`

### 4.4 Sélecteurs combinés

`div p { } div > p { } h1 + p { }`

---

## 5️⃣ Le modèle de boîte (Box Model)

Chaque élément est composé de :

- margin (extérieur)
    
- border
    
- padding
    
- content
    

`.box {   margin: 10px;   padding: 20px;   border: 2px solid black; }`

💡 Astuce essentielle :

`* {   box-sizing: border-box; }`

---

## 6️⃣ Couleurs et unités

### 6.1 Couleurs

`color: red; color: #ff0000; color: rgb(255, 0, 0);`

### 6.2 Unités

|Unité|Description|
|---|---|
|px|fixe|
|%|relatif|
|em|relatif au parent|
|rem|relatif à html|
|vw / vh|taille écran|

---

## 7️⃣ Positionnement

### 7.1 Position

`position: static; position: relative; position: absolute; position: fixed; position: sticky;`

### 7.2 Exemple

`.badge {   position: absolute;   top: 10px;   right: 10px; }`

---

## 8️⃣ Flexbox (indispensable)

### 8.1 Conteneur

`.container {   display: flex;   justify-content: space-between;   align-items: center; }`

### 8.2 Axes

- axe principal : horizontal
    
- axe secondaire : vertical
    

### 8.3 Propriétés clés

- justify-content
    
- align-items
    
- gap
    
- flex-direction
    

---

## 9️⃣ Grid (mise en page avancée)

`.grid {   display: grid;   grid-template-columns: 1fr 2fr;   gap: 20px; }`

Idéal pour :

- layouts complexes
    
- pages complètes
    

---

## 🔟 Responsive design

### 10.1 Media queries

`@media (max-width: 768px) {   body {     font-size: 14px;   } }`

### 10.2 Bonnes pratiques

- mobile first
    
- unités relatives
    
- flex + grid
    

---

## 1️⃣1️⃣ Héritage et cascade

Priorité CSS :

1. inline
    
2. id
    
3. class
    
4. élément
    

`p {   color: blue; }`

`.text {   color: red; }`

👉 `.text` gagne

---

## 1️⃣2️⃣ Pseudo-classes et pseudo-éléments

### Pseudo-classes

`a:hover { } input:focus { }`

### Pseudo-éléments

`p::first-letter { } p::after { }`

---

## 1️⃣3️⃣ Bonnes pratiques CSS

- noms de classes clairs
    
- éviter les ids pour le style
    
- un fichier CSS par responsabilité
    
- commenter quand nécessaire
    

`/* Carte produit */ .card { }`

---

## 1️⃣4️⃣ Organisation recommandée

`css/ ├── base.css ├── layout.css ├── components.css └── pages/`

---

## 1️⃣5️⃣ Résumé express

- CSS contrôle l’apparence
    
- Flexbox et Grid sont essentiels
    
- Responsive = obligatoire
    
- Simplicité > complexité

#css #frontend #cours 