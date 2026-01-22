# asynchrone-promises

## 📚 Sommaire

- [[#Pourquoi les Promises ?]]

	- [[#1 - QU'EST-CE QU'UNE PROMISE ?]]
	- [[#2. UTILISER UNE PROMISE AVEC .then()]]
	- [[#3. ENCHAÎNER DES .then()]]
	- [[#4. GÉRER LES ERREURS AVEC .catch()]]
	- [[#5. .finally() : TOUJOURS EXÉCUTÉ]]
	- [[#6. EXEMPLE RÉEL : SIMULER UNE API]]
	- [[#7. PROMISE.ALL() : EXÉCUTER EN PARALLÈLE]]
	- [[#8. EXEMPLE PRATIQUE : CHARGER PLUSIEURS UTILISATEURS]]
	- [[#9. COMPARAISON : SÉQUENTIEL VS PARALLÈLE]]
	- [[#10. LIEN AVEC async/await (PREVIEW)]]
	- [[#11. RÉSUMÉ DU COURS 2]]



## **Pourquoi les Promises ? **

- Dans le cours précédent, nous avons vu le *"Callback Hell"* : des callback imbriqués qui rendent le code illisible. [[js-10-intro_asynchrone.js]]

- Les Promises résolvent ce problème et sont la BASE de tout le JavaScript asynchrone moderne. 

- ⚠️ Même avec async/await, vous utilisez des Promises en coulisses !

# **1 - QU'EST-CE QU'UNE PROMISE ?**

- Une Promise (promesse) représente une valeur qui sera disponible :
	- Maintenant
	- Plus tard 
	- Jamais (en cas d'erreur)

- Une Promise a 3 états :
	- 1 - PENDING (en attente) ⏳ : L'opération est en cours
	- 2 - FULFILLED (résolue) ✅ : L'opération a réussi
	- 3 - REJECTED (rejetée) ❌ : L'opération a échoué

```js
// Exemple simple : setTimeout transformé en Promise

const attendre = (ms) => {

  return new Promise((resolve) => {
    setTimeout(() => {
      resolve("Terminé !"); // On résout la Promise
    }, ms);
  });
};

const promise = attendre(2000);

console.log(promise); // Promise { <pending> }
// Après 2 secondes, la Promise devient fulfilled
```

# **2. UTILISER UNE PROMISE AVEC .then()**

- Pour récupérer la valeur d'une Promise, on utilise .then()

```js
attendre(2000).then((resultat) => {

  console.log(resultat); // "Terminé !" après 2 secondes

});

console.log("Je continue sans attendre");

// Résultat :
// Je continue sans attendre
// Terminé !  ← Après 2 secondes
```

- .then() prend une fonction callback qui recevra la valeur quand la Promise sera résolue.

# **3. ENCHAÎNER DES .then()**

- On peut enchaîner plusieurs .then(). La valeur retournée par un .then() est passée au suivant.

```js
attendre(1000)

  .then(() => {

    console.log("Étape 1");

    return "Résultat 1";

  })

  .then((resultat) => {

    console.log("Étape 2, reçu :", resultat);

    return "Résultat 2";

  })

  .then((resultat) => {

    console.log("Étape 3, reçu :", resultat);

  });

// Résultat (après 1 seconde) :
// Étape 1
// Étape 2, reçu : Résultat 1
// Étape 3, reçu : Résultat 2
```

- Beaucoup plus lisible que [[js-10-intro_asynchrone.js]] et son callback hell

# **4. GÉRER LES ERREURS AVEC .catch()**

- Si une Promise échoue, on gère l'erreur avec .catch()

```js
const faireQuelqueChose = (reussit) => {

  return new Promise((resolve, reject) => {

    setTimeout(() => {
      if (reussit) {
        resolve("Succès !");
      } else {
        reject("Erreur !");
      }
    }, 1000);
  });
};
```

```js
// Cas de succès

faireQuelqueChose(true)
  .then((resultat) => {
    console.log(resultat); // "Succès !"
  })
  .catch((erreur) => {
    console.log("Erreur attrapée :", erreur);
  });

  
// Cas d'erreur

faireQuelqueChose(false)
  .then((resultat) => {
    console.log(resultat);
  })
  .catch((erreur) => {

    console.log("Erreur attrapée :", erreur); // "Erreur attrapée : Erreur !"
  });


//.catch() attrape TOUTES les erreurs de la chaîne de .then()
```

# **5. .finally() : TOUJOURS EXÉCUTÉ**

- .finally() s'exécute que la Promise réussisse ou échoue. Utile pour du nettoyage (fermer une connexion, masquer un loader, etc.)

```js
faireQuelqueChose(true)
  .then((resultat) => console.log(resultat))

  .catch((erreur) => console.log(erreur))

  .finally(() => {

    console.log("Opération terminée (succès ou échec)");

  });

// .finally() s'exécute dans TOUS les cas
```

# **6. EXEMPLE RÉEL : SIMULER UNE API**

- Simulons une requête vers un serveur.

```js
const fetchUser = (userId) => {

  console.log(`Chargement de l'utilisateur ${userId}...`);
  return new Promise((resolve, reject) => {
    setTimeout(() => {

      // Simuler une base de données

      const users = {

        1: { id: 1, nom: "Alice", age: 25 },
        2: { id: 2, nom: "Bob", age: 30 },
      };

      const user = users[userId];
      if (user) {
        resolve(user); // Utilisateur trouvé
      } else {
        reject(`Utilisateur ${userId} introuvable`); // Erreur
      }
    }, 1500);
  });
};
// Utilisation

fetchUser(1)

  .then((user) => {

    console.log("Utilisateur reçu :", user);
  })

  .catch((erreur) => {
    console.log("Erreur :", erreur);
  });
  
// Test avec un ID inexistant

fetchUser(999)
  .then((user) => {
    console.log("Utilisateur reçu :", user);
  })

  .catch((erreur) => {

    console.log("Erreur :", erreur); // "Erreur : Utilisateur 999 introuvable"

  });
```

# **7.  PROMISE.ALL() : EXÉCUTER EN PARALLÈLE**

- Promise.all() attend que TOUTES les Promises soient résolues. C'est TRÈS utile pour charger plusieurs données en parallèle.

```js

const task1 = attendre(1000).then(() => "Tâche 1 terminée");
const task2 = attendre(2000).then(() => "Tâche 2 terminée");
const task3 = attendre(1500).then(() => "Tâche 3 terminée");

Promise.all([task1, task2, task3]).then((resultats) => {
  console.log("Toutes les tâches terminées :");
  console.log(resultats);
  // ["Tâche 1 terminée", "Tâche 2 terminée", "Tâche 3 terminée"]
});

 * ⏱️ Temps total : 2 secondes (la plus lente)
 * Si on les avait enchaînées avec .then(), ça aurait pris 4.5 secondes !
```

# **8. EXEMPLE PRATIQUE : CHARGER PLUSIEURS UTILISATEURS**

```js
const user1 = fetchUser(1);
const user2 = fetchUser(2); 

Promise.all([user1, user2])
  .then((users) => {
    console.log("Tous les utilisateurs :", users);
  })

  .catch((erreur) => {
    console.log("Au moins un utilisateur introuvable :", erreur);
  });

 * ⚠️ Important : Si UNE SEULE Promise échoue, Promise.all() échoue !
```

# **9. COMPARAISON : SÉQUENTIEL VS PARALLÈLE**

```js

❌ SÉQUENTIEL (lent) : Attend chaque Promise l'une après l'autre
console.time("Séquentiel");
attendre(1000)

  .then(() => attendre(1000))
  .then(() => attendre(1000))
  .then(() => {
    console.timeEnd("Séquentiel"); // ~3000ms
  });


// ✅ PARALLÈLE (rapide) : Toutes les Promises en même temps

console.time("Parallèle");
Promise.all([attendre(1000), attendre(1000), attendre(1000)]).then(() => {
  console.timeEnd("Parallèle"); // ~1000ms
});

 * Promise.all() est 3x plus rapide dans cet exemple
```

# **10. LIEN AVEC async/await (PREVIEW)**

-  async/await (prochain cours) n'est que du "sucre syntaxique" pour les Promises.

```js
// Avec .then()

const getDataThen = () => {
  attendre(1000)
    .then(() => {
      console.log("Données chargées");
    })

    .catch((erreur) => {
      console.log("Erreur :", erreur);
    });
};
```

```js
// Avec async/await (plus moderne et lisible)

const getDataAsync = async () => {
  try {
    await attendre(1000);
    console.log("Données chargées");
  } catch (erreur) {
    console.log("Erreur :", erreur);
  }
};
```

- ⚠️ Une fonction async retourne TOUJOURS une Promise !

```js
const maFonction = async () => {
  return "Hello";
};
console.log(maFonction()); // Promise { 'Hello' }
  
// Pour récupérer la valeur :

maFonction().then((resultat) => console.log(resultat)); // "Hello"
```

# **11. RÉSUMÉ DU COURS 2**

## Ce que vous avez appris :
  
 * ✅ Qu'est-ce qu'une Promise (3 états : pending, fulfilled, rejected)

 * ✅ Utiliser .then() pour récupérer une valeur

 * ✅ Gérer les erreurs avec .catch()

 * ✅ .finally() pour du code qui s'exécute toujours

 * ✅ Enchaîner des .then() (éviter le Callback Hell)

 * ✅ Promise.all() pour exécuter en parallèle

 * ✅ Différence entre séquentiel et parallèle
 
 * Prochain cours : async/await pour un code encore plus lisible !
	VOIR COURS: [[js-12-async-fetch-api.js]]

