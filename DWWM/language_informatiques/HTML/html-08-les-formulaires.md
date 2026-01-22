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

L’attribut **datalist** et **output** sont HTML5. ## **Déclarer un formulaire :**

→ Formulaire : `<form></form>`

Entre les 2 il y a :  
→ champs texte, liste déroulante, cases à cocher  
→ et 1 bouton d’envoi (soumission du formulaire)

`<form>` → **action** et **method**.  
Autres attributs traditionnels mais facultatifs : **name**, **id**…