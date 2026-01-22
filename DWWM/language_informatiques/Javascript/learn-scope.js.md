- Le Scope ou la portée de variable
  
- Fait référence à la portée ou à la visibilité des variables, fonction et autre éléments du code

- Il détermine les parties du code où vous pouvez accéder et utiliser ces éléments.

- Le Scope évite les conflits de noms

- L'importance du scope dans la création de votre code réside dans les aspects suivants:

		1 - Encapuslation : limite l'accès aux variables à des parties spécifiques de votre code, - risques de modification accidentelle

		2 - Prévention des conflits de noms: assure que variable ou fonction ont a nom unique à l'intérieur de leur propre scope. 

		3 - Séparation des préoccupations : peut séparer les différentes parties de votre code en fonction de leur fonctionnalité ou de leur responsabilité. + lisible + maniable + modulaire

		4 - Durée de vie des variables:Les variables déclarées dans un scope local ne sont accessibles que tant que ce scope est actif puis supprimé quand plus nécessaires. + gestion de mémoire - fuites de mémoire

 A - Scope global :
Le scope global est le scope le plus large. Les variables déclarées en dehors de toute fonction ou bloc de code avec var, let ou const ont une portée globale, ce qui signifie qu'elles sont accessibles depuis n'importe où dans le code.
```js
const globalVariable = "Je suis une variable globale";
function myFunction() {
  console.log(globalVariable); // Accès à la variable globale
}
myFunction(); // Affiche "Je suis une variable globale"
```

B - Scope local de fonction :
Les variables déclarées à l'intérieur d'une fonction avec var, let ou const ont une portée locale à cette fonction. Elles ne sont accessibles qu'à l'intérieur de la fonction.
```js
function myFunction() {
  const localVariable = "Je suis une variable locale";
  console.log(localVariable); // Accès à la variable locale
}
myFunction(); // Affiche "Je suis une variable locale"
console.log(localVariable); // Erreur : la variable locale n'est pas accessible en dehors de la fonction
```

C- Scope de bloc:
 Les variables déclarées avec let et const à l'intérieur d'un bloc de code
 (par exemple, une boucle for, une condition if, etc.) ont une portée limitée à ce bloc.
 Elles ne sont pas accessibles en dehors du bloc.
```js
 function myFunction() {
  if (true) {
    let blockVariable = "Je suis une variable de bloc";
    console.log(blockVariable); // Accès à la variable de bloc
  }
  console.log(blockVariable); // Erreur : la variable de bloc n'est pas accessible en dehors du bloc
}
myFunction();
```

> [!error]+ Important
> ! Les variables déclarées avec var ont un scope de fonction et non de bloc.
> ! Elles peuvent être accessibles en dehors du bloc dans lequel elles sont déclarées.
