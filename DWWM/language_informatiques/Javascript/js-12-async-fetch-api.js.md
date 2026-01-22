
## 📚 Sommaire

- [[#COURS 3 : async/await & FETCH API]]
	
	- [[#1. LE PROBLÈME AVEC .then()]]
	- [[#2. INTRODUCTION À async/await]]
	- [[#3. RÉCUPÉRER UNE VALEUR AVEC await]]
	- [[#4. ENCHAÎNER DES OPÉRATIONS ASYNCHRONES]]
	- [[#5. GESTION D'ERREURS AVEC try/catch]]
	- [[#6. ATTENTION : await BLOQUE LA FONCTION]]
	- [[#7. EXÉCUTION EN PARALLÈLE AVEC Promise.all()]]
	- [[#8. FETCH API : RÉCUPÉRER DES DONNÉES D'INTERNET]]
	- [[#9. VÉRIFIER SI LA REQUÊTE A RÉUSSI]]
	- [[#10. EXEMPLE COMPLET : RÉCUPÉRER DES UTILISATEURS]]
	- [[#11. CHARGER PLUSIEURS UTILISATEURS EN PARALLÈLE]]
	- [[#12. EXEMPLE AVANCÉ : RÉCUPÉRER DES DONNÉES LIÉES]]
	- [[#13. RÉSUMÉ DU COURS 3]]


# **COURS 3 : async/await & FETCH API**

async/await : La syntaxe moderne pour l'asynchrone.  Dans les cours précédents, nous avons vu :
		- Cours 1 : setTimeout et callbacks
		- Cours 2 : Promises et .then()

async/await est la façon la PLUS MODERNE et LISIBLE. d'écrire du code asynchrone en JavaScript. C'est ce que vous utiliserez au quotidien !

# **1. LE PROBLÈME AVEC .then()**

Les .then() sont mieux que les callback, mais peuvent devenir long.

```js
// Avec .then() (verbeux)

const getUserDataThen = (userId) => {
  fetchUser(userId)
    .then((user) => {
      console.log("Nom :", user.nom);
      return fetchOrders(userId);
    })

    .then((orders) => {
      console.log("Commandes :", orders);
      return fetchDetails(orders[0]);
    })

    .then((details) => {
      console.log("Détails :", details);
    })

    .catch((error) => {
      console.log("Erreur :", error);
    });
};
```
- C'est lisible, mais on peut faire MIEUX avec async/await !


# **2. INTRODUCTION À async/await**

- async/await permet d'écrire du code asynchrone qui RESSEMBLE à su code synchrone. Règles :
		1 . On met 'async' devant une fonction
		2 . On utilise 'await' devant une Promise
		3 . await met le code en pause jusqu'à ce que la Promise soit résolue 

```js
// Fonction d'attente pour les exemples

const attendre = (ms) => {
  return new Promise((resolve) => setTimeout(resolve, ms));
};
```

```js
// Version avec .then()

const exemple1Then = () => {
  attendre(1000).then(() => {
    console.log("Terminé !");
  });
};
```

```js
// Version avec async/await (plus lisible)

const exemple1Async = async () => {
  await attendre(1000);
  console.log("Terminé !");
};
```

- 💡 await "met en pause" la fonction jusqu'à ce que la Promise soit résolue. Pendant ce temps, le reste du programme continue !

# **3. RÉCUPÉRER UNE VALEUR AVEC await**

- await permet de récupérer directement la valeur d'une Promise.

```js
const getMessage = () => {
  return new Promise((resolve) => {
    setTimeout(() => {
      resolve("Hello World");
    }, 1000);
  });
};
```

```js
// Avec .then()

getMessage().then((message) => {
  console.log(message); // "Hello World"
});
```

```js
// Avec async/await (plus simple)

const afficherMessage = async () => {
  const message = await getMessage();
  console.log(message); // "Hello World"
};

afficherMessage()
```

- await transforme Promise → valeur directement !

# **4. ENCHAÎNER DES OPÉRATIONS ASYNCHRONES**

-  Avec async/await, le code asynchrone ressemble à du code synchrone.

```js
const etape1 = () => {
  return new Promise((resolve) => {
    setTimeout(() => resolve("Étape 1 terminée"), 1000);
  });
};
  
const etape2 = () => {
  return new Promise((resolve) => {
    setTimeout(() => resolve("Étape 2 terminée"), 1000);
  });
};
  
const etape3 = () => {
  return new Promise((resolve) => {
    setTimeout(() => resolve("Étape 3 terminée"), 1000);
  });
};
```

```js
// Avec .then() (moins lisible)

const executerThen = () => {
  etape1()
    .then((result1) => {
      console.log(result1);
      return etape2();
    })

    .then((result2) => {
      console.log(result2);
      return etape3();
    })

    .then((result3) => {
      console.log(result3);
    });
};
```

```js
// Avec async/await (beaucoup plus clair !)

const executerAsync = async () => {
  const result1 = await etape1();
  console.log(result1);

  const result2 = await etape2();
  console.log(result2);

  
  const result3 = await etape3();
  console.log(result3);
};
 
executerAsync();
```

- C'est comme du code synchrone, mais c'est asynchrone !

# **5. GESTION D'ERREURS AVEC try/catch**

- Avec async/await, on gère les erreurs avec try/catch (comme en code synchrone).

```js
const operationRisquee = (reussit) => {
  return new Promise((resolve, reject) => {
    setTimeout(() => {

      if (reussit) {
        resolve("Succès !");
      } else {
        reject("Échec !");
      }
    }, 1000);
  });
};
```

```js 
// Avec .then()/.catch()

operationRisquee(false)
  .then((result) => console.log(result))
  .catch((error) => console.log("Erreur :", error));
```

```js
// Avec async/await + try/catch (plus naturel)

const testerOperation = async () => {
  try {
  
    const result = await operationRisquee(false);
    console.log(result);
    
  } catch (error) {
  
    console.log("Erreur attrapée :", error); // "Erreur attrapée : Échec !"
  }
};

testerOperation();
```

- try/catch fonctionne exactement comme avec du code synchrone !

# **6. ⚠️ ATTENTION : await BLOQUE LA FONCTION**

- await met en pause la FONCTION, pas tout le programme. 

```js
const tacheLongue = async () => {
  console.log("Début de la tâche longue");
  await attendre(3000); // Attend 3 secondes
  console.log("Tâche longue terminée");
};

console.log("Avant");

tacheLongue(); // ⚠️ Ne bloque pas, retourne immédiatement une Promise

console.log("Après"); // S'affiche IMMÉDIATEMENT
```

```js
// Résultat :

// Avant

// Début de la tâche longue

// Après

// Tâche longue terminée  ← Après 3 secondes
```

- Le reste du programme continue pendant que la fonction attend !

#  **7. EXÉCUTION EN PARALLÈLE AVEC Promise.all()**

- ⚠️ PIÈGE COURANT : await exécute les Promises l'une après l'autre !

```js
// ❌ MAUVAIS : Exécution séquentielle (lent)

const chargerDonneesLent = async () => {
  console.time("Lent");

  const users = await attendre(2000).then(() => ["Alice", "Bob"]);

  const posts = await attendre(2000).then(() => ["Post1", "Post2"]);

  console.timeEnd("Lent"); // ~4000ms (2s + 2s)
};
```

```js
// ✅ BON : Exécution parallèle (rapide)

const chargerDonneesRapide = async () => {
  console.time("Rapide");

  
  // On lance les deux Promises en même temps

  const [users, posts] = await Promise.all([
    attendre(2000).then(() => ["Alice", "Bob"]),
    attendre(2000).then(() => ["Post1", "Post2"]),
  ]);

  console.timeEnd("Rapide"); // ~2000ms (en parallèle !)
};

chargerDonneesLent();

chargerDonneesRapide();
```

- 💡 Règle : Utilisez Promise.all() quand les opérations sont INDÉPENDANTES !


# **8. FETCH API : RÉCUPÉRER DES DONNÉES D'INTERNET**

- fetch() est LA méthode moderne pour faire des requêtes HTTP. fetch() retourne une Promise !

```js
// Exemple simple

const getJoke = async () => {
  const response = await fetch("https://api.chucknorris.io/jokes/random");
  const data = await response.json(); // .json() retourne aussi une Promise !
  console.log(data.value);
};

getJoke();
```

-  ⚠️ fetch() retourne une Response, pas directement les données ! Il faut appeler .json() pour convertir la réponse en objet JavaScript.

# **9. VÉRIFIER SI LA REQUÊTE A RÉUSSI**

- fetch() ne rejette PAS en cas d'erreur HTTP (404, 500, etc.). Il faut vérifier response.ok !

```js
const fetchWithCheck = async (url) => {

  try {
    const response = await fetch(url);

    // Vérifier le statut HTTP
    if (!response.ok) {
      throw new Error(`Erreur HTTP ${response.status}: ${response.statusText}`);
    }

    const data = await response.json();
    return data;
    
  } catch (error) {
  
    console.log("Erreur :", error.message);

    throw error; // On relance l'erreur pour que l'appelant puisse la gérer
  }
};
```

```js

// Test avec une URL valide

fetchWithCheck("https://api.chucknorris.io/jokes/random")

  .then((data) => console.log("Blague :", data.value))

  .catch((error) => console.log("Impossible de charger la blague"));
```

```js
// Test avec une URL invalide

fetchWithCheck("https://api.chucknorris.io/inexistant")

  .then((data) => console.log(data))

  .catch((error) => console.log("Erreur attrapée :", error.message));
```

- Toujours vérifier response.ok avant de lire les données !


# **10. EXEMPLE COMPLET : RÉCUPÉRER DES UTILISATEURS**

- API publique : JSONPlaceholder (données de test)

```js
const getUser = async (userId) => {

  try {

    const response = await fetch(

      `https://jsonplaceholder.typicode.com/users/${userId}`
    );

    if (!response.ok) {

      throw new Error(`Utilisateur ${userId} introuvable`);

    }
    const user = await response.json();

    return user;

  } catch (error) {

    console.log("Erreur :", error.message);

    return null;
  }
};
```

```js
// Utilisation

const afficherUtilisateur = async () => {

  const user = await getUser(1);

  if (user) {

    console.log(`Nom : ${user.name}`);

    console.log(`Email : ${user.email}`);

    console.log(`Ville : ${user.address.city}`);
  }
};
 
afficherUtilisateur();
```

#  **11. CHARGER PLUSIEURS UTILISATEURS EN PARALLÈLE**

```js
const afficherPlusieursUtilisateurs = async () => {

  try {

    console.time("Chargement");

    // Charger 3 utilisateurs en parallèle

    const [user1, user2, user3] = await Promise.all([

      getUser(1),

      getUser(2),

      getUser(3),

    ]);

    console.timeEnd("Chargement");
  
    console.log("Utilisateurs :", [user1.name, user2.name, user3.name]);

  } catch (error) {

    console.log("Erreur lors du chargement :", error);
  }
};  

afficherPlusieursUtilisateurs();
```

- Beaucoup plus rapide qu'un chargement séquentiel !


# **12. EXEMPLE AVANCÉ : RÉCUPÉRER DES DONNÉES LIÉES**

- Récupérer un utilisateur, puis ses posts.

```js
const getUserWithPosts = async (userId) => {

  try {

    // 1. Récupérer l'utilisateur

    const user = await getUser(userId);

    console.log(`Utilisateur : ${user.name}`);
    
   
     // 2. Récupérer ses posts

    const response = await fetch(

      `https://jsonplaceholder.typicode.com/posts?userId=${userId}`
    );

    const posts = await response.json();
  
    console.log(`Nombre de posts : ${posts.length}`);

    console.log("Premier post :", posts[0].title);

    return { user, posts };

  } catch (error) {

    console.log("Erreur :", error.message);
  }
};

getUserWithPosts(1);
```

- Ici, on doit charger séquentiellement car les posts dépendent de l'utilisateur.


# **13. RÉSUMÉ DU COURS 3**


 ## Ce que vous avez appris :
 
 * ✅ async/await : la syntaxe moderne pour l'asynchrone

 * ✅ await transforme Promise → valeur

 * ✅ Gestion d'erreurs avec try/catch

 * ✅ Exécution séquentielle vs parallèle

 * ✅ Promise.all() avec async/await

 * ✅ fetch() : récupérer des données d'Internet

 * ✅ Vérifier response.ok

 * ✅ .json() pour convertir la réponse

 * ✅ Charger des données liées (séquentiel)

 * ✅ Charger des données indépendantes (parallèle)

 * Vous maîtrisez maintenant l'asynchrone en JavaScript moderne ! 🎉