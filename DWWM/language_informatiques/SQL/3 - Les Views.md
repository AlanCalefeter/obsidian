## VIEW SQL definition :

- Une vue SQL est un objet logique associé à une requête SQL, souvent une requête **SELECT**. Elle ne stocke pas physiquement les données dans la base de données mais exécute la requête chaque fois qu'elle est sollicitée, assurant ainsi des résultats à jour.

## Création d'une **vue en SQL**  
  
- La création d'une vue se fait grâce à la clause **CREATE VIEW** suivie du nom que l'on donne à la vue, puis du nom des colonnes dont on désire agrémenter cette vue (il faut autant de redéfinitions de colonne qu'il y en aura en sortie), puis enfin d'une clause AS précédant la sélection.

## Bonnes pratiques 

```js
$sql = "SELECT id, titre, nom 
  FROM article 
  INNER JOIN utilisateur ON utilisateur.id = article.id_auteur";
$result = $mysqli->query($sql);
if ($result) {
  // Lister les résultats
  while ($row = $result->fetch_object()) {
    // Reste du code ...
  }
}
```