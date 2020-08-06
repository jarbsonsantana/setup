# CentOS 6x
Configurações iniciais para sistemas linux CentOS 6x

# Sumário
- [CentOS 6x](#centos-6x)
- [Sumário](#sumário)
  - [1. Configurar-IP-Fixo](#1-configurar-ip-fixo)
  - [14. Links](#14-links)

## 1. Configurar-IP-Fixo
a. Verificando nome da interface
```
#ifconfig -a
```
b. Definindo IP (exemplo para eth0)
```
#vi /etc/sysconfig/network-scripts/ifcfg-eth0
DEVICE=eth0
TYPE=Ethernet
IPADDR=192.168.1.198
NETMASK=255.255.255.0
GATEWAY=192.168.1.1
ONBOOT=yes
```	
c. Reiniciando a rede
```
#service network restart
```
ou
``` 
#/etc/init.d/network restart
```
## 2. Definir-DNS
a. Informe os servidores de DNS
``` 
#vi /etc/resolv.conf
nameserver 8.8.8.8
nameserver 8.8.4.4
```
b. Reiniciando a rede
```
#service network restart
```
ou
``` 
#/etc/init.d/network restart
```

## 14. Links
- **Markdown - primeiros passos**: https://help.github.com/articles/basic-writing-and-formatting-syntax/
- **Escrevendo no GitHub**: https://help.github.com/categories/writing-on-github/
- **Formatação Markdown**: https://beta.observablehq.com/@jaynel/markdown-summary