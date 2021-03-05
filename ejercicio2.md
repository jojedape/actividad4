Requerimiento 1 y 2

1. Java 
2. Apache 
3. Tomcat 
4. openSSH 
5. MariaDB 



En primer lugar arrancamos la máquina virtual:


1. Java
Abrimos el terminal y tecleamos el comando java -version para ver que versión tenemos instalada. 
El sistema nos responde que no está instalada, así que procedemos a su instalación con el gestor de paquetes de ubuntu apt. Tecleamos el comando
 sudo apt-get install default-jdk
para instalar java.
Si volvemos a ejecutar java -version nos da la versión que acabamos de instalar

2. Apache
Para comprobar si está instalado tecleamos
 apache2 -version
y comprobamos que no está instalado
Procedemos a instalarlo con sudo apt install apache2.
Comprobamos que se ha instalado con el comando apache2 -version

Comprobamos que está activo con
sudo systemctl status apache2

Con el comando hostname -I nos da la dirección ip

Compromabos que se trata de una ip interna a la máquina virtual. Cambiamos la configuración de esta a modo bridge para que se conecte directamente a la red local.

Volvemos a preguntar por nuestra ip;  comprobamos que la diección ip de la máquina coincide con el servidor apache


Testeamos desde mi mac que nos podemos conectar a la máquina con un ping

por último hacemos la comprobación desde el navegador del mac

3. Tomcat
Para instalarlo tecleamos
 sudo apt install -y tomcat9 tomcat9-admin 
que corresponden al paquete principal y a las aplicaciones administrativas
Realizamos la comprobación conectandonos desde el navegador del mac al puerto 8080 de tomcat

4. openSSH
Para su instalación lo hacemos con el comando
sudo apt install -y ssh
Comprobamos que está instalado y activo con el comando 
	systemctl status ssh.service

Desde el terminal del mac realizamos una conexión con el siguiente comando:
ssh julio@192.168.1.130 -p 22

y entramos en la máquina:



5. MariaDB
	Para instalarlo tecleamos
	sudo apt install mariadb-server
y lo configuramos con el comando
sudo mysql_secure_installation

Nos sale un asistente que nos va preguntando si queremos cambiar la contraseña del superusuario,
si queremos quitar el usuario anónimo que viene por defecto, si queremos deshabilitar el usuario root en remoto, etc.

Comprobamos i el puerto 3306 (el puerto de mysql) está abierto para poder acceder desde el exterior con el comando
nc -zv

Como está cerrado lo abrimos con el comando
sudo ufw allow 3306/tcp

Ahora tenemos que entrar en el archivo de configuración de maria db para permitir el acceso desde remoto. Para ello editamos el archivo de configuración con el editor de ubuntu nano. 

Y editamos la línea bin-address y cambiamos la ip local por 0.0.0.0


Salvamos los cambiamos y salimos y reiniciamos el servicio con
sudo systemctl restart mariadb.service




