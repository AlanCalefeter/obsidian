#!/bin/bash

fichier=/c/Users/29010-34-08/Desktop/LiberKey/MyApps/laragon/www/webprojectsetup/bin/create_project.sh
cd bin

    if [ -f "$fichier" ]; then
    
echo " Le fichier exist.. Execution en cours.."
sleep 5
start $fichier

    else

echo "Le fichier n'existe pas dans ce chemin"
sleep 5

fi