
# **HTML – 04 – Les liens**

`<a>` → lien hypertexte permettant :

- une autre page
- une autre section
- une partie de la page courante
- une ressource (fichier, image, vidéo, etc.)

```html
<a href="page1.html" title="page suivante">cliquez ici</a>
```

Un lien est composé de trois parties et attributs :

- **attribut** `**href**` → obligatoire → valeur = destination du lien
- **attribut** `**title**` → obligatoire → valeur = texte explicatif
- **texte affiché** sur la page web

#### **title** → texte affiché au survol de la souris.

####**target** → indique dans quelle fenêtre (onglet) s’ouvre le doc.

- **_blank** → ouverture nouvelle fenêtre
- **_self** → ouverture fenêtre courante
- **_parent** → fenêtre “parente” (pop-up par ex.)
- **_top** → ouvre la page de fenêtre parente niveau 1 (s’il n’y a pas de fenêtres parentes, sinon agit comme `_self`)

---

## **Liens entre 2 pages**

On peut naviguer entre 2 pages HTML, de la manière suivante :

- **Dans le même répertoire que celle qui contient** `**<a>**`

```
<a href="page2.html" title="ouvrir une 2ème page">Cliquez ici</a>
```

- **Dans un** _**sous-répertoire**_ **du répertoire qui contient la page avec** `**<a>**`

```
<a href="monsousrepertoire/page2.html" title="2ème page">Cliquez ici</a>
```

- **Dans un autre répertoire (hors du répertoire qui contient** `**<a>**`**)**

```
<a href="../repertoireexterne/page2.html" title="clic">Cliquez ici</a>
```

---

## **Liens interne à la page**

→ peuvent naviguer dans la même page HTML. Un lien permet d’accéder directement à une autre balise dans la balise, de la balise (phrase peu claire mais je retranscris à l’identique).

Un attribut **id** :

```
<p id="lacible">blablabla</p>
```

→ Va au paragraphe nommé **lacible**

```
<a href="#lacible" title="aller à la cible">aller au paragraphe bla bla</a>
```

Pour aller vers un élément cible situé sur une autre page, on indique dans l’attribut **href** le signe # identifiant de la cible précédé du signe `/`.