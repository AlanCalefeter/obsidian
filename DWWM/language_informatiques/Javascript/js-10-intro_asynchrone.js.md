# Sommaire : 

- [[#introductions aux asynchrones]]
- [[#**1. Code Synchrone(NORMAL)**]]
- [[#**2. Problème du code Synchrone **]]
- [[#**3. Solution setTimeout( )**]]
- [[#**4. Visualisation de l'Ordre d'Execution**]]
- [[#**5. PLUSIEURS setTimeout**]]
- [[#**6. LES CALLBACKS**]]
- [[#**7. CALLBACKS ASYNCHRONES**]]
- [[#**8. PROBLÈME CALLBACK HELL**]]
- [[#**9. Exemple Pratique MINUTEUR**]]
- [[#**10. RÉSUMÉ DU COURS 1**]]
# **Introductions aux asynchrones**


- JavaScript exécute normalement le code ligne par ligne *(synchrone).*
  
- Mais certaines opérations prennent du temps :Charger des données depuis Internet, Attendre un clic de l'utilisateur, Lire un gros fichier

- L'asynchrone permet de ne PAS bloquer le programme pendant ces opérations.

---
## **1. Code Synchrone(NORMAL)**

- En mode synchrone, chaque ligne attend que la précédente soit terminée.
```js
console.log("Étape 1");
console.log("Étape 2");
console.log("Étape 3");
```

---
## **2. Problème du code Synchrone **

- Une opération longue bloque *TOUT* le reste du code.
```js
const countToMillion = () => {
  console.log("Début du comptage...");
  for (let i = 0; i < 1000000000; i++) {
    // Compte jusqu'à 1 milliard (prend plusieurs secondes)
  }
  console.log("Comptage terminé !");
};

console.log("Avant le comptage");
countToMillion(); // ⚠️ Bloque tout pendant plusieurs secondes !
console.log("Après le comptage");
```

- **PROBLEME** : Pendant le comptage, RIEN ne peut se passer !
	  -  la page est gelée ,
	  - l'utilisateur ne peut pas cliquer ,
	  - aucun autre code ne s'exécute.

---
## **3. Solution : setTimeout( )**

- *setTimeout()* exécute du code plus tard,* sans bloquer* le rest du programme.
- **SYNTAXE** : setTimeout(fonction, délaiEnMilisecondes)

```js
console.log("Je commence");
setTimeout(() => {
  console.log("J'apparais après 2 secondes");
}, 2000);

console.log("Je termine");
```

**Résultat :**
- Je commence
- Je termine
- J'apparais après 2 secondes  ← Apparaît 2 secondes plus tard

```
 💡 Observation importante :
 
 "Je termine" s'affiche AVANT le message du setTimeout !
 C'est ça, l'asynchrone : le code continue pendant que setTimeout attend.

```

---
## **4. Visualisation de l'Ordre d'Execution**

```js
console.log("1. Début");
setTimeout(() => {
  console.log("2. Après 0 seconde");
}, 0); // ⚠️ Même avec 0ms, c'est asynchrone !
console.log("3. Fin");
```

**Résultat :**
 -  1. Début
 -  3. Fin
 -  2. Après 0 seconde  ← S'affiche en dernier même avec 0ms !
   
   Pourquoi ? JavaScript a une "file d'attente" :
 * 1. Il exécute tout le code synchrone d'abord
 * 2. Puis il exécute les fonctions asynchrones

---
## **5. PLUSIEURS setTimeout**

- On peut avoir plusieurs *setTimeout* avec des délais différents.

```js
console.log("Départ !");

setTimeout(() => {
  console.log("3 secondes");
}, 3000);

setTimeout(() => {
  console.log("1 seconde");
}, 1000);

setTimeout(() => {
  console.log("2 secondes");
}, 2000);

console.log("Go !");
```

**Résultat :**
- Départ !
- Go !
- 1 seconde
- 2 secondes
- 3 secondes

- Les *setTimeout* s'exécutent dans l'ordre de leur délai, pas dans l'ordre du code !

---
## **6. LES CALLBACKS**

- *Callback*: fonction passée en paramètre à une autre fonction. *setTimeout* utilise un callback !

```js
//Exemple simple de callback

const direBonjour = (nom, callback) => {
  console.log(`Bonjour ${nom}`);
  callback(); // On exécute la fonction passée en paramètre
};

direBonjour("Alice", () => {
  console.log("Callback exécuté !");
});
```

**Résultat :**
- Bonjour Alice
- Callback exécuté ! 

---
## **7. CALLBACKS ASYNCHRONES**

- Les *callbacks* sont souvent utilisés avec des opérations *asynchrones*.

```js
const loadData = (callback) => {

  console.log("Chargement des données...");
  setTimeout(() => {
    const data = { nom: "Alice", age: 25 };
    callback(data); // On passe les données au callback
  }, 2000);
  
};
  
loadData((data) => {
  console.log("Données reçues :", data);
});

console.log("La suite du programme continue...");
```

**Résultat :**
- Chargement des données...
-  La suite du programme continue...
- Données reçues : { nom: 'Alice', age: 25 }  ← Après 2 secondes

---
## **8. PROBLÈME : CALLBACK HELL**

- Quand on enchaîne trop de callbacks, le code devient illisible. C'est ce qu'on appelle le "*Callback Hell*" ou *"Pyramid of Doom"*.

```js
setTimeout(() => {
  console.log("Étape 1");
  
  setTimeout(() => {
    console.log("Étape 2");
    
    setTimeout(() => {
      console.log("Étape 3");
      
      setTimeout(() => {

        console.log("Étape 4");

        // 😱 Code illisible !

      }, 1000);

    }, 1000);

  }, 1000);

}, 1000);
```

- **Solution** : Les *Promises* et *async/await* (prochains cours)

---
## **9. Exemple Pratique : MINUTEUR**

- Créons un compte à rebours simple.

```js
const countdown = (seconds) => {
  console.log(`Départ : ${seconds} secondes`);

  const timer = setInterval(() => {
    seconds--;
    console.log(seconds);

    if (seconds === 0) {
      clearInterval(timer); // Arrête le timer
      console.log("Terminé !");
    }
  }, 1000);
};
countdown(5)
```

- *setInterval()* est comme *setTimeout()*, mais répète l'action.
- *clearInterval()* permet de l'arrêter.

---
## **10. RÉSUMÉ DU COURS 1**

 Ce que vous avez appris :
```css
 - [X] Difference entre synchrone et asynchrone
 - [X] setTimeout() pour executer du code plus tard
 - [X] setInterval() pour repeter du code
 - [X] Les callbacks (fonctions passees en parametre)
 - [X] Ordre d execution du code asynchrone
 - [X] Le probleme du Callback Hell
```

---

#javascript #cours 