## Commands
<b>Para startar a imagem no docker</b></br>
<i>-p indica para ouvir a porta redirecionada</i>
```
docker run -d -p 8800:80 httpd
```

<b>Para carregar á página carregada pela imagem</b>
```
curl localhost:8800
```

<b>Para mostrar os containeres em execução</b>
```
docker ps
```

<b>Para verificar as portas em uso</b></br>
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

