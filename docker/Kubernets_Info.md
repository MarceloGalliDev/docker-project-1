# Kubernetes (K8s)

K8s é um orquestrador de containeres.

### Camadas do K8s
São separados em Pod, Controller, Service, Namespace

Todos containeres dentro de um pod compartilham do mesmo ip, rede, armazenamento, é a menor unidade de processamento dentro de um cluster kubernetes.
Controller é usado para manusear e controlar os pods, como update, create, delete, deploy, balanceamento entre outros.
Service é o caminho de acesso aos pods, identificando seu DNS e PORTA para acesso.
Namespace é uma tag que ajuda no filtro de grupos e identifica os objetos de um cluster kubernetes

### Arquitetura do K8s
São divididos em pods, deployment, replicaset, esse é uma arquitetura comumente usada.

O replicaSet são utilizados para gerenciar o uso dos pods, fazendo com que sejam monitorados e executado comandos de iniciar um novo pod caso haja falha ou apagar algum pod desnecessario.
O deployment é um controller, usado para manusear e controlar os replicaSet, aqui podemos definir estratégias de atualização ou fazer um rollback de versão, assegurando a disponibilidade e integridade do sistema.

POD < SERVICE < REPLICASET < DEPLOYMENT