# Kubernetes (K8s)

K8s é um orquestrador de containeres.

### Camadas do K8s
São separados em Pod, Controller, Service, Namespace

Todos containeres dentro de um pod compartilham do mesmo ip, rede, armazenamento, é a menor unidade de processamento dentro de um cluster kubernetes.
Controller é usado para manusear e controlar os pods, como update, create, delete, deploy, balanceamento entre outros.
Service é o caminho de acesso aos pods, identificando seu DNS e PORTA para acesso.
Namespace é uma tag que ajuda no filtro de grupos e identifica os objetos de um cluster kubernetes