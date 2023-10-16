# Docker

### Commandes de base des container
``` bash
docker ps -a
docker run hello-world
docker run ubuntu echo Simon
docker run -ti ubuntu bash # t = terminal, i = interactif
docker kill 020b0d56b2a9
docker start -t 020b0d56b2a9 # Restart le container avec le bash
docker rm 020b0d56b2a9
docker run -ti -p7777:7777 python:2 python -m SimpleHTTPServer 7777
# -p7777:7777 = redirection du port 7777 de la carte réseau du pc vers le port 7777 de la carte réseau virtuel du container
```

### Arrière plan
``` bash
# On démare un container
docker run -p7777:7777 -d python:2 python -m SimpleHTTPServer 7777

docker run -d --name carol ubuntu tail -f  # Tourne à l'infini
docker exec -ti carol bash # Rxécucte "bash" dans "carol"
```

### Commandes de base des images
``` bash
docker image ls
docker image rm python:2.7
docker image tag ubuntu monimage:montag
```

### Les commandes network de base
``` bash 
docker network ls
network create simon # créer un réseau simon
docker network connect simon 74068ac2e9c4
docker inspect 74068ac2e9c4
docker run -ti -p7778:7777 --network simon --name simonPython python:2 python -m SimpleHTTPServer 7777
# --network simon ==> on met le container dans le réseau simon
# --name ==> on choisit le nom du container
```

### Les commandes de gestion des volumes
``` bash
docker volume create monvolume
docker volume ls
docker run -ti --name alice --volume monvolume:/tmp/projet ubuntu bash
```

# Docker file
``` bash
FROM ubuntu

RUN apt-get update
RUN apt-get install -y iputils-ping vim net-tools dstat
COPY monfichierDeConf /etc/fichier.conf
ENTRYPOINT ["/bin/bash"]
```
Explication des mots clé :
- FROM ==> image d'origine
- RUN ==> commande à exécuter
- COPY ==> ici on met monfichierDeConf dans /etc/fichier.conf
- ENTRYPOINT ==> commande par défaut du container 
- WORKDIR ==> l'endroit ou le docker démarre par défaut c'est dans /
- EXPOSE ==> pour dire qu'on va lancer un service sur le port 7777 (c'est plus de la doc mais faut le faire)

### Utilisation d'un dockerfile
``` bash
docker build -t ubuntuperso -f file.Dockerfile . # Crée l'image ubuntuperso
docker run -ti ubuntuperso
```

### Upload une image en ligne
``` bash
docker login
docker tag simplhttp zarbose/simplhttp
docker push zarbose/simplhttp
```
 
# Docker compose
Un exemple : 
``` yml
version: "3.9"
services:
  python:
    build:
      context: ./
      dockerfile: python.Dockerfile
    image: zarbose/ec2-python
    container_name: python
    env_file:
      - secrets/.env_python
    ports:
      - "8000:8000"
    networks:
      - python
    depends_on:
      - influxdb
    volumes:
      - ./webapp/Ec2/db.sqlite3:/app/webapp/Ec2/db.sqlite3
influxdb:
    build:
      context: ./
      dockerfile: influxdb.Dockerfile
    image: zarbose/ec2-influxdb
    container_name: influxdb
    env_file:
      - secrets/.env_influxdb
    ports:
      - "8086:8086"
    networks:
      - python
      - grafana

  grafana:
    build:
      context: ./
      dockerfile: grafana.Dockerfile
    image: zarbose/ec2-grafana
    container_name: grafana
    env_file:
      - secrets/.env_gf
    ports:
      - "3000:3000"
    networks:
      - grafana
    depends_on:
      - influxdb

networks:
  python:
  grafana:
```
Lancement compose
``` bash
docker-compose up -d
```
