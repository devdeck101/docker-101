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

