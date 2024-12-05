## Mettre en place un network spécifique

docker network create home

## Mettre en place un db de postgres

docker run --name <container_name> --network home -e POSTGRES_PASSWORD=<mysecretpassword> -d <image>

## Mettre en place de adminer

docker run --network home -p 8080:8080 adminer

## Mettre en place l'api

docker build -t api .
docker run --network home -p <PORT>:<PORT> -e PORT=<PORT> -v ./:/app -v /app/node_modules api


## Inspection du network
docker inspect <nom_du_network>