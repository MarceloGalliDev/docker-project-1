## Commands
<b>Para startar a imagem no docker</b></br>
<i>-p indica para ouvir a porta redirecionada</i>
```
docker run -d -p 8800:80 httpd
```

<b>To show images loaded from the container</b>
```
curl localhost:8800
```

<b>To show running containers</b>
```
docker ps
```

<b>To check the ports in use</b></br>
<i>Mac:</i> 
```
lsof -i :<port>
```  
<i>Windows:</i>
```
netstat
```


## Instations for docker
If it's a debian-based image (the default nginx) then you can also use `apt-get update && apt-get install -y iputils-ping` inside the container to install it.

You can add it back in using the apt package manager. `apt-get update && apt-get install procps`

O uso de bridge nos comandos do docker, indica que estou fazendo ligação entre os containeres incluidos naquela bridge, possibilitando a interação entre eles

## Examples of Docker configuration
O comando abaixo faz uma criação de um container com a ultima imagem do nginx
Abre a porta 80 do meu hostIp e direciona para a porta 80 do container
```
docker container run --publish 80:80 nginx
```

O uso do -detach é para executar em segundo plano ou -d é a mesma coisa
```
docker container run --publish 80:80 --detach nginx
docker container run --publish 80:80 -d nginx
```

Nomeando um container usamos o --name
```
docker container run --publish 80:80 --detach --name {name_container_unique} nginx
```

O uso do stop pode ser usado somente os primeiros numeros do container_id
```
docker container stop {container_id}
```

Para visualização de logs
```
docker container logs {name_container}
```

Para verificarmos que processos estão rodando dentro do container
```
docker container top {name_container}
```

Para excluição de containeres
O uso do -f é para forçar a exclusão do container
```
docker container rm -f {id_container1} {id_container2} ... {id_container}
```

Quando executarmos um container que utiliza de enviroments, usamos o --env ou -e
Depois verificamos os logs para pegar a senha
```
docker container run --publish 8080:80 -d --name mysql_container -e MYSQL_RANDOM_ROOT_PASSWORD=true
docker container logs mysql_container
```

Listar detalhes de um container
```
docker container inspect {name_container}
```

Verificar status de todos containers
```
docker container status
```

Aqui iniciamos um container interativo
Container interativo nos permite acessa-lo com um shell terminal
No caso de uma imagem Ubuntu, nao tem necessidade de exemplificar o bash no comando para acessar o terminal
```
docker container run -it
```

Para eu iniciar um container ja criado, sendo interativo ou nao
```
docker container start -ai ou -a {name_container}
```

Para eu acessar um container em execução
```
docker container exec -it {name_container} {software}
```

Para eu verificar as portas do container em execução
```
docker container port {name_container}
```

Para eu acessar as informações formatadas do container
```
docker container inspect --format '{{ .NetworkSettings.IPAddress }}' {name_container}
```

## Docker Networks - CLI management
O uso de networks em docker nos permite criar redes virtuais isoladas, podemos criar nossa propria rede virtual e incluido comunicação com outros containeres dentro da rede que nos especificamos.
exemplo:
```
para criar a network
docker network create --driver bridge minha_rede

criado container e incluido o network nele
docker run -d --name meu-redis --network minha_rede redis
```

Verificar as Networks
```
docker network ls
```

inspect nas Networks
```
docker network inspect {nome da network}
```

Para criar uma nova rede virtual com drive especificado
```
docker network create --driver
```

Para conectar ou desconectar
```
docker network connect/disconnect
```

Quando criamos uma nova rede virtual, la recebe um recurso que criar DNS automatico para cada container, fazendo com que mesmo que altere o IP ambos os containeres dentro dessa rede mantenha-se conectados
Para ativar o DNS na rede padrão
```
docker network --link
```

## Links for documentation
para fazer um format no inspect => https://docs.docker.com/config/formatting/ </br>

## Create a docker image in my repository
usamos o comando para copiar e nomear uma tag
```
docker image tag {repositorio}/{nome_tag_original} {repositorio}/{nome_tag_atualizado} 
```

## Reference dockerfile
https://docs.docker.com/reference/dockerfile/
https://docs.docker.com/storage/
