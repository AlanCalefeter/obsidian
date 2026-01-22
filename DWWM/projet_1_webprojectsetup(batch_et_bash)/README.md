# Web_Project_Setup

TP Mini-Projet : Création d'une structure ou skeleton d’un projet web

---

## Sommaire :
- [[#À propos]]
- [[#Fonctionnalités]]
- [[#Structure du projet]]
- [[#Prérequis]]
- [[#Installation]]
- [[#Utilisation]]
- [[#Technologies utilisées]]
- [[#Captures d’écran]]
- [[#Auteurs]]
- [[#Licence]]

---
## À propos
Ce projet a était crée pour générer une structure de base ou skeleton pour un site web statique en utilisant des scripts batch (.cmd) et bash (.sh). 
La création d'une structure de projet est une étape fondamentale dans le développement web, permettant de préparer le terrain pour l'ajout de contenu et de fonctionnalités ultérieures. 

---
## Fonctionnalités
- Création automatique d’arborescence de projet  
- Génération des fichiers HTML, SCSS et JS de base  
- Compatible Laragon / Git Bash  
- Structure modulaire et extensible
---
### Structure du projet

```
mon-site-exemple
├─ .browserslistrc                         
├─ .well-known                             
│  └─ security.txt                         
├─ 403.html                                
├─ 404.html                                
├─ LICENSE                                 
├─ README.md                               
├─ assets                                  
│  ├─ css                                  
│  │  ├─ style.css                         
│  │  └─ style.css.map                     
│  ├─ fonts                                
│  │  ├─ NotoSans-VariableFont.woff2      
│  │  ├─ OFL.txt                           
│  │  └─ README.txt                        
│  └─ js                                   
│     └─ app.js                            
├─ favicon.png
├─ img                                     
│  ├─ icons                                
│  │  ├─ android-icon-144x144.png
│  │  ├─ android-icon-192x192.png
│  │  ├─ android-icon-36x36.png
│  │  ├─ android-icon-48x48.png
│  │  ├─ android-icon-72x72.png
│  │  ├─ android-icon-96x96.png
│  │  ├─ apple-icon-114x114.png
│  │  ├─ apple-icon-120x120.png
│  │  ├─ apple-icon-144x144.png
│  │  ├─ apple-icon-152x152.png
│  │  ├─ apple-icon-180x180.png
│  │  ├─ apple-icon-57x57.png
│  │  ├─ apple-icon-60x60.png
│  │  ├─ apple-icon-72x72.png
│  │  ├─ apple-icon-76x76.png
│  │  ├─ apple-icon-precomposed.png
│  │  ├─ apple-icon.png
│  │  ├─ favicon-16x16.png
│  │  ├─ favicon-32x32.png
│  │  ├─ favicon-96x96.png
│  │  ├─ favicon.png
│  │  ├─ ms-icon-144x144.png
│  │  ├─ ms-icon-150x150.png
│  │  ├─ ms-icon-310x310.png
│  │  └─ ms-icon-70x70.png
│  ├─ logo-110x110.webp
│  ├─ logo-160x160.webp
│  ├─ logo-200x200.webp
│  ├─ logo-800x800.webp
│  └─ logo-96x96.webp
├─ index.html                              
├─ package-lock.json                       
├─ package.json                            
├─ pages                                   
│  ├─ about.html                           
│  ├─ article-details.html                 
│  ├─ blog.html                            
│  ├─ contact.html                         
│  ├─ cookies-policy.html                  
│  ├─ faq.html                             
│  ├─ legal-notice.html                    
│  ├─ portfolio.html                       
│  ├─ privacy-policy.html                  
│  ├─ project-details.html                 
│  ├─ search-results.html                  
│  ├─ service-details.html                 
│  ├─ services.html                        
|  ├─ team.html                            
│  ├─ terms-conditions.html                
│  └─ testimonials.html                    
├─ robots.txt                          
├─ scss                                    
│  ├─ abstracts                          
│  │  ├─ _functions.scss                   
│  │  ├─ _index.scss                       
│  │  ├─ _mixins.scss                      
│  │  └─ _variables.scss                   
│  ├─ base                                 
│  │  ├─ _fonts.scss                       
│  │  ├─ _global.scss                      
│  │  ├─ _index.scss                       
│  │  ├─ _reset.scss                       
│  │  ├─ _root.scss                        
│  │  └─ _typography.scss                  
│  ├─ components                           
│  │  ├─ _buttons.scss                     
│  │  ├─ _card.scss                        
│  │  ├─ _icons.scss                       
│  │  └─ _index.scss                       
│  ├─ layouts                              
│  │  ├─ _container.scss                   
│  │  ├─ _footer.scss                      
│  │  ├─ _header.scss                      
│  │  └─ _index.scss                       
│  ├─ pages                                
│  │  ├─ _about.scss                       
│  │  ├─ _home.scss                        
│  │  └─ _index.scss                       
│  ├─ style.scss                           
│  └─ utilities                            
│     ├─ _accessibility.scss               
│     ├─ _alignment.scss                   
│     ├─ _display.scss                     
│     ├─ _flexbox.scss                     
│     ├─ _grid.scss                        
│     ├─ _index.scss                       
│     ├─ _spacing.scss                     
│     └─ _visibility.scss                  
├─ sitemap.xml                             
├─ docs                                    
│  ├─ architecture                         
│  │  └─ overview.md                       
│  ├─ diagrams                             
│  ├─ security                             
│  ├─ workflow.md
│  └─ README.md                            
└─ .editorconfig  

```
---
## Prérequis
- [Git](https://git-scm.com/)  [[git_note]]
- [Laragon](https://laragon.org/)  
- [VS Code](https://code.visualstudio.com/)
---
## Installation
**Pour Bash**
```bash
# Cloner le dépôt
git https://github.com/anthonymorvan/Web_Project_Setup.git

# Aller dans le dossier
cd Web_Project_Setup

# (Optionnel) Donner les droits d’exécution
chmod +x setup_project.sh

# Lancer le script
bash wps.sh
```
**Pour Batch**
```cmd
# Cloner le dépôt
git https://github.com/anthonymorvan/Web_Project_Setup.git

# Aller dans le dossier
cd Web_Project_Setup

# Lancer le script
bash wps.cmd
```
---
## Utilisation
```cmd
bash wps.sh

OU

batch wps.cmd
```
Le script te demandera le nom de ton projet et créera automatiquement tous les fichiers et dossiers nécessaires.

---
## Technologies utilisées
- Bash
- Batch
- Git / GitHub
- Markdown

---
## Captures d’écran
- ## BATCH:

![image](./images/Capture-0-batch.png)
![image](./images/Capture-0-bis-batch.png)
![image](./images/Capture-1-batch.png)
![image](./images/Capture-2-batch.png)
![image](./images/Capturer-3-batch.png)

---
- ## BASH:

![image](./images/Capture-0-bash.png)
![image](./images/Capture-0-bis-bash.png)
![image](./images/Capture-1-bash.png)
![image](./images/Capture-2-bash.png)
![image](./images/Capturer-3-bash.png)

---
## Auteurs
**Anthony Morvan**

**Alan Calefeter**

---
## Licence
Ce projet est distribué sous licence MIT
[LICENSE](https://github.com/anthonymorvan/Web_Project_Setup?tab=MIT-1-ov-file)
