# 📌 Propriétés CSS essentielles

## 🎨 Apparence & texte

### `color`

Couleur du texte.

`color: #333;`

### `background-color`

Couleur de fond.

`background-color: lightgray;`

### `font-size`

Taille du texte.

`font-size: 1rem;`

### `font-weight`

Épaisseur du texte.

`font-weight: 600;`

### `line-height`

Espacement entre les lignes.

`line-height: 1.5;`

### `text-align`

Alignement horizontal du texte.

`text-align: center;`

---

## 📦 Box model

### `margin`

Espace extérieur autour d’un élément.

`margin: 16px;`

### `padding`

Espace intérieur entre le contenu et la bordure.

`padding: 12px;`

### `border`

Bordure de l’élément.

`border: 1px solid #ccc;`

### `box-sizing`

Contrôle le calcul des tailles.

`box-sizing: border-box;`

---

## 📐 Dimensions

### `width` / `height`

Largeur et hauteur.

`width: 100%; height: 50px;`

### `max-width`

Empêche un élément de devenir trop large.

`max-width: 1200px;`

---

## 📍 Positionnement

### `display`

Type d’affichage.

`display: block; display: inline; display: flex; display: grid;`

### `position`

Mode de positionnement.

`position: relative; position: absolute;`

### `top` / `right` / `bottom` / `left`

Décalage pour les éléments positionnés.

`top: 10px; right: 0;`

---

## 🧭 Flexbox (très utilisé)

### `display: flex`

Active Flexbox.

`display: flex;`

### `justify-content`

Alignement horizontal.

`justify-content: space-between;`

### `align-items`

Alignement vertical.

`align-items: center;`

### `gap`

Espace entre les éléments.

`gap: 16px;`

---

## 🧱 Grid

### `display: grid`

Active Grid.

`display: grid;`

### `grid-template-columns`

Définit les colonnes.

`grid-template-columns: 1fr 2fr;`

### `grid-template-rows`

Définit les lignes.

`grid-template-rows: auto 1fr;`

---

## 🌐 Responsive

### `@media`

Règles conditionnelles selon l’écran.

`@media (max-width: 768px) {   body {     font-size: 14px;   } }`

---

## 🖱️ Interaction

### `cursor`

Change le curseur.

`cursor: pointer;`

### `opacity`

Transparence.

`opacity: 0.7;`

### `transition`

Animation fluide.

`transition: all 0.3s ease;`

---

## 🎭 Effets visuels

### `border-radius`

Arrondit les coins.

`border-radius: 8px;`

### `box-shadow`

Ajoute une ombre.

`box-shadow: 0 4px 8px rgba(0,0,0,0.1);`

---

## 🧠 Utilitaires très pratiques

### `overflow`

Gestion du débordement.

`overflow: hidden; overflow: auto;`

### `z-index`

Ordre de superposition.

`z-index: 10;`

---

## ✅ Résumé rapide

|Catégorie|À retenir|
|---|---|
|Texte|color, font-size, line-height|
|Box|margin, padding, border|
|Layout|display, flex, grid|
|Responsive|media queries|
|UX|transition, cursor|

---