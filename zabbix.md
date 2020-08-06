<p align="center"> 
<img src="https://user-images.githubusercontent.com/32847584/89578242-3c3a1980-d808-11ea-8910-a28ef3161ce6.png">
</p>
# Zabbix
Instalação e configuração do Zabbix

## Sumário
- [Zabbix](#zabbix)
  - [Sumário](#sumário)
   - [Download do pacote Zabbix](#download-do-pacote-zabbix)
   - [Instalação do banco de dados](#banco-de-dados)
   - [Configurando Frontend](#configurando-frontend)
   - [Instalando Zabbix Agent](#instalando-zabbix-agent)
   - [Finalizando a Instalação](#finalizando-instalação)     
   - [Links](#links)

### Download do Pacote Zabbix
  - Faça o download do pacote
   - Ubuntu 18.04  
```
#wget https://repo.zabbix.com/zabbix/4.0/ubuntu/pool/main/z/zabbix-release/zabbix-release_4.0-2+bionic_all.deb
#dpkg -i zabbix-release_4.0-2+bionic_all.deb
```
   - Ubuntu 14.04  
```
#wget https://repo.zabbix.com/zabbix/4.0/ubuntu/pool/main/z/zabbix-release/zabbix-release_4.0-2+trusty_all.deb
#dpkg -i zabbix-release_4.0-2+trusty_all.deb
```

  - Atualize os pacotes
```
#apt update
```	

### Banco de Dados
 - Instale o MySQL
``` 
#apt-get install mysql-server
```
 - Instale o pacote do Zabbix server com suporte ao banco de dados Mysql
```
#apt-get install zabbix-server-mysql
```
 - Logue no banco de dados com o comando abaixo, vai entrar na console do Mysql, vai pedir senha, digite somente enter. Por padrão a senha vem em branco por isso somente <Enter>
```
#mysql -u root -p enter
```
 - Na console do Mysql digite os comandos abaixo para criar o banco de dados com o nome zabbix e senha zabbix
```
#create database zabbix character set utf8 collate utf8_bin;
grant all privileges on zabbix.* to zabbix@localhost \
identified by ‘zabbix’;
quit;
```
 - Crie as tabelas na base de dados do zabbix
```
#cd /usr/share/doc/zabbix-server-mysql
#zcat create.sql.gz | mysql -uroot zabbix
```
 - Edite o arquivo de configuração do Zabbix Server
```
#vi /etc/zabbix/zabbix_server.conf
DBHost=localhost
DBName=zabbix
DBUser=zabbix
DBPassword=zabbix
StartPollers=20
StartPollersUnreachable=10
StartPingers=10
StartDiscoverers=10
StartVMwareCollectors=5
```

### Configurando Frontend
 - Instalando os pacotes do PHP, necessários para o Frontend do Zabbix
``` 
#apt-get install php7.2 php7.2-mysql php7.2-bcmath php7.2-gd php7.2-mbstring php7.2-xml php7.2-gettext php7.2-ldap
```
 - Edite o arquivo de configuração
``` 
#vi /etc/php/7.2/apache2/php.ini
memory_limit = 128MB
post_max_size = 16M
upload_max_filesize = 2M
max_execution_time = 300
max_input_time = 300
date.timezone = America/Recife
```
 - Instalando o pacote do Frontend do Zabbix
``` 
#apt-get install zabbix-frontend-php zabbix-apache-conf
```
 - Reiniciar o serviço do apache2
``` 
#service apache2 restart
```
 - Ativar o serviço do Zabbix Server para subir no boot
``` 
#systemctl enable zabbix-server
```
 - Iniciando o serviço do Zabbix Server
``` 
#service zabbix-server start
```
 - Conferindo os logs de atividade
``` 
#tail -f /var/log/zabbix/zabbix_server.log
```

### Instalando Zabbix Agent
 - Instale os pacotes para o funcionamento do Agent
``` 
#apt install zabbix-agent zabbix-get zabbix-sender
```
 - Pacotes para o SNMP e mibs padrões
``` 
#apt install snmp snmp-mibs-downloader
```

### Finalizando a Instalação
 - Agora abra o navegador no IP do servidor Zabbix
``` 
http://IPDOSERVIDOR/zabbix
```
 - Tela 1
<p align="center"> 
<img src="https://user-images.githubusercontent.com/32847584/89577196-b4074480-d806-11ea-9745-6553f46b6a84.png">
</p>
 - Tela 2
<p align="center"> 
<img src="https://user-images.githubusercontent.com/32847584/89577227-bcf81600-d806-11ea-8019-031050faba52.png">
</p>
 - Tela 3
<p align="center"> 
<img src="https://user-images.githubusercontent.com/32847584/89577279-d4370380-d806-11ea-9781-69326ec0153f.png">
</p>
 - Tela 4
<p align="center"> 
<img src="https://user-images.githubusercontent.com/32847584/89577309-e31db600-d806-11ea-8801-2ae3065efbe0.png">
</p>
 - Tela 5
<p align="center"> 
<img src="https://user-images.githubusercontent.com/32847584/89577333-eadd5a80-d806-11ea-93ed-3ea6eadaee53.png">
</p>
 - Tela 6
<p align="center"> 
<img src="https://user-images.githubusercontent.com/32847584/89577348-f2046880-d806-11ea-9517-bc1e736e4bce.png">
</p>
 - Após finalizar as configurações realize o login com usuário e senha padrão da instalação
	- Username: Admin
	- Password: zabbix
O login é case sensitive

 - Tela 7
<p align="center"> 
<img src="https://user-images.githubusercontent.com/32847584/89577375-f7fa4980-d806-11ea-9591-f021fabf0eb2.png">
</p>


### Links
- **Instalação do Zabbix 4.4 Ubuntu 18.04**: https://blog.nototi.com.br/instalacao-do-zabbix-4-4-ubuntu-18-04/
