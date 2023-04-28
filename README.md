# 20220277

# DevOps - TP1 - Weather scrapper

<image src="https://bmu-verlag.de/wp-content/uploads/docker.jpeg" width=800 center>

[![Downloads](https://static.pepy.tech/personalized-badge/docker?period=month&units=international_system&left_color=blue&right_color=yellow&left_text=docker)](https://pepy.tech/project/docker)   [![Downloads](https://static.pepy.tech/personalized-badge/requests?period=month&units=international_system&left_color=brightgreen&right_color=orange&left_text=requests)](https://pepy.tech/project/requests) [![Downloads](https://static.pepy.tech/personalized-badge/openweather?period=month&units=international_system&left_color=blue&right_color=green&left_text=openweather)](https://pepy.tech/project/openweather)

  
> ### **Cahier des charges** : 
Ce projet vise à :
- créer un wrapper qui retourne la météo d'un lieu donné avec sa latitude et sa longitude (passées en variable d'environnement) en utilisant openweather API en utilisant pyhton (libre à vous de choisir votre language).
- Packager son code dans une image Docker
- Mettre à disposition son image sur DockerHub
- Mettre à disposition son code dans un repository Github

### **Préréquis** :
Pour réaliser ce projet, nous avons besoin de faire quelques installation de base (si ce n'est pas déjà le cas). Nous allons commencer par installer python requests pour pouvoir développer en python et faire des requêtes vers la openweather API.
> ### **1. Installation de Python, requests et docker**
```
$ sudo apt install python3-pip
$ pip install requests
$ pip install docker
```

> ### **2. Création de comptes**
Pour pouvoir utiliser l'API openweather, nous allons créer un compte sur le site https://openweathermap.org/ (vous pouvez utiliser votre compte si vous en possédez déjà). \
Pour mettre notre projet sur docker hub, il faut créer un compte sur le site de DockerHub https://hub.docker.com/ et créer un registry.

Une fois les installations de base faite et les comptes créés, nous allons pouvoir commencer le code en créant notre code de wrapper dans le fichier `weather.py`. Une fois fait, nous allons créons un fichier `Dockerfile` pour la configuration de notre image.

> ### **3. Création de l'image et test**
- `docker build . -t weather:0.0.1` : Cette commande permet de créer l'image docker sous le nom de weather avec le tag 0.0.1
- `docker run --env LAT="31.2504" --env LONG="-99.2506" --env API_KEY=****  weather:0.0.1`: cette commande vous permet d'exécuter l'image docker sur le serveur docker en passant les variables d'environnement API_KEY, LAT et LONG. L'API_KEY est à récupérer sur votre compte openweather.

> Avant d'envoyer l'image sur le serveur docker, nous allons procéder à certaines test pour voir les vulnérabilités de notre image.
> `docker run --rm -i hadolint/hadolint < Dockerfile`: cette commande permet de voir et de corriger les éventuelles erreurs et warnings dns dans le fichier de configuration Dockerfile.
> - `--no-cache-di` : permet d'effacer le cache des dossiers des bibliothèques installées. Il est donc à mettre dans chaque installation de library.
> - `requests==2.28.2` : permet de préciser la version de la bibliothèque à installer.

Si tout est OK, nous pouvons maintenant envoyer l'image sur le serveur docker.

> ### **4. Création de tag et envoe de l'image sur dockerhub**
- `docker tag weather:0.0.1 yourregistry/weather:0.0.1`: Cette commande permet de tagger l'image docker sur le serveur docker.
- `docker login -u yourregistry`: Cette commande permet de se connecter sur le serveur docker que le registry soit privé ou public cette étape est nécessaire.
- ***(ETAPE OPTIONNELLE)*** `docker pull anicetdevops/weather:0.0.1`: Cette commande permet de récupérer l'image docker sur le serveur docker.
- `docker push yourregistry/weather:0.0.1`: Cette commande permet d'envoyer l'image docker sur le serveur docker

> ### **5. Envoie du porjet sur GitHub**
```
- git add origin main
- git commit -m "message de votre commit"
- git pull origin main
- git push origin main
```
>
> Etudiant: AGBONON EDAGBDJI Yao Anicey \
> Promo: BDML 2024 \
> Email: yao-anicet.agbonon-edagbedji@efrei.net
>
