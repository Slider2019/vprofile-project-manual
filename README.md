# 🚀 DevOps VProfile Monolithic Project

# Introducción

## 🧱 VProfile Project - Configuración Local (Manual)

## 1.- 🎯 Objetivo del Proyecto

Este proyecto del curso de *"DevOps Beginners to Advanced with projects"* de **Imran Teli** tiene **dos propósitos principales**:

1.  **Establecer una línea base** para proyectos futuros:
    -   Despliegue de pilas de aplicaciones.
    -   Refactorización.
    -   Contenerización.
    -   Despliegue en clúster Kubernetes.
    -   Automatización.
 
2.  **Montar un laboratorio local** para R&D (Investigación y Desarrollo):
    -   Reproducción de entornos reales con múltiples servicios.
    -   Práctica segura sin afectar servidores productivos.
    -   Confianza en cambios e implementaciones.

## 2.- 🖥️ ¿Qué es una pila de aplicaciones web?

Una **pila** es un conjunto de servicios que trabajan en conjunto para entregar una aplicación web funcional.

En este proyecto, la aplicación es una **red social escrita en Java**.

----------

## 3.- 🧰 Herramientas necesarias

-   🧱 **Oracle VirtualBox**: Hipervisor.
-   📦 **Vagrant**: Automatización de la creación y configuración de VMs.
-   💻 **Git Bash**: CLI para ejecutar comandos y control de versiones.
-   📝 **Editor de texto**: Sublime, VSCode, Notepad++, ó con el que te sientas más a gusto.

----------

## 4.- 🔁 Problemas comunes y soluciones en éste proyecto

### Problemas:

-   Configurar manualmente pilas complejas es lento y propenso a errores.
-   No es **repetible**.
-   Puede haber temor a modificar servidores reales.

### Solución:

👉 Automatizar la configuración local con **Infrastructure as Code (IaC)**.

Esto lo hace:

-   Repetible ✅
-   Rápido ✅
-   Seguro ✅
-   Ideal para R&D y pruebas ✅

***NOTA:*** Ésta versión del proyecto no está automatizada. Sin embargo, se actualizará una versión futura con automatización completa de esta.

----------

## 5.- 🗺️ Arquitectura de la Aplicación

#### Pre Requisitos:
- JDK 17 ó 21
- Maven 3.9
- MySQL 8

#### Tecnologías usadas:
- Spring MVC
- Spring Security
- Spring Data JPA
- Maven
- JSP
- Tomcat
- MySQL
- Memcached
- Rabbitmq
- ElasticSearch

#### La pila consta de los siguientes servicios:
| Servicio | Rol |
|--|--|
| 🌀 **Nginx** | Web Server / Load Balancer |
| 🐱 **Tomcat**  | App Server para Java  |
| 🐇 **RabbitMQ** | Message Broker (Añadido como Dummy para practicar) |
| 🧠 **Memcached** | Sistema de cache para mejorar rendimiento de consultas a la BD |
| 🐬 **MySQL** | Base de datos relacional |


![ChatGPT Image 11 may 2025, 09_24_26 p m](https://github.com/user-attachments/assets/716145ab-74e2-4907-8c60-220a184a43bd)


----------

## 6.- 🔄 Flujo de Ejecución de la Aplicación

1.  🧑‍💻 El usuario ingresa la **IP del balanceador de carga (Nginx)** en su navegador.
2.  🌐 Nginx recibe la solicitud y la **redirecciona a Tomcat**.
3.  🧩 Tomcat procesa la solicitud y accede a los datos del usuario:
    -   Consulta primero a **Memcached**.
    -   Si no hay cache, va a **MySQL**.
    -   Una vez obtenidos los datos, se cachean para futuras peticiones.
4.  📨 RabbitMQ actúa como middleware (aunque no es funcional en este demo).
5.  🧾 El usuario ve la respuesta en su navegador.


----------

## 7.- 🏗️ Arquitectura de Automatización

```
Vagrantfile --> Vagrant CLI --> Oracle VirtualBox --> VMs individuales para cada servicio
```

Cada servicio corre en su propia VM automatizada por Vagrant:

-   VM1: Nginx
-   VM2: Tomcat
-   VM3: RabbitMQ
-   VM4: Memcached
-   VM5: MySQL

----------

## 8.- ⚙️ Pasos del Proyecto

1.  ✅ Configurar herramientas (Git Bash, Vagrant, VirtualBox, etc.)
2.  🔁 Clonar el código fuente del proyecto (que contiene el `Vagrantfile`)
3.  📦 Ejecutar `vagrant up` para crear y provisionar las máquinas virtuales.
4.  🔍 Validar conectividad entre VMs.
5.  🧪 Configurar los servicios en orden:
    -   MySQL
    -   Memcached
    -   RabbitMQ
    -   Tomcat
    -   Nginx
6.  🚀 Construir y desplegar la aplicación Java.
7.  🧪 Validar desde el navegador mediante la IP del balanceador de carga.

----------

## 9.- Profundizando en los pasos del proyecto

### 1.- 🛠️ Instalar los Pre Requisitos:

#### En entorno Windows

Instalar **Chocolatey** según las instrucciones dadas en el siguiente link:
https://chocolatey.org/docs/installation

Ejecutar los siguientes comandos ***(Actualizados a Mayo de 2025)*** como administrador en el Powershell (Abrir PowerShell como Administrador)

    choco install virtualbox --version=7.1.8 -y
    choco install vagrant --version=2.4.5 -y
    choco install git -y
    choco install corretto17jdk -y
    choco install maven -y
    choco install awscli -y
    choco install intellijidea-community -y
    choco install vscode -y
    choco install sublimetext3 -y

### 2.- 🏗️ Setup

Una vez instalados los Pre Requisitos, abrimos GitBash como administrador e instalamos un plugin adicional para Vagrant: `vagrant host-mannager`. 


💡 `vagrant-hostmanager`  es un plugin de Vagrant que actualiza automáticamente el archivo `/etc/hosts`  tanto en nuestra máquina local como en las máquinas virtuales, permitiendo que se comuniquen entre sí usando nombres de host en lugar de direcciones IP. Es ideal para entornos con múltiples VMs que necesitan resolverse por nombre.



### 3.- Configuración de las Máquinas Virtuales (VM)

1.  Clona el código fuente en VS Code ó descarga como ZIP, guarda en una carpeta y extrae su contenido.
	![asd122](https://github.com/user-attachments/assets/e269ddb6-9be9-4af9-aaf5-27459ca0ef17)

2.  Entra al directorio del repositorio (`cd`).
	![1](https://github.com/user-attachments/assets/9f5ab635-a59a-4bec-a576-19e74031a9b8)


3.  Entra al directorio `vagrant/Manual_provisioning` y escoge según tu plataforma (Windows, LINUX ó MAC).
    ![aaa111](https://github.com/user-attachments/assets/7c12073b-04a5-43cb-aad2-52819b0d76d6)


**Levantar las máquinas virtuales**

```bash
$ vagrant up
```

**NOTA:** Levantar todas las máquinas virtuales puede tomar bastante tiempo, dependiendo de varios factores.  
Si la configuración de las VM se detiene a mitad del proceso, ejecutar nuevamente el comando `vagrant up`.

**INFO:** Los nombres de host de todas las máquinas virtuales y las entradas del archivo `/etc/hosts` se actualizarán automáticamente.


### 4.- Configuración de la Máquina Virtual de la Base de Datos

1. Inicia sesión en la máquina virtual de base de datos:

```bash
$ vagrant ssh db01
```


2. Actualiza el sistema operativo con los últimos parches:

```bash
# dnf update -y
```

3. Configura el repositorio:

```bash
# dnf install epel-release -y
```

4. Instala el paquete de MariaDB:

```bash
# dnf install git mariadb-server -y
```

5. Inicia y habilita el servicio de MariaDB:

```bash
# systemctl start mariadb
# systemctl enable mariadb
```

6. Ejecuta el script de configuración segura de MySQL:

```bash
# mysql_secure_installation
```

**NOTA:** Establece la contraseña de root de la base de datos. En este caso, se usará `admin123` como contraseña.

    Set root password? [Y/n] Y
    New password:
    Re-enter new password:
    Password updated successfully!
    Reloading privilege tables..
    ... Success!
    
    By default, a MariaDB installation has an anonymous user, allowing anyone
    to log into MariaDB without having to have a user account created for
    them. This is intended only for testing, and to make the installation
    go a bit smoother. You should remove them before moving into a
    production environment.
    
    Remove anonymous users? [Y/n] Y
    ... Success!
    
    Normally, root should only be allowed to connect from 'localhost'. This
    ensures that someone cannot guess at the root password from the network.
    Disallow root login remotely? [Y/n] n
    ... skipping.
    
    By default, MariaDB comes with a database named 'test' that anyone can
    access. This is also intended only for testing, and should be removed
    before moving into a production environment.
    
    Remove test database and access to it? [Y/n] Y
    - Dropping test database...
    ... Success!
    - Removing privileges on test database...
    ... Success!
    
    Reloading the privilege tables will ensure that all changes made so far
    will take effect immediately.
    Reload privilege tables now? [Y/n] Y
    ... Success!

7. Configura el nombre de la base de datos y los usuarios:

```bash
# mysql -u root -padmin123
```

```sql
mysql> create database accounts;
mysql> grant all privileges on accounts.* TO 'admin'@'localhost' identified by 'admin123';
mysql> grant all privileges on accounts.* TO 'admin'@'%' identified by 'admin123';
mysql> FLUSH PRIVILEGES;
mysql> exit;
```

8. Descarga el código fuente e inicializa la base de datos:

```bash
# cd /tmp/
# git clone -b local https://github.com/hkhcoder/vprofile-project.git
# cd vprofile-project
# mysql -u root -padmin123 accounts < src/main/resources/db_backup.sql
# mysql -u root -padmin123 accounts
```

```sql
mysql> show tables;
mysql> exit;
```

9. Reinicia el servicio `mariadb-server`:

```bash
# systemctl restart mariadb
```

10. Inicia el firewall y permite el acceso al puerto 3306 para MariaDB:

```bash
# systemctl start firewalld
# systemctl enable firewalld
# firewall-cmd --get-active-zones
# firewall-cmd --zone=public --add-port=3306/tcp --permanent
# firewall-cmd --reload
# systemctl restart mariadb
```

### 5.- CONFIGURACIÓN DE MEMCACHE

1.  Inicia sesión en la máquina virtual de Memcache:
    

```bash
$ vagrant ssh mc01
```

2.  Verifica la entrada en el archivo de hosts. Si faltan entradas, actualízalo con la IP y los nombres de host:
    

```bash
# cat /etc/hosts
```

3.  Actualiza el sistema operativo con los últimos parches:
    

```bash
# dnf update -y
```

4.  Instala, inicia y habilita Memcached en el puerto 11211:
    

```bash
# sudo dnf install epel-release -y
# sudo dnf install memcached -y
# sudo systemctl start memcached
# sudo systemctl enable memcached
# sudo systemctl status memcached
# sed -i 's/127.0.0.1/0.0.0.0/g' /etc/sysconfig/memcached
# sudo systemctl restart memcached
```

5.  Inicia el firewall y permite el acceso al puerto 11211 para Memcache:
    

```bash
# systemctl start firewalld
# systemctl enable firewalld
# firewall-cmd --add-port=11211/tcp
# firewall-cmd --runtime-to-permanent
# firewall-cmd --add-port=11111/udp
# firewall-cmd --runtime-to-permanent
# sudo memcached -p 11211 -U 11111 -u memcached -d
```

### 6.- CONFIGURACIÓN DE RABBITMQ

1.  Inicia sesión en la máquina virtual de RabbitMQ:
    
```bash
$ vagrant ssh rmq01
```

2.  Verifica la entrada en el archivo de hosts. Si faltan entradas, actualízalo con la IP y los nombres de host:
    
```bash
# cat /etc/hosts
```

3.  Actualiza el sistema operativo con los últimos parches:
    
```bash
# dnf update -y
```

4.  Establece el repositorio EPEL:

```bash
# dnf install epel-release -y
```

5.  Instala las dependencias necesarias:

```bash
# sudo dnf install wget -y
# dnf -y install centos-release-rabbitmq-38
# dnf --enablerepo=centos-rabbitmq-38 -y install rabbitmq-server
# systemctl enable --now rabbitmq-server

```

6.  Configura el acceso de usuario `test` y asígnale privilegios de administrador:
    
```bash
# sudo sh -c 'echo "[{rabbit, [{loopback_users, []}]}]." > /etc/rabbitmq/rabbitmq.config'
# sudo rabbitmqctl add_user test test
# sudo rabbitmqctl set_user_tags test administrator
# rabbitmqctl set_permissions -p / test ".*" ".*" ".*"
# sudo systemctl restart rabbitmq-server
```

7.  Inicia el firewall y permite el acceso al puerto 5672 para RabbitMQ:
    
```bash
# sudo systemctl start firewalld
# sudo systemctl enable firewalld
# firewall-cmd --add-port=5672/tcp
# firewall-cmd --runtime-to-permanent
# sudo systemctl start rabbitmq-server
# sudo systemctl enable rabbitmq-server
# sudo systemctl status rabbitmq-server
```

### 7.- CONFIGURACIÓN DE TOMCAT

1.  Inicia sesión en la máquina virtual de Tomcat:
    
```bash
$ vagrant ssh app01
```

2.  Verifica la entrada en el archivo de hosts. Si faltan entradas, actualízalo con la IP y los nombres de host:
    
```bash
# cat /etc/hosts
```

3.  Actualiza el sistema operativo con los últimos parches:
    
```bash
# dnf update -y
```

4.  Establece el repositorio EPEL:
    
```bash
# dnf install epel-release -y
```

5.  Instala las dependencias necesarias (Java 17, Git, Wget):
    
```bash
# dnf -y install java-17-openjdk java-17-openjdk-devel
# dnf install git wget -y
```

6.  Cambia al directorio temporal:
    
```bash
# cd /tmp/
```

7.  Descarga y extrae el paquete de Tomcat:
    
```bash
# wget https://archive.apache.org/dist/tomcat/tomcat-10/v10.1.26/bin/apache-tomcat-10.1.26.tar.gz
# tar xzvf apache-tomcat-10.1.26.tar.gz
```

8.  Crea un usuario para Tomcat:
    
```bash
# useradd --home-dir /usr/local/tomcat --shell /sbin/nologin tomcat
```

9.  Copia los archivos extraídos al directorio del usuario Tomcat:
    
```bash
# cp -r /tmp/apache-tomcat-10.1.26/* /usr/local/tomcat/
```

10.  Cambia la propiedad del directorio a tomcat:
    
```bash
# chown -R tomcat.tomcat /usr/local/tomcat
```

11.  Crea un archivo de servicio para Tomcat en systemd:
   
```bash
# vi /etc/systemd/system/tomcat.service
```

🔧 Inserta el siguiente contenido:

```ini
[Unit]
Description=Tomcat
After=network.target

[Service]
User=tomcat
Group=tomcat
WorkingDirectory=/usr/local/tomcat
Environment=JAVA_HOME=/usr/lib/jvm/jre
Environment=CATALINA_PID=/var/tomcat/%i/run/tomcat.pid
Environment=CATALINA_HOME=/usr/local/tomcat
Environment=CATALINE_BASE=/usr/local/tomcat
ExecStart=/usr/local/tomcat/bin/catalina.sh run
ExecStop=/usr/local/tomcat/bin/shutdown.sh
RestartSec=10
Restart=always

[Install]
WantedBy=multi-user.target
```

12.  Recarga los archivos de configuración de systemd:
   
```bash
# systemctl daemon-reload
```

13.  Inicia y habilita el servicio de Tomcat:
    
```bash
# systemctl start tomcat
# systemctl enable tomcat
```

14.  Habilita el firewall y permite el acceso al puerto 8080:
    
```bash
# systemctl start firewalld
# systemctl enable firewalld
# firewall-cmd --get-active-zones
# firewall-cmd --zone=public --add-port=8080/tcp --permanent
# firewall-cmd --reload
```

### 8.- COMPILACIÓN Y DESPLIEGUE DEL CÓDIGO (app01)
👉 _Configuración de Maven, clonación del repositorio, compilación del proyecto y despliegue en Tomcat._

----------

#### 🔧 Configurar Maven

1.  Cambia al directorio temporal:
    
```bash
# cd /tmp/
```

2.  Descarga Maven 3.9.9:
    
```bash
# wget https://archive.apache.org/dist/maven/maven-3/3.9.9/binaries/apache-maven-3.9.9-bin.zip
```

3.  Extrae el paquete:
    
```bash
# unzip apache-maven-3.9.9-bin.zip
```

4.  Copia el contenido a un directorio en `/usr/local`:
    
```bash
# cp -r apache-maven-3.9.9 /usr/local/maven3.9
```

5.  Establece opciones de entorno para Maven:
    
```bash
# export MAVEN_OPTS="-Xmx512m"
```

----------

#### 📥 Descargar el código fuente

```bash
# git clone -b local https://github.com/hkhcoder/vprofile-project.git

```

----------

#### ⚙️ Actualizar configuración

1.  Entra al directorio del proyecto:
    
```bash
# cd vprofile-project
```

2.  Edita el archivo de configuración de la aplicación para agregar los detalles del backend (DB, MQ, Memcache, etc.):
    
```bash
# vim src/main/resources/application.properties
```

----------

#### 🔨 Compilar el código

Ejecuta Maven dentro del repositorio para construir el archivo `.war`:

```bash
# /usr/local/maven3.9/bin/mvn install
```

----------

#### 🚀 Desplegar el artefacto en Tomcat

1.  Detén el servicio Tomcat:
    
```bash
# systemctl stop tomcat
```

2.  Elimina la aplicación anterior si existe:
    
```bash
# rm -rf /usr/local/tomcat/webapps/ROOT*
```

3.  Copia el nuevo `.war` como `ROOT.war`:
    
```bash
# cp target/vprofile-v2.war /usr/local/tomcat/webapps/ROOT.war
```

4.  Ajusta los permisos del directorio `webapps`:
    
```bash
# chown tomcat.tomcat /usr/local/tomcat/webapps -R
```

5.  Inicia y reinicia Tomcat:
    
```bash
# systemctl start tomcat
# systemctl restart tomcat
```

----------

### 9.- CONFIGURACIÓN DE NGINX  

Inicia sesión en la máquina virtual de Nginx
    
```bash
$ vagrant ssh web01  
$ sudo -i  
```

Verifica la entrada de Hosts, si faltan entradas, actualízalas con la IP y los nombres de host

```bash
# cat /etc/hosts  
```

Actualiza el sistema operativo con los últimos parches

```bash
# apt update  
# apt upgrade  
```

Instala Nginx

```bash
# apt install nginx -y  
```

Crea el archivo de configuración de Nginx

```bash
# vi /etc/nginx/sites-available/vproapp  
```

Actualiza con el siguiente contenido

```nginx
upstream vproapp {
    server app01:8080;
}
server {
    listen 80;
    location / {
        proxy_pass http://vproapp;
    }
}
```

Elimina la configuración predeterminada de Nginx

```bash
# rm -rf /etc/nginx/sites-enabled/default  
```

Crea un enlace para activar el sitio web

```bash
# ln -s /etc/nginx/sites-available/vproapp /etc/nginx/sites-enabled/vproapp  
```

Reinicia Nginx

```bash
# systemctl restart nginx  
```

### 10.  🧪 Validar desde el navegador mediante la IP del balanceador de carga.

![asd](https://github.com/user-attachments/assets/f7d1108e-2765-49b0-b4bd-209b6653bc88)
