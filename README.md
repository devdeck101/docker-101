# Developer Deck 101 - Docker 101 - Cheat Sheet
***
Simples referência para acompanhar os vídeos da Playlist ([Click Aqui para Assistir](https://www.youtube.com/playlist?list=PLR8OzKI52ppVkcnXQFuTZY8Yaa8ECjYgM)) do Youtube. 

## _Não se esqueça de se Inscrever, ativar as notificações e claro deixar seu LIKE e seus comentários._
---

### __Rodar containers__
A primeira coisa para trabalhar com os container é saber como executá-los:
```console
root@bdeveloperdeck101:~$ docker run ...
```
Existem vários parâmetros para passar, vou mostrar os principais.
Quando queremos remover o container logo após sair dele:
```console
root@bdeveloperdeck101:~$ docker run --rm
```
Quando queremos iteragir com o container:
```console
root@bdeveloperdeck101:~$ docker run -it
```
Quando queremos nomear o container:
```console
root@bdeveloperdeck101:~$ docker run --name developerdeck101-container
```
Quando queremos expor uma porta externamente(3000) e mapear para o porta local do container (80):
```console
root@bdeveloperdeck101:~$ docker run -p 3000:80
```
Quando queremos escolher qual imagem utilizar:
```console
root@bdeveloperdeck101:~$ docker run --name developerdeck101-container ubuntu:14.04
```
Quando queremos dizer qual é o comando que queremos executar:
```console
root@bdeveloperdeck101:~$ docker run --name developerdeck101-container ubuntu:14.04 bash
```
Juntanto tudo:
```console
root@bdeveloperdeck101:~$ docker run --rm -it -p 3000:80 --name developerdeck101-container ubuntu:14.04 bash
```
### __Listar imagens__
Quero saber as imagens locais que tenho disponível:
```console
root@bdeveloperdeck101:~$ docker images
```
Quero remover uma imagem local:
```console
root@bdeveloperdeck101:~$ docker rmi ubuntu:14.04
```
### __Containers executanto__
Quero saber quais containers estão executando:
```console
root@bdeveloperdeck101:~$ docker ps
```
Criar um novo bash em um container executando:
```console
root@bdeveloperdeck101:~$ docker exec -it CONTAINER_NAME bash
```
### __Fazendo os Container conversarem__
Funciona mas não é o melhor pois passa pelo host as mensagens:
```console
root@bdeveloperdeck101:~$ docker run --rm -ti -p 1234:1234 ubuntu:14.04 bash
```
Functiona mas infelizmente faz um link não dinâmico:

Server
```console
root@bdeveloperdeck101:~$ docker run --rm -ti --name server ubuntu:14.04 bash
```
Client
```console
root@bdeveloperdeck101:~$ docker run --rm -ti --link server --name client ubuntu:14.04 bash
```
### __Fazendo os Container conversarem de forma correta__
Criar uma rede:
```console
root@bdeveloperdeck101:~$ docker network create developerdeck101net
```
Criar um container:

Server
```console
root@bdeveloperdeck101:~$ docker run --rm -ti --net=developerdeck101net --name server ubuntu:14.04 bash
```

Client
```console
root@bdeveloperdeck101:~$ docker run --rm -ti --link server --net:developerdeck101net --name client ubuntu:14.04 bash
```

### __Criando nosso Ambiente MERN__
Backend Dockerfile
```console
FROM node:10.9.0-alpine
RUN mkdir -p /usr/src/app
WORKDIR /usr/src/app
RUN npm install -g nodemon --quiet
EXPOSE 3000
CMD ["npm", "start"]
```
Frontend Dockerfile
```console
FROM node:10.9.0-alpine
RUN mkdir -p /usr/src/app
EXPOSE 3000
CMD ["npm", "start"]
```
Docker compose file: docker-compose.yml
```console
version: '2'
services:
 mongodb:
  image: "mongo"
  ports:
  - "27017:27017"
 backend:
  build: ./devdeck101-backend/
  ports:
   - "4000:4000"
  volumes:
   - ./devdeck101-backend:/usr/src/app
  depends_on:
   - mongodb
 frontend:
   build: ./devdeck101-frontend/
   ports:
    - "3000:3000"
   volumes:
    - ./devdeck101-frontend:/usr/src/app
   depends_on:
    - backend
```
Construir seu Ambiente
```console
root@bdeveloperdeck101:~$ docker compose build
```
Iniciar seu Ambiente
```console
root@bdeveloperdeck101:~$ docker compose up
```
Desligar/Baixar/Parar seu Ambiente
```console
root@bdeveloperdeck101:~$ docker compose down
```

