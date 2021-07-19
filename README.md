# **Treinamentos  Kubernetes**



Colocar ✔ quando concluído. 

# **Treinamentos**



## ✔ **Linux Foundation**

https://learning.edx.org/course/course-v1:LinuxFoundationX+LFS158x+3T2020/home



## **Apresentação - Curso de Introdução ao Kubernetes**

https://docs.google.com/presentation/d/1weqpBWa9FNjKc1ugCUIpwYYquvoIOFbUvEcZ9ZYapAg/edit#slide=id.g23786ddafa_0_68

**Curso Introdução ao Kubernetes**

Apresentação https://www.youtube.com/watch?v=RuNTvYejG90&feature=youtu.be

- 01 - Revisão docker - https://www.youtube.com/watch?v=bcRArpK00OU&feature=youtu.be
- 02 - O que é Kubernetes?https://www.youtube.com/watch?v=X2r09kPi8aA&feature=youtu.be
- 03 - Arquitetura do K8s - https://www.youtube.com/watch?v=bPFxwwSfSmk&feature=youtu.be
- 04 Conceitos importantes do K8s - https://www.youtube.com/watch?v=Y0kHzwifFEA&feature=youtu.be
- 05 Instalação dos componentes do K8s - https://www.youtube.com/watch?v=7H61VJV0YI8&feature=youtu.be
- 06 Configuração do K8s (53:48) - https://www.youtube.com/watch?v=V1g0alYqI1w&feature=youtu.be
- 07 ReplicaSet (7:14) - https://www.youtube.com/watch?v=qfiQyTqzUqU&feature=youtu.be
- 08 Deployment (18:52) - https://www.youtube.com/watch?v=2JbQkTF6TzU&feature=youtu.be
- 09 Service (27:30) - https://www.youtube.com/watch?v=zGqMvzbWAJc&feature=youtu.be
- 10 Microservices (7:48) - https://www.youtube.com/watch?v=SS748X6xvdk&feature=youtu.be



## **LinuxTips - Descomplicando o Kubernetes** 

https://github.com/badtuxx/DescomplicandoKubernetes



## **Linux Tips - Canary Deploy**



https://www.youtube.com/watch?v=CTvsdWZrAW0

https://github.com/badtuxx/k8s-canary-deploy-example

## **AcloudGuru**

## **AWS**



## **Monitoramento**

https://kubedev.io/bonus-monitoramento/


![image](https://user-images.githubusercontent.com/31936133/125138813-ba243600-e0e5-11eb-9b86-531dc4c54311.png)

# **Anotações**

## Laboratório K8S

https://labs.play-with-k8s.com/



## Componentes do K8s

**O k8s tem os seguintes componentes principais:**

- Master node
- Worker node
- Services
- Controllers
- Pods
- Namespaces e quotas
- Network e policies
- Storage

**[kube-apiserver](https://kubernetes.io/docs/concepts/overview/components/#kube-apiserver)** é a central de operações do cluster k8s. Todas as chamadas, internas ou externas são tratadas por ele. Ele é o único que conecta no ETCD.

**[kube-scheduller](https://kubernetes.io/docs/concepts/overview/components/#kube-apiserver)** usa um algoritmo para verificar em qual node o pod deverá ser hospedado. Ele verifica os recursos disponíveis do node para verificar qual o melhor node para receber aquele pod.

No **[ETCD](https://kubernetes.io/docs/concepts/overview/components/#etcd)** são armazenados o estado do cluster, rede e outras informações persistentes.

**[kube-controller-manager](https://kubernetes.io/docs/concepts/overview/components/#cloud-controller-manager)** é o controle principal que interage com o `kube-apiserver` para determinar o seu estado. Se o estado não bate, o manager irá contactar o controller necessário para checar seu estado desejado. Tem diversos controllers em uso como: os endpoints, namespace e replication.

O **[kubelet](https://kubernetes.io/docs/concepts/overview/components/#kubelet)** interage com o Docker instalado no node e garante que os contêineres que precisavam estar em execução realmente estão.

O **[kube-proxy](https://kubernetes.io/docs/concepts/overview/components/#kube-proxy)** é o responsável por gerenciar a rede para os contêineres, é o responsável por expor portas dos mesmos.

**[Supervisord](http://supervisord.org/)** é o responsável por monitorar e restabelecer, se necessário, o `kubelet` e o Docker. Por esse motivo, quando existe algum problema em relação ao kubelet, como por exemplo o uso do driver `cgroup` diferente do que está rodando no Docker, você perceberá que ele ficará tentando subir o kubelet frequentemente.

**[Pod](https://kubernetes.io/docs/concepts/workloads/pods/pod-overview/)** é a menor unidade que você irá tratar no k8s. Você poderá ter mais de um contêiner por Pod, porém vale lembrar que eles dividirão os mesmos recursos, como por exemplo IP. Uma das boas razões para se ter mais de um contêiner em um Pod é o fato de você ter os logs consolidados.

O Pod, por poder possuir diversos contêineres, muitas das vezes se assemelha a uma VM, onde você poderia ter diversos serviços rodando compartilhando o mesmo IP e demais recursos.

**[Services](https://kubernetes.io/docs/concepts/services-networking/service/)** é uma forma de você expor a comunicação através de um **NodePort** ou **LoadBalancer** para distribuir as requisições entre diversos Pods daquele Deployment. Funciona como um balanceador de carga.

## Principais Comandos

A figura a seguir mostra a estrutura dos principais comandos do `kubectl`.

| [![Principais Comandos](https://github.com/badtuxx/DescomplicandoKubernetes/raw/main/images/kubernetes_commands.png)](https://github.com/badtuxx/DescomplicandoKubernetes/blob/main/images/kubernetes_commands.png) |
| ------------------------------------------------------------ |
| *Principais comandos [Ref: uploaddeimagens.com.br](https://uploaddeimagens.com.br/images/002/667/919/full/Kubernetes-Comandos.png)* |

## Container Network Interface

Para prover a rede para os contêineres, o k8s utiliza a especificação do **CNI**, Container Network Interface.

CNI é uma especificação que reúne algumas bibliotecas para o desenvolvimento de plugins para configuração e gerenciamento de redes para os contêineres. Ele provê uma interface comum entre as diversas soluções de rede para o k8s. Você encontra diversos plugins para AWS, GCP, Cloud Foundry entre outros.

Mais informações em: https://github.com/containernetworking/cni

Enquanto o CNI define a rede dos pods, ele não te ajuda na comunicação entre os pods de diferentes nodes.

As características básicas da rede do k8s são:

- Todos os pods conseguem se comunicar entre eles em diferentes nodes;
- Todos os nodes pode se comunicar com todos os pods;
- Não utilizar NAT.

Todos os IPs dos pods e nodes são roteados sem a utilização de [NAT](https://en.wikipedia.org/wiki/Network_address_translation). Isso é solucionado com a utilização de algum software que te ajudará na criação de uma rede Overlay. Seguem alguns:

- [Weave](https://www.weave.works/docs/net/latest/kube-addon/)
- [Flannel](https://github.com/coreos/flannel/blob/master/Documentation/kubernetes.md)
- [Canal](https://github.com/tigera/canal/tree/master/k8s-install)
- [Calico](https://docs.projectcalico.org/latest/introduction/)
- [Romana](http://romana.io/)
- [Nuage](https://github.com/nuagenetworks/nuage-kubernetes/blob/v5.1.1-1/docs/kubernetes-1-installation.rst)
- [Contiv](http://contiv.github.io/)

Mais informações em: https://kubernetes.io/docs/concepts/cluster-administration/addons/

## Volumes

**EmptyDir** 

Um volume do tipo **EmptyDir** é criado sempre que um Pod é atribuído a um nó existente. Esse volume é criado inicialmente vazio, e todos os contêineres do Pod podem ler e gravar arquivos no volume.

Esse volume não é um volume com persistência de dados. Sempre que o Pod é removido de um nó, os dados no `EmptyDir` são excluídos permanentemente. É importante ressaltar que os dados não são excluídos em casos de falhas nos contêineres.

Disco disponível somente enquando o pod estiver rodando.

Recomendado para logs por exemplo.

Disco no Node em /var/lib/kubelet/pods , find . -iname "*nomedodisco*"



**Persistent Volume**

O subsistema **PersistentVolume** fornece uma API para usuários e administradores que resume detalhes de como o armazenamento é fornecido e consumido pelos Pods. Para o melhor controle desse sistema foi introduzido dois recursos de API: `PersistentVolume` e `PersistentVolumeClaim`.

Um **PersistentVolume** (PV) é um recurso no cluster, assim como um nó. Mas nesse caso é um recurso de armazenamento. O PV é uma parte do armazenamento no cluster que foi provisionado por um administrador. Os PVs tem um ciclo de vida independente de qualquer pod associado a ele. Essa API permite armazenamentos do tipo: NFS, ISCSI ou armazenamento de um provedor de nuvem específico.

Um **PersistentVolumeClaim** (PVC) é semelhante a um Pod. Os Pods consomem recursos de um nó e os PVCs consomem recursos dos PVs.

Mas o que é um PVC? Nada mais é do que uma solicitação de armazenamento criada por um usuário.

Vamos criar um `PersistentVolume` do tipo `NFS`, para isso vamos instalar os pacotes necessários para criar um NFS Server no GNU/Linux.

Sequencia: Cria o **PV** depois o **PVC**.







## Kubectl Taint

O **Taint** nada mais é do que adicionar propriedades ao nó do cluster para impedir que os pods sejam alocados em nós inapropriados.

Por exemplo, todo nó `master` do cluster é marcado para não receber pods que não sejam de gerenciamento do cluster.

O nó `master` está marcado com o taint `NoSchedule`, assim o scheduler do Kubernetes não aloca pods no nó master, e procurar outros nós no cluster sem essa marca.

```yaml
## NoSchedule - Novos containers não são executados no node
**Habilitado** - kubectl taint node k8s-worker-01 key1=value1:NoSchedule
**Desabilitado** - kubectl taint node k8s-worker-01 key1=value1:NoSchedule-

## NoExecute - Não executa containers no node, ele mata e migra para outro node
**Habilitado** - kubectl taint node elliot-03 key1=value1:NoExecute
**Desabilitado** - kubectl taint node elliot-03 key1=value1:NoExecute-
```



## **Label**

O **Node Selector** é uma forma de classificar nossos nodes como por exemplo nosso node `elliot-02` que possui disco **SSD** e está localizado no DataCenter `UK`, e o node `elliot-03` que possui disco **HDD** e está localizado no DataCenter `Netherlands`.

Para criar pods em nodes com o Label "disk""HDD", adiciona no deployment  no spec do pod a opção abaixo.

```yaml
 nodeSelector:
              disk: HDD
```



## **Deployments**

**service-clusterip.yaml**

```yaml
apiVersion: v1
kind: Service
metadata:
  labels:
    run: nginx
  name: nginx-clusterip
  namespace: default
spec:
  externalTrafficPolicy: Cluster
  ports:
  - port: 80
    protocol: TCP
    targetPort: 80
  selector:
    run: nginx
  sessionAffinity: None
  type: ClusterIP
```

**service-nodeip.yaml**

```yaml
apiVersion: v1
kind: Service
metadata:
  labels:
    run: nginx
  name: nginx-nodeport
  namespace: default
spec:
  externalTrafficPolicy: Cluster
  ports:
  - nodePort: 32548
    port: 80
    protocol: TCP
    targetPort: 80
  selector:
    run: nginx
  sessionAffinity: ClientIP
  type: NodePort
```



**service-loadbalancer.yaml**

```yaml
apiVersion: v1
kind: Service
metadata:
  labels:
    run: nginx
  name: nginx-loadbalancer
  namespace: default
spec:
  externalTrafficPolicy: Cluster
  ports:
  - nodePort: 32548
    port: 80
    protocol: TCP
    targetPort: 80
  selector:
    run: nginx
  sessionAffinity: None
  type: LoadBalancer
```



**deployment-limitado.yaml** 

```yaml
apiVersion: extensions/v1beta1
kind: Deployment
metadata:
  labels:
    run: nginx
  name: nginx-limitado
  namespace: default
spec:
  progressDeadlineSeconds: 600
  replicas: 1
  revisionHistoryLimit: 2
  selector:
    matchLabels:
      run: nginx
  strategy:
    rollingUpdate:
      maxSurge: 25%
      maxUnavailable: 25%
    type: RollingUpdate
  template:
    metadata:
      creationTimestamp: null
      labels:
        run: nginx
    spec:
      containers:
      - image: nginx
        imagePullPolicy: Always
        name: nginx
        ports:
        - containerPort: 80
          protocol: TCP
        resources:
          limits:  ## Quando o K8S vai liberar para esse deployment
            memory: 128Mi
            cpu: 1
          requests: ## Minimo garantido que o K8S vai liberar para esse deployment
            memory: 96Mi
            cpu: 1
        terminationMessagePath: /dev/termination-log
        terminationMessagePolicy: File
      dnsPolicy: ClusterFirst
      restartPolicy: Always
      schedulerName: default-scheduler
      securityContext: {}
      terminationGracePeriodSeconds: 30
```

```yaml
Atenção! 1 core de CPU corresponde a 1000m (1000 milicore). Ao especificar 200m, estamos querendo reservar 20% de 1 core da CPU. Se fosse informado o valor 0.2 teria o mesmo efeito, ou seja, seria reservado 20% de 1 core da CPU.
```







```yaml
cat > /etc/docker/daemon.json <<EOF
{
  "exec-opts": ["native.cgroupdriver=systemd"],
  "log-driver": "json-file",
  "log-opts": {
    "max-size": "100m"
  },
  "storage-driver": "overlay2"
}
EOF


# sudo mkdir -p /etc/systemd/system/docker.service.d
# systemctl daemon-reload
# systemctl restart docker
# docker info | grep -i cgroup
```

Se a saída foi Cgroup Driver: systemd, tudo certo!

## 





# **Comandos Kubernetes**





|                           Comando                            | Descrição                                                    |
| :----------------------------------------------------------: | :----------------------------------------------------------- |
| kubeadm init --control-plane-endpoint "k8s-elb-01:6443" --upload-certs | subir o cluster com elb                                      |
|          kubeadm token create --print-join-command           | Restaurar o token do join p/ worker node                     |
| kubectl apply -f "https://cloud.weave.works/k8s/net?k8s-version=$(kubectl version \|base64 \|tr -d '\n')" | Instalação do pod network para ter a comunicação entre pods de diferentes nodes |
|  kubeadm init --apiserver-advertise-address $(hostname -i)   | Inicializa cluster                                           |
|  echo "source <(kubectl completion bash)" >> /root/.bashrc   | auto complete                                                |
|               kubectl run nginx --image=nginx                | Cria um POD                                                  |
|              kubectl get pods nginx **-o yaml**              | mostra o manifesto do pod                                    |
| kubectl run meu-nginx --image nginx **--dry-run=client** -o yaml > pod-template.yaml | Opção DryRun não Cria o POD                                  |
| kubectl create deployment meu-nginx --image=nginx **--dry-run=client** -o yaml > deployment-template.yaml | Opção DryRun não Cria o Deployment                           |
|                  kubectl explain "recurso"                   | Explica o recurso "main page"                                |
|                        kubectl expose                        | Cria Services                                                |
|                    kubectl logs -f nginx                     | Analise de Logs                                              |
|        kubectl create deployment nginx --image=nginx         |                                                              |
|    kubectl scale deployment "*nomedeploy*" --replicas=40     |                                                              |
|              kubectl get pods -l dc="**label**"              | Lista os pods com o Label                                    |
|               kubectl get pods **-L** "label"                | Lista os pods com o label "DC"                               |
|                                                              |                                                              |
|                                                              |                                                              |
|                                                              |                                                              |
|                                                              |                                                              |
|                                                              |                                                              |
|                                                              |                                                              |
|                                                              |                                                              |
|                                                              |                                                              |
|                                                              |                                                              |
|                                                              |                                                              |
|                                                              |                                                              |
|                                                              |                                                              |
|                                                              |                                                              |

# **Best Practices**

**Tipos de topologias de K8s multi-master**

https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/ha-topology/



**Instalação kubeadm, kubelet e kubectl**

https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/install-kubeadm/



**Instalação Kubernetes multi-master**

https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/high-availability/



**HAproxy**

https://www.haproxy.org/



**Options for Highly Available topology**

https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/ha-topology/



**Creating Highly Available clusters with kubeadm**

https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/high-availability/
