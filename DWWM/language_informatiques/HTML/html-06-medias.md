
# **HTML – 06 – Médias**

## **Les bases des images**

### `<img>`

→ plusieurs attributs.  
→ `src` (source) → spécifie l’URL.

`<img>` ne contient pas de texte : doit être immédiatement fermée.  
Ex. :

```
<img src="nomdufichier" />   ⚠ slash "/"
```

---

## **Texte de remplacement**

→ attribut **alt**, obligatoire.

Deux avantages :

1. Si pas d’image, l’internaute (et les moteurs de recherche) peuvent quand même lire l’image.
2. Fournit une légende à une image, qui s’affiche par souris.

Ex. :

```
<img src="logo windows.jpg" alt="logo windows" />
```

---

## **2e Attribut :** `**title**`

→ permet d’indiquer un titre à votre image.  
Balise facultative mais fortement conseillée (pour référencement sur moteurs de recherche et synthèse vocale).  
→ court et souvent comme alt.

Ex. :

```
<img src="logo windows.jpg" alt="logo windows" title="logo windows" />
``` ## **Positionnement et alignement**

→ Par défaut, l’image place la ligne de texte à présent alignée **s’il le bas de l’image**.  
→ Avec HTML5 il n’y a plus de : align / border / hspace.

---

## **Taille de l’image**

**taille de l’image → width + height → taille en pixel (px) de l’image**

Ex. :

```
<img src="logo windows.jpg" width="225" height="225">
```

⚠️ **Attention aux formats** (smartphones, tablettes…).

---

# **Les autres balises d’images**

## **Les zones réactives**

La balise `<img>` peut être découpée en zones dites réactives ; chaque zone découpée (selon des points de coordonnées) devient cliquable (c-à-d un lien avec une URL de destination).

L’attribut **usemap** indique cette zone avec autre attribut HTML.

`<map>` → affiche l’image → l’aire permet de nommer à `<map name="">` → préciser la destination, la forme et les points de coordonnées de la forme de zone souhaitée.  
La destination prend en cliqué et un attribut alt (texte descriptif / alternatif).

```
<area> → shape et coords          (forme arrie ?)   (coordonnées de la zone)
```

---

## **La Balise** `**<figure>**`

`<figure>` → légende à une illustration (image, schéma, tableau, vidéo, code etc.)  
→ spécifié dans la balise enfant `<figcaption>` :

---

## **La Balise** `**<picture>**`

`<picture>` → plusieurs sources d’images dans une même balise `<img>`  
→ concerne la **web responsive**  
→ même image mais dimensions et cadrages ≠ # **Les autres Médias**

## **Vidéo**

`<video>` → depuis HTML5

3 formats vidéos sont reconnus par les navigateurs :

- mp4 (H.264 AAC)
- webm (Matroska)
- ogg (Theora)

→ nécessite la conversion avec logiciel (ex : VLC)

### **Attributs de réglage vidéo :**

- **controls** → accès au contrôle de lecture (bouton, volume etc.)
- **preload**
    - `"auto"` → débute le téléchargement
    - `"true"` → lance la lecture automatiquement
    - `"image.jpg"` → indique une image (aperçu)
- **loop** → lecture en boucle

Sur une page web, beaucoup de vidéos sont intégrées via **YouTube**.  
Si problème, ajout de type MIME : _…Attacces_ (dans tes notes).

---

## **Sons**

`<audio>` → attribut similaire à `<video>`

---

## **La balise** `**<object>**`

`<object>` → intègre ressource externe considérée comme “plug-in” (fichier PDF ou Flash par exemple).  
→ la balise peut inclure des HTML d’un autre fichier.

---

## **La balise** `**<embed>**`

`<embed>` → globalement similaire à `<object>`

---

## **La balise** `**<iframe>**`

`<iframe>` → intègre une page HTML dans la page HTML courante.  
→ affiche sans rechargement une fenêtre dite “pop-up”.