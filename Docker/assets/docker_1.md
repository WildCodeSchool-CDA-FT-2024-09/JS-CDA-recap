## Coté API

Mettre en place le docker file
docker build -t <container_name> .
docker run <container_name>
Si ok, ajout de l'option -d pour detach

Mettre en place les commandes :
docker ps
docker ps -a
docker system prune
docker stop <ID>
docker logs --follow <ID> (-tf)

## Publish to docker Hub

Follow the doc to create an account https://docs.docker.com/docker-hub/quickstart/
docker push <nomdudockerhub>/<nomimage>
:warning reprendre le build pour incorporer le nom du dockerhub dans l'image

## Mettre en place la config de dev

- Problème d'acces
  docker run -p 4000:4000 <container_name>

- problème de hot refresh
  docker run -p 4000:4000 -v $(PWD):/app -v /app/node_modules <container_name>

## Coté client

Mettre en place le docker file

docker build -t <container_name> .
docker run -v $(PWD):/app -v /app/node_modules -p <port>:<port> <container_name>

flag : -it -d
ou docker exec -it 1032d9c3f890 sh

Mettre en place la config vite
`vite.config.ts`

import { defineConfig } from 'vite';

export default defineConfig({
server: {
host: '0.0.0.0', // Permet à Vite d'écouter sur toutes les interfaces
port: 5173, // Le port que vous exposez dans Docker
},
});

- Problème: passage de variable d'environnement
  -e VITE_API_URL=http://localhost:4000

  docker run -it -v $(PWD):/app -v /app/node_modules -p 5173:5173 -e VITE_API_URL=http://localhost:4000 julienrichardwcs/bacasable_client

## Watch the target

docker stats <container_name>
