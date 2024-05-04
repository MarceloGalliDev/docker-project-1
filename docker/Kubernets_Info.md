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

### NodePort
No Kubernetes, o NodePort é um tipo de serviço que expõe um serviço em uma porta estática no IP de cada nó do cluster. É um dos modos pelos quais você pode tornar um serviço acessível externamente, fora do cluster Kubernetes. NodePort é uma forma simples e fácil de obter acesso externo a um dos serviços dentro de seu cluster Kubernetes.

Como Funciona o NodePort
Quando você configura um serviço Kubernetes com o tipo NodePort, o Kubernetes reserva uma porta específica em todos os nós do cluster (essa porta é geralmente um valor na faixa de 30000-32767). Qualquer tráfego que chega a esta porta em qualquer nó é automaticamente encaminhado para o serviço correspondente dentro do cluster.

Exemplo:
```
apiVersion: v1
kind: Service
metadata:
  name: meu-servico
spec:
  type: NodePort
  ports:
    - port: 80
      targetPort: 8080
      nodePort: 30007
  selector:
    app: minha-aplicacao

```
- port: A porta que será exposta pelo serviço dentro do cluster.
- targetPort: A porta que o Pod dentro do cluster está ouvindo.
- nodePort: A porta que será exposta em cada nó do cluster. Se você não especificar essa porta, o Kubernetes escolherá automaticamente uma porta na faixa padrão (30000-32767).
