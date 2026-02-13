
Script pour automatiser mon push git 
	- bien vérifier les *variables d'environnements* 
	- dans le commandeur, créer un fichier *.cmd* et lui donner le chemin du *.sh*

```bash
#!/bin/bash

# Vérifie que l'on est dans un dépôt git
if ! git rev-parse --is-inside-work-tree >/dev/null 2>&1; then
  echo "❌ Ce dossier n'est pas un dépôt Git"
  exit 1
fi

# Demande le message de commit
read -p "📝 Message du commit : " commit_message

if [ -z "$commit_message" ]; then
  echo "❌ Le message de commit ne peut pas être vide"
  exit 1
fi

# Demande la branche
read -p "🌿 Nom de la branche : " branch_name

if [ -z "$branch_name" ]; then
  echo "❌ Le nom de la branche ne peut pas être vide"
  exit 1
fi

# Commandes git
git add .

git commit -m "$commit_message"
if [ $? -ne 0 ]; then
  echo "❌ Échec du commit"
  exit 1
fi

git push origin "$branch_name"

echo "✅ Push effectué avec succès sur la branche '$branch_name'"

```