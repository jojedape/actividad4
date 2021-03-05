


ACTIVIDAD 3 DESPLIEGUE DE APLICACIONES WEB







Diego Mompó									    24-02-21
Julio Ojeda
Sara Dozzi
Silvia Cañas

Introducción	3
Crear Base de Datos y Tabla	3
Crear recurso de BBDD para la aplicación	3
Añadir Resource	3
Comprobación de la librería	4
Por último, listamos el directorio lib, de tomcat, donde aparece el conector:	4
Insertar datos desde la app del Tomcat	5
Configuración FTP en Ubuntu.	6
Instalación FTP	6
Instalación de Filezilla para probar la conexión al servidor  FTP.	8
Configuración de usuarios y permisos para FTP en Ubuntu.	10
Prueba del servidor FTP desde cmd de Windows 10 (anfitrión) y Filezilla	13
Acceso al servidor FTP desde la aplicación web en Tomcat.	17
Pruebas desde el servidor de Tomcat al servicio FTP	19
Configuración del servidor CDN en Ubuntu	21


Introducción
	En esta actividad vamos a la configurar FTP, CDN y Base de datos para una 	aplicación. Lo primero que tenemos que hacer antes de configurar todo es 	desplegar la aplicación en el servidor. Para ello Cogemos el archivo .war que nos 	han facilitado y lo metemos en la siguiente imagen

	Esta imagen se encuentra en el gestor de aplicaciones de tomcat.
Crear Base de Datos y Tabla
	La creación de la base de datos se va a encargar Diego y entre los tres vamos a 	configurarlo. Entre todos hemos decidido que la base de datos se hará en MariaDB. 	A través del comando sudo MariaDB accedemos a MariaDB.

	Primero creamos la base de datos y la seleccionamos. Para ello escribimos 	CREATE DATABASE NombreBaseDeDatos. En nuestro caso la base de datos se 	llamará Actividad 3. Con USE seleccionamos la base datos.

	
	Para crear la tabla escribimos  CREATE TABLE (nombre de la tabla) (nombre de 	las columnas). En nuestro caso, el comando quedaría de la siguiente manera:

Crear recurso de BBDD para la aplicación
	La configuración la realizamos mediante el fichero "context.xml" contenido en la 	carpeta Tomcat9. Esta configuración nos dará la ventaja de poder realizar cambios 	sin 	reiniciar completamente el servidor, y permitirá que la aplicación web 	sea 	portable, que en anteriores versiones no se aplicaba.
Añadir Resource
	 Añadimos "resource" en context.xml como se muestra:



	Importante, descargar el driver correspondiente para mysql en la siguiente página:	https://mvnrepository.com/artifact/mysql/mysql-connector-java

	Nosotros hemos descargado la siguiente:
	mysql-connector-java-8.0.23.jar

	El siguiente paso es mover dicho conector desde la consola de linux a la carpeta 	correspondiente (/usr/share/tomcat9/lib) en este caso.

	El comando utilizado es el siguiente, que lo desplaza desde el directorio de 	"Descargas":
	sudo mv mysql-connector-java-8.0.21.jar /../usr/share/tomcat9/lib

Comprobación de la librería
Por último, listamos el directorio lib, de tomcat, donde aparece el conector:



Insertar datos desde la app del Tomcat


	Comprobamos que en la base de datos aparecen los usuarios insertados en 	MariaDb

Accedemos a la BBDD con usuario:
		-sudo sudo mysql -u (usuario) -p     >>>>ejecutamos y nos pide la 				contraseña del usuario que está accediendo.
Entramos a la bbbdd "actividad3"
		-use actividad3
Realizamos la consulta:
		select * from PERSONAS;

	Salimos ejecutando el comando "exit".




Configuración FTP en Ubuntu.

Instalación FTP 

Primero instalamos el paquete con el gestor apt en ubuntu:




Comprobamos que se ha instalado correctamente: 
-systemctl Status vsftp



Se habilitan los siguientes puertos: 20,21,22,990
20:  que se utiliza para las transferencias de ficheros, sin autenticar, y sin cifrar.
21: puerto 21, utilizado para conectarse de forma remota a un servidor y autenticarse en él, sin cifrado.
990: Se realiza una negociación SSL antes de que se envíe cualquier comando FTP, cifrado.


Procedemos a editar el fichero con el editor de linux, nano el archivo /etc/vsftpd.conf y a activar los siguientes parametros:

#anonymus_enable=YES,   habilitamos el usuario anonimo que por defecto está desabilidado.





Añadimos el parametro anon_root: "ruta de la carpeta Tomcat." como se muestra en la siguiente imagen, que corresponde al usuario anónimo y su ruta de acceso:



Instalación de Filezilla para probar la conexión al servidor  FTP.



Procedemos a descargar filezilla en un equipo cliente Windows 10, 








Probamos el acceso con el usuario anónimo y ver que finalmente se conecta y puede visualizar la carpeta etc/tomcat9.







Configuración de usuarios y permisos para FTP en Ubuntu.

Creamos usuarios administrador y registrado




El parámetro siguiente permite que los usuarios del equipo local (en este caso ubuntu 20.04) se conecten mediante ftp, el cual está ya habilitado en el fichero vsffpd.conf.




Ahora abrimos el fichero vsffpd.conf y añadimos el siguiente parámetro: 
para que los usuarios que hemos creado abran la ruta por defecto /etc/tomcat9. 

local_root="/etc/tomcat9".





Guardamos los cambios.

Creamos los usuarios con shell asignada, para poder iniciar sesión con la conexión FTP.
Los usuarios son: registrado, y administrador.
Se les configura a su vez el directorio /ftp-usuarios, para que se inicie en dicha ubicación.
El parametro -g corresponde al grupo "ftp" creado anteriormente.



Se le crea a cada usuario una contraseña con el mismo nombre:
Ejemplo para crear la contraseña del "administrador".

 

Permisos de la carpeta "tomcat9"



Los permisos que tiene actualmente son: 
Propietario: lectura, escritura y ejecucion (todos)
Grupo "Tomcat": lectura y ejecución: r – x
Otros usuarios: lectura y ejecución. r – x


Al usuario administrador, tal como se pide en la actividad, y tal como tiene ahora los permisos (r-w), habría que asignarle el permiso de escritura, dentro de "otros usuarios" de la carpeta tomcat.
Añadimos el usuario administrador al grupo "tomcat" para que tenga todos los permisos.



Comprobamos que se han aplicado los permisos de escritura a subcarpetas de tomcat9, de grupo:



Al realizar dichos cambios, el usuario puede escribir y por tanto se crea un directorio en /home que pertenece al usuario, y puede modificarlos, en dicho directorio, que como norma general debe ser solo de lectura de ficheros, pero añadiremos un parámetro para resolverlo.
Primero saltará un error desde filezilla:



Se soluciona añadiendo un parámetro al fichero vsftpd.conf, 

allow_writeable_chroot=YES

Ahora vemos que podemos acceder con "administrador" y escribir sobre un fichero, ya que le hemos dado tal permiso.

También des comentamos el siguiente parámetro:



Reiniciamos el servicio en consola: 
-systemctl restart vsftpd.

Probamos a crear un nuevo archivo en el directorio listado del usuario administrador, para probar su nuevo permiso de escritura:


Lo llamamos "patata".




-Ahora probamos con el usuario "registrado" a conectar con filecilla, y a descargar ficheros (permiso que tiene asignado, entendido como lectura y ejecución)

En la imagen el usuario "registrado" se descarga el fichero "hola.txt".



-Comprobamos, que efectivamente NO puede subir ficheros:




Prueba del servidor FTP desde cmd de Windows 10 (anfitrión) y Filezilla

Probamos acceso al servidor FTP desde cmd.
Comandos FTP:



Hacemos conexión con el usuario anonymous y nos da un error:



Tendremos que comentar el siguiente parámetro para que nos deje listar el contenido de la carpeta especificada de acceso:



Volvemos a introducir usuario:anonymous, y contraseña (la del servidor local) y nos deja listar el contenido del directorio asignado en el fichero vsftpd.conf, (hola.txt).




Ahora nos logueamos con el usuario "administrador", contraseña del usuario creado en el servidor de ubuntu "administrador". Como vimos, ya tiene permisos de escritura y subida de ficheros.



Por último, accedemos con el usuario creado "registrado", contraseña "registrado".
Este solo tiene permisos de lectura en nuestro "ubuntu-server".



Recordamos, que para especificar un acceso a carpeta debemos especificarlo en el fichero vsftpd.conf, en nuestro caso para el usuario predeterminado anonymous, y para los usuarios locales creados (administrador y registrado).



Cerramos ftp en cmd, con "close" y después "quit".




NOTA: con fillezilla ya hemos probado lo que cada usuario puede hacer según los permisos que tiene, en el punto anterior.


Acceso al servidor FTP desde la aplicación web en Tomcat.

Proceso de enjaulado de los usuarios, se añaden los siguientes parámetros teniendo en cuenta que los usuarios anónimo, administrador y registrado tengan acceso con sus correspondientes permisos.




Creamos el fichero userlist : sudo nano/etc/userlist y lo editamos con los usuarios locales y añadimos el parámetro correspondiente en el fichero vsftpd: userlist_file=/ruta de acceso.










-Fichero vsftpd.userlist donde guardamos los usuarios.



reiniciamos el servicio con : systemctl restart vsftpd.


Utilizaremos la carpeta ftp-usuarios creada, con varios ficheros, para acceder desde tomcat al servidor ftp y realizar la subida y descarga de ficheros.
Añadimos  el grupo de tomcat, al que pertenece administrador a la carpeta /ftp-usuarios y le concedemos permisos de escritura posteriormente.
El usuario "registrado" queda en "otros usuarios" de linux. Con permisos de lectura y ejecución.




Listamos para comprobar que el grupo tomcat aparece en el directorio ftp-usuarios y sus subcarpetas y ficheros



Ahora damos todos los permisos para acceder a la carpeta ftp-usuarios. Estos son root y administrador.



Pruebas desde el servidor de Tomcat al servicio FTP


Contenido de la carpeta que hemos creado para las pruebas, "ftp-usuarios":





Primero probamos a subir un fichero y editarlo con el usuario "administrador" a quien corresponden dichos permisos.
Subimos un fichero llamado "prueba" y clickamos en put.
Nos muestra el fichero en la tabla del directorio /ftp-usuarios.
En la tabla inferior se muestra el contenido del directorio configurado de acceso: /ftp-usuarios.

Aparece seleccionado a la dcha. de examinar. Seleccionamos put, para subirlo y nos aparecerá en la tabla inferior.



Ahora accedemos con el usuario "registrado" que sólo puede leer ficheros y descargarlos.
Introducimos "hola.txt" y nos muestra el contenido.



Contenido del fichero "hola.txt" el cual corresponde a lectura y descarga.




Configuración del servidor CDN en Ubuntu



Creamos el directorio que va a contener los archivos dentro de la carpeta /var/www con el comando:
sudo mkdir CDN

Para evitar problemas de permisos cambiamos la propiedad de la carpeta al usuario de apache www.data
sudo chown -R www-data /var/www/html/CDN
Y le damos permiso de escritura y de lectura al resto de usuarios


Editamos el archivo context.xml de tomcat y creamos una variable de entorno que dirija a la ruta donde tenemos los recursos



