@echo off

cd bin
IF EXIST create_project.cmd (
echo fichier exist... loading...
timeout /t 3
call create_project.cmd) ELSE (
echo fichier introuvable..)

pause