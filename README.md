# Instalação do Kubernetes bare metal com o Ansible

## Configurando o hosts

Basta colocar o IP do master node e dos worker nodes. Os IPs podem ser locais ou externos com exceção do ***K8S_MASTER_INTERNAL_IP***, que deve ser o IP da rede interna da máquina onde o master node foi instalado.

Abaixo chega exemplo do arquivo host configurado. O master e o worker-1 tem IP públicos fictícios, e nas vars tem o IP interno do master

```
[k8s-master]
master      ansible_host=3.100.24.114

[k8s-workers]
worker-1    ansible_host=100.2.24.114

[all:vars]
K8S_MASTER_INTERNAL_IP=172.31.24.100
```

## Configurando a versão que será instalada

- Nesse arquivo de [vars](roles/install-docker/vars/main.yml) você pode modificar a versão do Docker que vai ser instalada.
- Nesse arquivo de [vars](roles/install-kubernetes/vars/main.yml) você pode modificar a versão do kubeadm, kublet e kubectl que vão ser instaladas.

## Antes de executar o Ansible
Se certificar de que as máquinas conseguem executar comandos em modo sudo sem precisar de senha e também configurar o acesso ssh sem seha para as máquinas. Também lembrar de liberar o tráfego interno na rede das máquinas.

## Executar o Ansible
```
ansible-playbook -i hosts k8s-install.yml
```
