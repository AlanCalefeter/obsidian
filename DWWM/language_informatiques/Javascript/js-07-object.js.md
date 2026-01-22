
# Sommaire :
[[#Les Objects en javascript]]
[[#Qu'est ce qu'un JSON]]

## Les Objets en javascript

- Les object servent à ranger plusieurs variable dans une même boite
- On crée des object de la même manière que les variables avec le mot clé "const" suivi d'un nom, d'un signe "=" et des accolades "{ }"
  
```js
const cat = {
  name: "Garfield",
  favoriteFood: "Lasagna",
};
```

- Pour ajouter plus de propriétés à un objet, commencez par une virgule,
 puis ajouter la propriété. Comme pour le css (voir [[_sommaire_css]] ) 
-  Un objet peut avoir autant de propriétés que nous le souhaitons,
 tant que chaque propriété est séparée par une virgule.
- Les propriétés d'un objet peuvent être des numbers, des strings,
des booleans, des arrays(tableaux) ou même d'autres objets.
- Nous accédons à la propriété d'un objet en utilisant le nom de l'objet,
 un "." et le nom de la propriété
 
```js
const person = {
  name: "Joe Exotic",
  nickname: "Tiger King",
  occupation: "Zookeeper",
  age: 57,
};
console.log(person.nickname);

```


## Qu'est ce qu'un JSON 

- signifie JavaScript Object Notation
- utilisé pour échanger des données entre les appli Web et les serveurs 
- JSON ressemble à une version stringifiée d'un objet JS normal.
- Nous pouvons créer JSON_VARIBLE comme un objet normal "{}", mais entouré de guillemets simples " ' ".
- Un objet JSON contient une collection de paires clé-valeur, similaire à un objet JS.
- Cependant, dans JSON, nous devons inclure les clés entre guillemets, comme "times" ici.
```json
const JSONVariable = '{"story": "life", "times":2, "fiction": true}';
```

- Les objets JSON peuvent collecter des données statiques telle que des nombres, des tableaux, des booléens ou des strings.
- Cependant, ils ne peuvent pas stocker de fonctions à l'intérieur.
  
```json
const JSONVariable1 = '{"story": "life", "times":2, "fiction": function(){}}';
```

- Nous pouvons convertir un objet JS en JSON avec la méthode JSON.stringify( ).
- Ici, nous pouvons convertir l'objet concert JS en un objet JSON si nous utilisons JSON.stringify(concert).
  
```js
const concert = {
  band: "Super Carrots",
  music: "Indie",
};
console.log(concert);
console.log(JSON.stringify(concert));
const concertJSON = JSON.stringify(concert);
```

- Nous pouvons également transformer une string JSON en un objet JS avec la méthode JSON.parse().
  
```json
const dogJSON = '{"name":"Rocko", "age":3}';
console.log(JSON.parse(dogJSON));
const dog = JSON.parse(dogJSON);
console.log(dog.name);
const dogNAME = dog.name;
```

- Comme pour les propriété, nous pouvons regrouper les fonctions associées dans des objets.
- Les fonctions à l'intérieur d'un objet sont appelées les méthodes de l'objet.
  
```js
const dog1 = {
  name: "Bo",
};
function bark() {
  console.log("woof woof");
}
bark();
```

- Nous créeons des méthodes d'objet comme les propriétés, en commançant par un nom et deux-points ":", suivis du mot-clé function, "()", et des accolades "{}".
  
```json
const dogMaster = {
  name: "Bo",
  bark: function () {
    console.log("woof woof");
  },
};
dogMaster.bark();
```

- Les méthodes sont similaires aux fonctions régulières. Cela signifie que nous pouvons également inclure des paramètres et des instructions de return.
  
```json
const dogSuperMaster = {
  name: "Bo",
  bark: function (word) {
    return "woof woof, " + word;
  },
};
console.log(dogSuperMaster.bark("hungry"));
const myDog = dogSuperMaster.bark("hungry");
console.log(myDog);
```

- Exemple 1 : Assemblez le code pour créer la méthode de l'objet

```json
const phone = {
  brand: "Apple",
  number: "555-555-5555",
  ring: function () { },
};
```

- Exemple 2 : l'objet exécute la méthode meow
  
```json
const cat1 = {
  name: "Kittens",
  meow: function () {
    console.log("meow");
  },
};
cat1.meow();
```

- Exemple 3 : utiliser les méthodes pour accéder et mettre à jour les propriétés de notre objet

```json
let myCereal = {
  name: "Trix",
  display: function () {
    console.log("Trix");
  },
};
myCereal.display();
```

- Le mot clé "this" fait référence à l'objet qui contient la méthode. Dans ce cas, myCereal.

- Nous pouvons utiliser "this" suivi d'un "." pour obtenir les propriétés de l'objet à partir de ses méthodes.

```json
const myCereal1 = {
  name: "Trix",
  display: function () {
    console.log(this.name);
  },
};
myCereal1.display();
```

- De même, nous pouvons utiliser "this" suivi d'un "." pour mettre à jour les propriétés de l'objet depuis ses méthodes.

- Le mot-clé "this" ne peut être utilisé que pour accéder aux propriétés d'un objet à l'intérieur de la méthode de l'objet.

```js
const myCereal2 = {
  name: "Trix",
  changeAndDisplay: function () {
    this.name = "Cap'n Crunch";
    console.log(this.name);
  },
};
myCereal2.changeAndDisplay();
```


