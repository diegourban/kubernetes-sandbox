# kubernetes-sandbox

- Kubernetes é um cluster que administra e orquestra container
- Minikube é um ambiente de teste do Kubernetes
- Para rodar Minikube serve o comando: minikube start
- kubectl é a ferramenta na linha de comando para gerenciar o cluster Kubernetes
- Para definir um container no Kubernetes é preciso definir um Pod
 - Um Pod é a menor unidade de deploy no Kubernetes
 - Um Pod agrupa um ou mais containers que compartilham a mesma interface de rede e sistema de arquivos
 - Um Pod é um objeto no Kubernetes descrito por um arquivo YML
 - O YML do Pod define qual é a imagem, porta, versão, nome entre outras configurações
 
- Kubernetes consiste de masters e nodes/minions;
- um Deployment funciona como um controlador do Pod
 - um deployment define as quantidade das replicas
 - um deployment garante a disponibilidade do Pod
- para ter acesso ao deployment fora do Kubernetes precisa de um Service
 - existem vários tipos de serviços, entre eles o LoadBalancer
 - o serviço fica associado ao deployment ou Pods através do Selector 
- minikube service <nome-service> --url devolve a URL para testar o service

- um Deployment é um controller stateless e não compartilha nenhuma informação entre Pods
- um StatefulSet permite compartilhar informações entre Pods
- para tal devemos definir um volumeMounts, volumes e um PersistentVolumeClaim
 - o volumeMounts define a pasta concreta de montagem e dá um nome para o volume
 - o item volumes associa nome do volume com uma permissão
 - o PersistentVolumeClaim define as permissões e o tamanho do recurso

- Parametrização de CPU e memória de cada Pod
 - a configuração para tal é feita no container através de um elemento resources onde podemos especificar requests e limits
 - requests é o valor o container está garantido de ter
 - limits é o máximo permitido o que o container terá disponível
```
    resources:
    requests:
      memory: "16Mi"
      cpu: "100m"
    limits:
      memory: "32Mi"
      cpu: "200m"
```

- Replicação automática do ambiente usando a tarefa Horizontal Pod Autoscaler
 - nessa configuração definimos o valor do CPU que, quando ultrapassa, causa um aumento de replicas
```
    kubectl autoscale \
    deployment \
    aplicacao-noticia-deployment \
    --cpu-percent=50 \
    --min=1 \
    --max=10
```

- Aprendemos também como habilitar um addon no Minikube:
 - um addon é um plugin/funcionalidade extra do minikube

para listar os addons
```minikube addons list```

para habilitar
```minikube addons enable metrics-server```

Para desabilitar
```minikube addons disable metrics-server```

## Comandos Minikube

O Minikube implementa um cluster local do Kubernetes para Linux, Mac e Windows. O objetivo principal é ser uma ótima ferramenta para o desenvolvimento local de aplicativos Kubernetes para experimentar, aprender, rodar testes e usar na integração contínua.

Para iniciar o Minikube:
```minkube start```

Para iniciar o Minikube com uma versão especifica do Kubernetes:
```minikube start --kubernetes-version="v1.16"```

Para acessar o dashboard do Kubernetes em execução:
```minikube dashboard```

Para ver o status do Minikube:
```minikube status```

Para parar o cluster:
```minikube stop```

Para se conectar pelo SSH com o nó master do cluster:
```minikube ssh```

E para remover o cluster:
```minikube delete```

E para remover todos os clusters e perfis:
```minikube delete --all```

## Comandos kubectl

para listar os pods
```kubectl get pods```

tbm funciona para deployments e services, por exemplo:
```kubectl get services```

para detalhes de um pod
```kubectl describe pod <nome-pod>```

o comando describe tbm funciona para deployment e service, por exemplo:
```kubectl describe service <nome>```

para criar pod, deployment ou service a partir de um arquivo yml
```kubectl create -f <nome-arquivo-yml>```

para remover pod, deployment ou service a partir de um arquivo yml
```kubectl delete -f <nome-arquivo-yml>```

para remover um pod
```kubectl delete pod <nome-pod>```

para remover um deployment
```kubectl delete deployment <nome-deployment>```

para remover um service
```kubectl delete service <nome-service>```
