# CentOS 6x
Configurações iniciais para sistemas linux CentOS 6x

## Sumário
- [CentOS 6x](#centos-6x)
  - [Sumário](#sumário)
   - [Configurar IP Fixo](#configurar-ip-fixo)
   - [Definir DNS](#definir-dns)
   - [Atualizar Sistema](#atualizar-sistema)
   - [Instalar SSH](#instalar-ssh)
   - [Definir HOSTNAME](#definir-hostname)   
   - [Verificações](#verificações)   
   - [VMWare Tools](#vmware-tools)   
   - [Links](#links)

### Configurar IP Fixo
  - Verificando nome da interface
```
#ifconfig -a
```
  - Definindo IP (exemplo para eth0)
```
#vi /etc/sysconfig/network-scripts/ifcfg-eth0
DEVICE=eth0
TYPE=Ethernet
IPADDR=192.168.1.198
NETMASK=255.255.255.0
GATEWAY=192.168.1.1
ONBOOT=yes
```	
 - Reiniciando a rede
```
#service network restart
```
ou
``` 
#/etc/init.d/network restart
```
### Definir DNS
 - Informe os servidores de DNS
``` 
#vi /etc/resolv.conf
nameserver 8.8.8.8
nameserver 8.8.4.4
```
 - Reiniciando a rede
```
#service network restart
```
ou
``` 
#/etc/init.d/network restart
```
### Atualizar Sistema
 - Execute a atualização do sistema
``` 
#yum update
#yum upgrade
```

### Instalar SSH
 - Instale o pacote OpenSSH
``` 
#yum install openssh-server
```
### Definir HOSTNAME
 - Verifique o nome do host
``` 
#hostname
```
 - Altere o nome do host
``` 
#vi /etc/sysconfig/network
NETWORKING=yes
HOSTNAME=novoHost
```
### Verificações
 - Verifique a memória disponível
``` 
#free
```
 - Verifique os processadores
``` 
#lscpu
```
 - Verifique os discos
``` 
#lsblk
```
 - Verifique seu IP
``` 
#ifconfig
```
### VMWare Tools
 - Instale os pré-requisitos das ferramentas VMWare:
``` 
#yum install faz o gcc kernel-devel kernel-headers glibc-headers perl net-tools
```
 - Acione a opção Install/Upgrade VMWare Tools na VM pelo vCenter ou vSphere para monter uma unidade na VM e em seguida:
``` 
#mkdir /mnt/cdrom
#mount /dev/cdrom /mnt/cdrom
#cp /mnt/cdrom/VMwareTools*.tar.gz /tmp
#cd /tmp
#tar xvfz VMwareTools * .tar.gz
#cd /tmp/vmware-tools-distrib
#./vmware-install.pl # add -d
```

### Links
- **Configurar IP fixo e DNS no CentOS 6.x**: https://wiki.hosthp.com.br/configurar-ip-fixo-e-dns-no-centos-6-x/
- **Como instalar ferramentas VMWare no CentOS 6 e CentOS 7 / RHEL**: https://serenity-networks.com/how-to-install-vmware-tools-on-centos-6-and-centos-7-rhel/
