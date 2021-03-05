ACTIVIDAD 1
COMANDOS
-1. ¿Cómo sabemos si tenemos conexión a internet? 
El comando ping envía pequeños paquetes de datos al servidor  que le digamos en el comando y el servidor a su vez nos da una respuesta midiéndose el tiempo en responder. El servidor puede ser de nuestra red local o de la red pública
Para realizarlo escribimos ping y el nombre del servidor o la dirección IP

Al ejecutar el comando vemos que tenemos respuesta del servidor de la red pública, por lo que podemos asegurar que tenemos conexión a internet.
-2. ¿Cómo sabemos si nuestro servidor es accesible desde Internet?
El comando netsat detecta las conexiones de nuestro equipo tanto entrantes como salientes
Escribimos el comando seguido del nombre de dominio a consultar

Nos muestras todas las conexiones realizadas
-3. ¿Cómo sabemos a quién pertenece una dirección web (URL)? Pista: 
El comando dig realiza búsqueda en los registros de dns a través del nombre de dominio y devuelve la dirección ip

Efectivamente si introducimos la ip 142.250.184.163 nos lleva a la web de google

-4. ¿Cómo probamos que podemos acceder a un servidor? 
Con el comando curl podemos interactuar con cualquier sitio web y así comprobar que podemos accder a él.
Podemos lanzar la siguiente petición que se descargue la página web de google. 

Comprobamos que se ha descargado el código html. Y por lo tanto hemos accedido al servidor. Si le añadieramos al comando –output nombre del archivo nos descargaría el archivo.
-5. Qué otros comandos te han hecho falta? 
En principio no he tenido que usar más comando, pero para comprobar directorios y moverme por carpetas he utilizado ls y cd.

