# intro-docker

Exibir versão do Docker instalada: ````docker -- version````

Fazer um Hello World: ````docker run -ti hello-world````

Executar uma imagem do Debian: ````docker run -ti debian````

Executar uma imagem do DentOS versão 7 ```` docker run -ti centos:7 ````

Listar imagens docker: ````docker images````

Listar containers em execução: ````docker ps````

Listar todos os containers: ````docker ps -a````

Rodar Ubuntu: ````docker run -ti ubuntu /bin/bash````

Rodar CentOS versão 7: ````docker run -ti centos:7````

Listar containers em execução: ````docker ps````

Listar todos os containers: ````docker ps -a````

Sair de um container sem para-lo: ````CTRL+P+Q````

Entrar em um container: ````docker attach <CONTAINER ID>````

Listar todos os containers: ````docker ps -a````

Criar um container: ````docker create ubuntu````

inciar um container: ````docker start 2cae9d8a213c````

Executar um container: ````docker run -ti 2cae9d8a213c````

Executar um comando no container: ````ifconfig````

Parar um container: ````docker stop fe7bf2ad9448````

Iniciar um container: ````docker start fe7bf2ad9448````

Ver status do container: ````docker stats fe7bf2ad9448````

Ver containers em execução: ````docker ps````

Remover um container parado: ````docker rm 2cae9d8a213c````

Listar todos os containers: ````docker ps -a````

Remover um container que esteja em execução: ````docker rm -f fe7bf2ad9448````

Listar containers em execução: ````docker ps````

Listar todos os containers: ````docker ps -a````

Inspecionar um container: ````docker inspect 083606e5a077````

Nomear um container: ````docker run -ti --name teste debian````

Listar memória do container: ````docker inspect a4ba5ba4f099 | grep -i mem````

Atribuir memória a um container: ````docker run -ti --memory 512m --name novo_teste debian````

Listar memória do container: ````docker inspect a4ba5ba4f099 | grep -i mem````

Atualizar memória do container: ````docker update -m 256m 899c48361c94````

Listar memória do container: ````docker inspect a4ba5ba4f099 | grep -i mem````

Listar containers em execução: ````docker ps````

Listar todos os containers: ````docker ps -a````

Definir limite de uso de cpu pelo container: ````docker run -ti --cpu-shares 1024 --name container1 debian````

Listar limite de uso de cpu pelo container: ````docker inspect container1 | grep -i cpu````

Alterar limite de uso de cpu pelo container: ````docker updade --cpu-shares 512 container1````

### Volumes

Subir container passando um volume: ````docker run -ti -v /volume ubuntu /bin/bash````

confira as partições linux: ````df -h````

liste as pastas e arquivos: ls

Entre no volume: cd volume

Crie uma pasta: mkdir teste

Crie um arquivo: touch arquivo

Liste os containers em execução: docker ps

docker inspect -f {{.mounts}} 937ab35090e4

mkdir teste

cd teste

touch Dockerfile

docker run -ti -v primeiro_dockerfile:/volume debian

Se vc estiver usando Mac, o formato precisa ser assim: 

docker run -ti -v /Users/tell/teste:/volume debian

conferindo no host: docker inspect -f {{.Mounts}} 417913a0675b

conferindo no docker: docker attach 417913a0675b

criar um data-only

Vamos criar 2 containers Postgresql, com volume em eoutro container dbdados

Vamos fazer um bind da porta do host com a porta do container -p host:container

O -e serve para passar uma variavel de ambiente (enviroment)

docker run -d -p 5432:5432 --name pgsql1 --volumes-from dbdados -e POSTGRESQL_USER=docker -e POSTGRESQL_PASS=docker -e POSTGRESQL_DB=docker kamui/postgresql

docker run -d -p 5433:5432 --name pgsql2 --volumes-from dbdados -e POSTGRESQL_USER=docker -e POSTGRESQL_PASS=docker -e POSTGRESQL_DB=docker kamui/postgresql

Se você estiver usando Mac, para consegir visualizar o mapeamento, precisa disso antes: ````docker run -it --rm --privileged --pid=host justincormack/nsenter1````

Para visualizar o mapeamento: ````cd /var/lib/docker/volumes/c6af26baeb055c376b41c688f9fae8aa20322854972b57a5613f45f
25d88202a/_data````

### Dockerfile

````#imagem de origem
FROM debian

#nome do autor
MAINTEINER seu-nome

#Permite execuar comandos no container e instalar pacotes
#Ter cuidado pois cada linha de RUN cria uma camada no container
RUN apt-get update && apt-get install apache2 && apt-get clean

#adiciona arquivos,  diretorios e .tar  para dentro do container
ADD opa.txt /diretorio/

#o cmd é um parametro do entrypoint que é o principal processo do container
CMD ["sh", "-c", "echo", "$HOME"]

#Adicionar metadatas: versao, fabricante
LABEL Description = "Bla bla bla"

#copia arquivos não copia .tar, diferente do ADD
COPY opa.txt /diretorio/

#Permite definir o principal processo do container, 
#e caso esse processo morra
#o container também será finalizado
ENTRYPOINT ["/usr/bin/apache2ctl", "-D", "FOREGROUND"]

#Configura as variaveis de ambiente
ENV meunome="Tell"

#Define as portas do container que precisam ser expostas
EXPOSE 80

#Define usuário do container o default é root
USER nome-do-usuario-padrao

#define o diretório raiz
WORKDIR diretorio-de-trabalho-do-container

#define o volume
VOLUME /seu-diretorio ``````
`````

Dockerfile

`````FROM debian

RUN apt-get update && apt-get install -y apache2 && apt-get clean

ENV APACHE_LOCK_DIR="var/lock"
ENV APACHE_PID_FILE="var/run/apache2.pid"
ENV APACHE_RUN_USER="www-data"
ENV APACHE_RUN_GROUP="www-data"
ENV APACHE_LOG_DIR="/var/log/apache2"

LABEL Description="Webserver"

VOLUME /var/www/html

EXPOSE 80
`````
docker build -t webserver:1.0 .

docker images

telnet 172.17.0.2 80
ou
curl 172.17.0.2:80

docker attach e82777cbd7dd

### Docker Hub

hub.docker.com

docker ps

docker tag 6d345bacb63 tmoitas/webserver:1.0

docker images

docker login

docker push tmoitas/webserver:1.0


Parametros de rede para o container
Exibir modo bridge docker0: ifconfig



Passe um servidor de DNS que vai responder as requisições: docker run -ti --dns 8.8.8.8 debian

cat etc/resolv.conf

exit

Nome dentro do container: docker run -ti --hostname nome-container debian

cat /etc/hostname

exit


Linkar 2 containers

docker run -ti --name container1 debian

docker run -ti --link container1 --name container2 debian

ping container1

cat /etc/resolv.conf

cat /etc/hosts

docker run -ti --link --expose 80 debian

Conectar a posta do container com a porta do host: docker run -ti --publish 8080:80 debian









