# **Treinamentos  Kubernetes**



Colocar ✔ quando concluído. 

# **Treinamentos**

**LinuxTips - Descomplicando o Kubernetes** 

https://github.com/badtuxx/DescomplicandoKubernetes

# **Anotações**

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


sudo mkdir -p /etc/systemd/system/docker.service.d
systemctl daemon-reload
systemctl restart docker

docker info | grep -i cgroup

Se a saída foi Cgroup Driver: systemd, tudo certo!

## inicializa cluster
kubeadm init --apiserver-advertise-address $(hostname -i)

Instalação do pod network
para ter a comunicação entre pods de diferentes nodes
modprobe br_netfilter ip_vs_rr ip_vs_wrr ip_vs_sh nf_conntrack_ipv4 ip_vs
kubectl apply -f "https://cloud.weave.works/k8s/net?k8s-version=$(kubectl version | base64 | tr -d '\n')"


# 





# **Comandos Kubernetes**





|                           Comando                            | Descrição                                |
| :----------------------------------------------------------: | :--------------------------------------- |
| kubeadm init --control-plane-endpoint "k8s-elb-01:6443" --upload-certs | subir o cluster com elb                  |
|          kubeadm token create --print-join-command           | Restaurar o token do join p/ worker node |
|                                                              |                                          |
|                                                              |                                          |
|                                                              |                                          |
|                                                              |                                          |
|                                                              |                                          |
|                                                              |                                          |
|                                                              |                                          |
|                                                              |                                          |
|                                                              |                                          |
|                                                              |                                          |
|                                                              |                                          |
|                                                              |                                          |
|                                                              |                                          |
|                                                              |                                          |
|                                                              |                                          |
|                                                              |                                          |
|                                                              |                                          |
|                                                              |                                          |
|                                                              |                                          |
|                                                              |                                          |
|                                                              |                                          |
|                                                              |                                          |
|                                                              |                                          |
|                                                              | kend                                     |
|                                                              |                                          |
|                                                              |                                          |
|                                                              |                                          |

# **Best Practices**

Tipos de topologias de K8s multi-master: https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/ha-topology/

Instalação kubeadm, kubelet e kubectl: https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/install-kubeadm/

Instalação Kubernetes multi-master: https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/high-availability/

HAproxy: https://www.haproxy.org/



**Options for Highly Available topology**

https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/ha-topology/

**Creating Highly Available clusters with kubeadm**

https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/high-availability/
