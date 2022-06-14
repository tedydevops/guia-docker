# //--------docker basics----------//
## CONTAINERS:
- :baby: exemplo:
  -  criar container da imagem nginx, 
  -  nome nginx1, 
  -  modo detach, 
  -  limitando esse container a utilizar somente 512 MB de RAM,
  -  limitando a utilizar somente 50% do CPU,
  -  mapeia volume na minha porta host pela porta do container, 
  -  expor a minha porta host 8080 pela 80 do container:
~~~
docker container run --name nginx1 -d -m 512M -c=".5" -v <host>:<container> -p 8080:80 nginx
~~~
- :writing_hand: executar container em modo interativo da linha de comando
~~~
docker container exec -it <container ID ou nome> bash
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
- :skull: deletar container:
~~~
docker rm <nome container ou id>
~~~
- :skull: deletar TODOS containers:
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
## DOCKER COMPOSE (sobe uma aplicação inteira, diversos containers, com um comando):
- :point_up: na pasta com o arquivo docker_compose.yaml: 
~~~
docker compose up
~~~
 
:thinking: toda documentação pelo comando:
~~~
docker --help
~~~

## DOCKER SWARM
1) iniciar vai gerar um leader e gerar um token:
~~~
docker swarm init
~~~
2) vai ser gerado um comando para adicionar worker nodes,
 - esse comando deve ser adicionado em cada maquina, 
  - mas para ser adicionado,
   - deve instalar antes docker pelo curl, 
    - e depois com sudo -su mudar nome do hostname:
~~~
curl -fsSL <.site docker...> | bash
hostname <nome do host mostrado no docker node ls do Leader>
docker swarm join <token enorme exibido do Leader>
~~~
- obs: mínimo de 1 cluster, numero impar para nao derrubar cluster: mais de 50% cluster ativos, sistema eleição
- obs:dentro do cluster qualquer ação binda o cluster todo
- o Leader permite que outros nós possam virar/desvirar Leader:
~~~
docker node promote/demote <nome node>
~~~
- adicionar manager: primeiro precisa gerar o token a ser colado no nó vazio, faça na maquina Leader:
~~~
docker swarm join-token manager
~~~
- adicionar worker: primeiro precisa gerar o token a ser colado no nó vazio, faça na maquina worker:
~~~
docker swarm join-token worker
~~~
- services:
~~~
docker service create --name <name> --replicas/--help
~~~
~~~
docker service
...            ps/inspect/scale/rm/rollback/update
~~~
- volumes:
~~~
docker volume
~~~
- network:
~~~
docker network create -d overlay <name>
~~~
:thinking: toda documentação pelo comando:
~~~
docker --help
~~~
### :open_mouth:!!!Diferente do RUN, o CMD executa apenas na criação do container e não no build da imagem. Deve ser único no Dockerfile.!!!
