# **Treinamentos  Kubernetes**



Colocar ✔ quando concluído. 

# **Treinamentos**

**LinuxTips - Descomplicando o Kubernetes** 

https://github.com/badtuxx/DescomplicandoKubernetes

**AcloudGuru**

**AWS**

**EDX**



# **Anotações**



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
