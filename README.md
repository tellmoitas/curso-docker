# curso-docker

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

  
