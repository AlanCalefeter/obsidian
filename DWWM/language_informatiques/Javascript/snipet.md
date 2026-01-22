# Snipet


# Sommaire

- [[#nettoyage de code]]
- [[#Vérifie si un champ est vide ou contient seulement des espaces]]
- [[#Vérifie la longueur minimale d'un texte]]
- [[##mini chronomètre (10 secondes)]]




## **nettoyage de code**

```js
export function cleanText(text) {

  if (!text) {

    console.error("cleanText(text) : test vide")

  }

  // nettoyer le texte en string avec typeof

  if (typeof text === "string") {

    console.log("Le texte est une string !")

  } else {

    console.log("Le texte n'est pas une string");

  }

  // remplacement de caractere dangereux avec forEach , replace() et RegExp

  const tableauCaratere = [`<`, `>`, `"`, `'`];

  console.log("Le premier elements du tableau est : " + tableauCaratere[0]);

  tableauCaratere.forEach(elementTableau => {

    const regexText = new RegExp(`[${elementTableau}]`, "g");

    text = text.replace(regexText, "_");

  });

  return text.trim();

}
```


##  **Vérifie si un champ est vide ou contient seulement des espaces**

```js
export function isEmpty(value) {

  if (!value) {
    console.error("valeur manquante !")
  }

  // Verifie si value existe et si il est vide

  console.log("Test isEmpty:", value);

  const result = !value || value.trim() === '' || value.length === 0;

  console.log("Résultat:", !result);

  return result;

}
```

## **Vérifie la longueur minimale d'un texte**

```js
export function hasMinLength(text, minLength) {

  isEmpty(text)

  const textTrimLength = text.trim().length

  const result = textTrimLength >= minLength

  return result

}
```

##  **mini chronomètre (10 secondes)** 

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

countdown (10)
```