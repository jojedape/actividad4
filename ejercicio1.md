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

