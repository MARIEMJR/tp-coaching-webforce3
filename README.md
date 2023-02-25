# tp-coaching-webforce3
Instruction pour la session de coaching
Mini-projet : Installer sur une VM (fournie), un serveur Web en Python Flask fonctionnant sur le port 30101. Ce serveur écrit les actions des utilisateurs dans un disque attaché à la VM. écrire les instructions pour le pare-feu
# Exercice 1 - Scrum
1- Aller sur project

2- Ensuite sur New Project

3- Sélectionner un modèle puis cliquer sur créer

4- Créer la liste des tâches à effectuer

5- Faire un screenshot
![image](https://user-images.githubusercontent.com/122799110/221375751-668a22c8-63ab-45d6-a0cb-36580aaf6208.png)

#Exercice 2 - Linux
1-Mettre à jour les packages de votre VM ubuntu:
``
sudo apt-get update
sudo apt-get upgrade
``

2-Vérifier la version de python3 déjà installée:
`python3 --version : Python 3.8.10 `

3-créer un alias nommé python valide pour le user ubuntu de votre VM:
  -Ouvrir le fichier .bashrc du user ubuntu:
  `sudo nano ~/.bashrc`
  Ajouter la ligne suivante au fichier :

   `alias python='python3`

Rechargez les modifications faites dans le fichier ~/.bashrc en tapant la commande suivante :

   `source ~/.bashrc`
   
La commande "python" peut être utilisée pour exécuter le programme "python3" sur la VM.

Pour vérifier,utiliser :

   `python -V`
4- Installer flask:

Si pip n'est pas installé, faire la commande suivante :

 ` sudo apt install pip`
Vérifier si pip est bien installé et la version :

  `pip --version` 
Installer flask :

  ` pip install flask`
Vérifier si flask est bien installé et la version :

   `flask --version`
#Exercice 3 - Storage
1- Rechercher le disque supplémentaire de 1Gb connecté à la VM:

Utiliser la commande suivante pour lister les disques et les partitions connectés au système, avec des informations telles que le nom du périphérique, le type de périphérique, la taille du périphérique, etc:
`sudo fdisk -l`
   
Pour trouver directement le disque supplémentaire de 1Gb connecté à la VM utiliser la commande suivante:

   `sudo fdisk -l | grep "1 GiB"`
2- Formater le disque au format ext4

Vérifier que le disque ne figure pas dans la liste des systèmes de fichiers montés, avec leur point de montage correspondant:

   `mount`
 formater le disque au format ext4:

  `sudo mkfs -t ext4 /dev/vdc`
3- Monter (mount) ce disque sur le point montage /home/ubuntu/tp-coaching-webforce3/log :

Créez le répertoire de point de montage avec la commande suivante :

  sudo mkdir -p /home/ubuntu/tp-coaching-webforce3/log
Montez le disque sur le point de montage en utilisant la commande suivante :

  `sudo mount /dev/vdc /home/ubuntu/tp-coaching-webforce3/log`
#Exercice 4 - Git/Github
1- Dans PyCharm allez dans File->Settings->Version control->github

2- Appuyer sur la croix, en haut a gauche de cette fenetre et selectionnez log in with token.

3- Entrez votre token github

4- Vous pouvez maintenant faire des git commit et git push depuis PyCharm

#Exercice 5 - Python
Créez un fichier blogs.py

 `nano blogs.py`
le commenter:


