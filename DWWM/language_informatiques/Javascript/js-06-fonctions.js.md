 - Doit être écrit avec le terme ***function*** 
   
 - Sert à effectuer la tâche en un seul endroit
   
 - Nomenclature en camelCase suivi de parenthèses "( )"
   
 - Le code se place entre les accolades 
   
 -  Pour appeler la fonction :
	 -  nomFonction ( )

 -  Nous pourrions créer et appelé une nouvelle fonction greetLeslie( ); avec un code similaire.
```js
	 	function greetLeslie( ) {
	
  const name = "Leslie";
  console.log("Hello, " + name);
}
greetLeslie();
```

- au lieu d'écrire deux fonctions, on peut transmettre des infos spécifiques à une seule fonction grâce aux paramètres 
```js
function greet(name){
console.log("Hello, " + name);
}
greet("April");
greet("Leslie");
```

 - On peut retourner les valeurs d'une fonction avec le mot clé "return"
 - On peut stocker la valeur retour dans une variable et l'afficher dans la console
```js
	 function userAge(number) {
  const age = "User age: " + number;
  return age;
}
console.log(userAge(22));

const result = userAge(29);
console.log(result);
```

 - On peut mettre plusieurs paramètre dans une fonction séparé par des virgules 
```js
	 function display(firstName, lastName) {
  console.log(firstName + " " + lastName);
}
display("Alex", "Morgan");
```

- Les fonctions sont des actions, leurs nom doivent contenir au moins un verbe
	- Lorsqu'il y a plusieurs mots, le verbe est un préfixe, comme sumTotal.
	- Les fonctions qui renvoient une valeur sans la modifier de quelque manière que ce soit commencent par des verbes comme get.
	- les fonctions qui renvoient des valeurs booléennes commencent par is.

- Les types de valeur sont importants lorsque les fonctions effectuent des opérations

- La sortie d'une fonction n'a pas besoin d'être du même type que l'entrée.

-  Les fonctions peuvent avoir tous type de valeurs en paramètre comme par exemple des tableaux
```js
function displayNames(names) {
  console.log(names);
}
const students = ["Laurel", "Yannis"];

displayNames(students);

function displayNumberOfNames(names) {
  console.log(names.length);
}
displayNumberOfNames(students);

function displayFirstName(names) {
  console.log(names[0], names[1]);
}
displayFirstName(students);
```

[[learn-scope.js]] 
