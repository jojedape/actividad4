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
