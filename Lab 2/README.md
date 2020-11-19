# Lab 3: Microstack

- **Disciplina:** CSC-05: Operações Cibernéticas e Jogos de Guerra Cibernética - Lado Defesa
- **Aluno:** Gianluigi Dal Toso
- **Turma:** 2021
- **Data:** 19/10/2020

Este relatório também pode ser conferido online (em formato Markdown) pela URL: [URL-AQUI](URL-AQUI)

---

Neste relatório serão descritos os passos realizados ao seguir o roteiro disponível para o _Laboratório 3: Microstack_.

A execução do laboratório foi gravada no formato _asciinema_ (gravação do terminal, sem intervalo entre comandos). Para cada subseção à seguir, serão disponibilizados os links referentes as gravações.

O Laboratório foi executado no seguinte ambiente:
- **Sistema Operacional**: Arch Linux x64 (5.8.8-arch1-1)
- **CPU**: Intel i7-6500U
- **RAM**: 8 GB
- **GPU**: Intel Skylake GT2 [HD Graphics 520]


**Tabela de Conteúdos**:

COLOCAR TOC AQUI
---

## Parte 1: Preparação de ambiente


### 1) Preparar uma VM Ubuntu 18.04 para os experimentos

Usar a seguinte configuração do Vagrant:
```conf
Vagrant.configure("2") do |config|
    config.vm.box = "ubuntu/bionic64"
    config.vm.hostname = "controller"
    config.disksize.size = '50GB'
    config.vm.provider "virtualbox" do |vb|
        vb.memory = 8192
        vb.cpus = 4
        vb.customize ["modifyvm", :id, "--nested-hw-virt", "on"]
    end
    config.vm.network :private_network, ip: "172.16.2.25"
end
```

E usar os comandos
```bash
vagrant up
vagrant ssh
lscpu | grep Virtualization
```
---
![]()

### 2) Instalar o snapd e o microstack
```
sudo apt uodate
sudo apt install snapd -y
sudo snap install microstack --beta -classic
```

### 3) Preparar a configuração do microstack
```
sudo microstack.init
```

### 4) Acesse via browser o microstack completo (login: admin / senha: keystone)

### 5) Procure nessa página de gerenciamento do OpenStack quantos vCPUs estão disponíveis, quanto de memória disponível para VMs, e quanto de disco disponível para VMs. (Admin » Compute » Hypervisors)


### 6) Verifique que o projeto "admin: possui uma "imagem" pronta para ser usada (imagem "cirros") com tamanho de 12.3MB

### 7) Verifique a configuração da rede

```
rede interna (entre VMs)
rede externa (onde um roteador permite o acesso)
```

### 8) Verifique que foi configurado um roteador virtual

### 9) Fazer teste de ping da VM Ubuntu para a interface externa do roteador

```
ping 10.20.20.203
```



---
## Parte 2: Comandos de "OpenStack"

### 1) Visualizar as imagens, flavors, redes cadastradas
```
microstack.openstack image list
microstack.openstack network list
microstack.openstack flavor list
```

### 2) Comandos para criar uma máquina virtual "cirros"
```
microstack.openstack server create --flavor m1.small --nic net-id=test --image cirros meu-servidor
```


### 3) Configurar e atribuir um endereço "externo" para a VM

```
microstack.openstack floating ip create -f value -c floating_ip_address external
microstack.openstack server add floating ip meu-servidor <valor do comando anterior>
```




###