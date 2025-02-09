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

# Exercice 2 - Linux

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

On doit installé le pip :

 ` sudo apt install pip`
 
Vérifier si pip est bien installé et la version :

  `pip --version` 
  
Installer flask :

  ` pip install flask`
  
Vérifier si flask est bien installé :

   `flask --version`
   
# Exercice 3 - Storage

1- Rechercher le disque supplémentaire de 1Gb connecté à la VM:

Utiliser la commande suivante pour lister les disques et les partitions connectés au système :

`sudo fdisk -l`
   
Pour trouver directement le disque supplémentaire de 1Gb connecté à la VM utiliser la commande suivante:

   `sudo fdisk -l | grep "1 GiB"`
   
2- Formater le disque au format ext4

Vérifier que le disque ne figure pas dans la liste des systèmes de fichiers montés, avec leur point de montage correspondant:

   `df -h`
   
 formater le disque au format ext4:

  `sudo mkfs -t ext4 /dev/vdc`
  
3- Monter (mount) ce disque sur le point montage /home/ubuntu/tp-coaching-webforce3/log :

Créez le répertoire de point de montage avec la commande suivante :

  `sudo mkdir log`
  
Montez le disque sur le point de montage en utilisant la commande suivante :

  `sudo mount /dev/vdc /home/ubuntu/tp-coaching-webforce3/log`
  
# Exercice 4 - Git/Github

1- Dans PyCharm allez dans File->Settings->Version control->github

2- Appuyer sur la croix, en haut a gauche de cette fenetre et selectionnez log in with token.

3- Entrez votre token github

4- Vous pouvez maintenant faire des git commit et git push depuis PyCharm

# Exercice 5 - Python

Créez un fichier blogs.py

 `nano blogs.py`
 
le commenter:

```python
from flask import Flask
import logging
 # create the app
 # app est une application Flask
app = Flask(__name__)
 #effecture la configuration de base du système du journalisation dans la fiche "log/record.log" 
logging.basicConfig(filename='log/record.log', level=logging.DEBUG, format=f'%(asctime)s %(levelname)s %(name)s %(threadName)s : %(message)s')
 # application route, décorateur pour lier une fonction à une URL
@app.route('/blogs')
#creation de la fonction avec le nom blog qui retourne " Welcom to the Blog"
def blog():
    app.logger.info('Info level log')
    app.logger.warning('Warning level log')
    return f"Welcome to the Blog"
 #l'exectuion de l'application en localhost
app.run(host='localhost', debug=True)
```
Ajouter une variable d'environnement FLASK_APP=blogs n utilisant la commande suivante :

`export FLASK_APP=blogs.py`

mettre cette variable dans le fichier ~/.bashrc de votre user ubuntu:

` nano ~/.bashrc`

Pour prendre en compte le changement fais sur le fichier :

`source ~/.bashrc`

Lancer le web server avec la commande :

` flask run --host=0.0.0.0 -p 30101`

Rajouter une condition manquante pour pouvoir lancer le web server:

`if __name__ == '__main__'`

Vérifier avec votre navigateur en utilisant l'url http://<ip_de_votre_vm>:30101/blogs:

![image](https://user-images.githubusercontent.com/122799110/221377787-9ad82367-f049-46be-9dbe-0cd518edac6c.png)

# Exercice 6 - Pare-feu

Trouvez la commande de gestion du firewall sous ubuntu 20.04:
`sudo ufw [option]`

fermer le port 5000 en utilisant le commande:

`sudo ufw deny 5000 `

autoriser le port 30101:

`sudo ufw allow 30101`
Vérifier l'application Web sur ces ports par la commande:
`netsate | grep "30101"`

# TP Ansible
Mettre en place ansible dans votre VM, si ce n'est pas deja fait Nous allons créer un virtualenv python pour installer la derniere version d'Ansible
`cd ~/tp-coaching-webforce3`

`python3 -m venv venv  # set up the module venv in the directory venv

`source venv/bin/activate`  # activate the virtualenv python

`pip3 install wheel`  # set for permissions purpose

`pip3 install --upgrade pip` # update pip3

`pip3 install ansible` # install ansible 

`pip3 install requests` # extra packages

`pip3 install natsort `# require for an ansible filter

`ansible --version `# check the version number`

# TP ansible 1
Créer un fichier ansible-1.yaml qui automatise l'exercice 2 ci-dessus.

1-Le script doit mettre à jour les packages ubuntu.
2-Vérifier la version de python3
3-Créer un alias dans ~/.bashrc
4-installer le package pip Testez votre script, il doit etre idempotent
```
---
- name: Playbook exercice 1 ansible
  hosts: localhost
  become: true
  tasks:
   - name: Mise à jour les packages ubuntu
     ansible.builtin.apt:
             #name: update
      update_cache: yes
      upgrade: dist

   - name: vérifier la version de python3
     ansible.builtin.command:
      cmd: python3 --version

   - name: Créer un alias
     ansible.builtin.lineinfile:
      dest: ~/.bashrc
      line: 'alias python="python3"'
```





