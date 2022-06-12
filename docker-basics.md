# //--------docker basics----------//
## CONTAINERS:
- :baby:criar container da imagem nginx, nome nginx1, modo detach, expor a minha porta host 8080 pela 80 do container:
~~~
docker container run --name nginx1 -d -p 8080:80 nginx
~~~
- :writing_hand: executar container em modo interativo da linha de comando
~~~
docker container exec -it <container ID ou nome>
~~~
- :eyes: checar quais conteiners running:
~~~
docker ps 
~~~
- :eyes: checar TODOS conteiners independente de running:
~~~
docker ps -a
~~~
- :eyes: checar status container:
~~~
docker status <container ID ou nome>
~~~
- :pause_button: :arrow_forward:startar / stop container:
~~~
docker container start/stop <container ID ou nome>
~~~
- :skull:deletar container:
~~~
docker rm <nome container ou id>
~~~
- :skull:deletar TODOS containers:
~~~
docker rm $(docker ps -qa)
~~~
- :writing_hand: acessar container:
~~~
docker attach <conteiner ID>
~~~
- :trident: versionar container:
~~~
docker commit <conteiner ID> <nome da imagem>:<tag>
~~~
## IMAGES:
- :eyes: checar todas imagens:
~~~
docker images
~~~
- :skull: deletar imagem:
~~~
docker rmi <nome imagem ou id>
~~~
- :skull: deletar TODAS imagens que não estão em uso:
~~~
docker image prune
~~~
- :skull: deletar TODAS imagens(msm se estiver sendo usada):
~~~
docker rmi $(docker images -q) -f
~~~
- :currency_exchange: retagear imagem existente:
~~~
docker image tag <nome da imagem>:<TAG>
~~~
## DOCKER FILE build
- :baby: criar imagem com a tag=<>, dentro da pasta com Dockerfile:
~~~
docker build -t <usuario dockerhub/nome da sua imagem> .
~~~
### Diferente do RUN, o CMD executa apenas na criação do container e não no build da imagem. Deve ser único no Dockerfile.
