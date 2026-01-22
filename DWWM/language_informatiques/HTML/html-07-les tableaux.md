# **HTML – 07 – tableaux**

## **Création d’un tableau**

`<table></table>` → composé de plusieurs lignes encadrées par `<tr></tr>`  
→ chaque ligne composée de plusieurs cellules par `<td></td>`

Aujourd’hui, structuration et positionnement se fait par `<div>`, `<header>`, `<footer>`, `<nav>` etc.

---

## **Titre**

→ permet d’ajouter un titre (ou légende) à un tableau via `<caption>`  
qui doit être placé directement sous la balise `<table>`.

---

## **Mise en forme avancée**

### **En-têtes et Pieds**

### **En-têtes**

Chaque cellule de la première ligne (titre colonne) est repérée par `<th>`  
encadrée dans une balise `<thead>` et une ligne `<tr>`.

→ balise qui ne s’utilise qu’une seule fois par tableau. Sinon utiliser `<tbody>` et `<tfoot>`.

### **Pieds**

`<tfoot>` permet d’indiquer des cellules en pied de tableau (ex : total de colonnes dans tableau de chiffres).

→ contrairement à `<thead>`, `<tfoot>` n’a pas de balise `<th>`.

---

`<tbody>` → dès que `<thead>` et/ou `<tfoot>`, il faut mettre `<tbody>`  
(facultative mais respecte le web sémantique).

La balise se place après `<thead>` et se termine avant `<tfoot>`.

---

## **Regroupement de lignes / colonnes**

On peut regrouper plusieurs lignes ou plusieurs colonnes pour des cellules dépendantes. ## **L’Attribut colspan**

L’attribut **colspan** sur une balise `<td>` prend une valeur numérique  
qui indique le nombre de colonnes à regrouper. La cellule s’étendra sur  
le nombre de colonnes indiquées comme valeur.

---

## **L’Attribut rowspan**

L’attribut **rowspan** est à appliquer à `<td>`, prend une valeur numérique  
qui indique le nombre de lignes à regrouper. La cellule s’étendra sur  
le nombre de lignes indiquées en valeur.

---

## **Habillage de colonne et de lignes**

HTML5 crée les nouvelles balises `<colgroup>` et `<col>` qui permettent,  
avec des feuilles CSS, de créer via un habillage visuel (ou simplement  
visuel) contournant **colspan** et **rowspan** de colonnes d’un tableau.  
Par ex., on applique une couleur de fond sur les 6 premières colonnes tandis que  
une 3e colonne aura une autre couleur de fond.

---

# **HTML – 08 – Les formulaires**

→ Permet aux internautes d’effectuer une saisie et de les envoyer  
vers le site web pour y être traitées (grâce à un script CGI, ASP.net ou PHP).

Les saisies dans un formulaire peuvent s’effectuer par :

- des champs de saisie de texte ;
- zones de texte multilignes ;
- liste de choix (combobox ou liste déroulante) ;
- des cases à cocher (checkbox pour des choix multiples de réponses) ;
- des boutons radio qui imposent un choix unique de réponse (oui/non, madame, monsieur) ;
- il est aussi possible de télécharger un fichier.

L’attribut **datalist** et **output** sont HTML5.