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

