//--------docker basico----------//
 
//--1) instalando UBUNTU: 
docker pull ubuntu
docker images
docker run -it (ID da imagem ubunto aqui) /bin/bash
apt-get update

//---checar quais conteiners running:
docker ps 

//---checar quais conteiners independente de running:
docker ps -all

//---conectar conteiner:
docker attach (conteiner ID aqui)

//---versionar container:
docker commit (conteiner ID aqui) ubuntu:(nomear uma tag aqui)

fim