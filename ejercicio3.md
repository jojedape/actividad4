


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



