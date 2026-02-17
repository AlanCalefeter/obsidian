
# RÈGLES DE CODAGE (projet) 

# 1 - Nommage 

Par défaut, c’est la notation Camel case qui est utilisée. 

## 1. Les classes et structures

- Le nom des classes et des structures commencent par une majuscule. 
- En C#, le nom des structures commence par un « S ». En effet, il est important d’identifier facilement une structure. En particulier, parce que son passage en paramètre d’une méthode se fait par copie et non par référence. 
- Dans une classe, il faut bien séparer les parties :  
	- PUBLIC 
	- PRIVATE 
	- RESTRICTED

Par des lignes de commentaire : ex: 
```cs
 // *** PUBLIC ***********************************
```
## 2. Les variables 

- Le nom des constantes commencent par une majuscule. Ex : « NbDeCoupsMax » 
- Le nom des variables locales commencent par une minuscule. Ex : « nbDeCoups » 
- Le nom des variables d’instance commencent par un tiret du bas puis une minuscule. Ex : « _nbDeCoups » 
- Lorsqu’une variable a une unité, celle-ci est précisée en fin de nom de variable après un tiret du bas. Ex : « _pressionCircuit_bar » 

## 3. Les fonctions (ou méthodes de classe) 

- Le nom des fonctions commencent par une majuscule. 
# 2 - Formatage

## 1. Gestion des accolades 

Les accolades d’ouverture et de fermeture (pour des déclarations de classe, de fonction, pour des boucles, pour des conditions etc.) sont systématiques (même pour encadrer un code d’une seule ligne) & seules sur leur ligne. Ex : 

```js
if (i > 0) {
 i++ ; 
 }
```