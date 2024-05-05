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

### Netshoot
Netshoot é uma ferramenta de diagnóstico de rede muito útil, popularmente usada em ambientes de contêineres, como aqueles geridos pelo Docker ou Kubernetes. É uma imagem Docker que contém uma ampla coleção de ferramentas de rede. Essas ferramentas podem ser usadas para solucionar problemas de conectividade e performance de rede em contêineres e entre contêineres em um cluster.

Netshoot inclui uma variedade de ferramentas de diagnóstico e análise de rede. Algumas das ferramentas mais comuns incluídas são:
- curl: Ferramenta para transferir dados de ou para um servidor, usando uma das muitas suportadas protocolos (HTTP, HTTPS, FTP, etc.).
- dig: Utilitário de DNS lookup.
- nmap: Utilitário para descoberta de rede e auditoria de segurança.
- tcpdump: Poderoso analisador de pacotes.
- netstat: Ferramenta para exibir conexões de rede, tabelas de roteamento, estatísticas de interface, masquerade connections, e multicast memberships.
- iperf: Ferramenta para medir a largura de banda da rede.
- mtr: Combinação de traceroute e ping para diagnóstico de rede.
- iftop: Display para uso de banda da rede em qualquer interface de rede.
- traceroute, ping, e muitas outras ferramentas úteis para o diagnóstico de rede.

Para executar um pod Netshoot interativo no Kubernetes, você pode usar o seguinte comando: (exemplo)
```
kubectl run --rm -i --tty netshoot --image=nicolaka/netshoot -- bash
```

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

### LoadBalancer
LoadBalancer Service é um tipo de serviço que fornece uma forma de expor aplicações ao tráfego externo de maneira automatizada e integrada com balanceadores de carga oferecidos por provedores de serviços em nuvem. Este serviço facilita a distribuição automática do tráfego de entrada entre os pods que estão rodando a aplicação, oferecendo maior disponibilidade e desempenho.
- Exposição Automática: Quando você cria um serviço do tipo LoadBalancer no Kubernetes, ele automaticamente solicita a criação de um balanceador de carga externo no provedor de nuvem que está sendo usado (como AWS, Google Cloud ou Azure). Este balanceador de carga recebe um IP público que pode ser usado para acessar o serviço.
- Distribuição de Tráfego: O tráfego que chega ao IP público do balanceador de carga é distribuído automaticamente entre os pods que estão associados ao serviço. Isso é feito de forma equitativa para garantir que nenhum pod receba uma carga desproporcional.

```
apiVersion: v1
kind: Service
metadata:
  name: meu-servico-loadbalancer
spec:
  type: LoadBalancer
  ports:
    - port: 80
      targetPort: 8080
  selector:
    app: minha-aplicacao
```

- type: LoadBalancer: Define o tipo de serviço como LoadBalancer.
- ports: Especifica as portas que o serviço vai expor. Neste exemplo, o tráfego no port 80 do balanceador de carga é direcionado para o port 8080 dos pods.
- selector: Define quais pods receberão o tráfego que passa pelo serviço. Neste caso, todos os pods com o label app: minha-aplicacao.