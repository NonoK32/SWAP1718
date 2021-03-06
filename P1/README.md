# Práctica 1
## Configuración del entorno de virtualización
Debido a que voy a usar VirtualBox en lugar de VM Player, a las máquinas
virtuales que voy a usar debo añadirles una interfaz de red extra, la host-only,
como se puede ver en la imagen, las maquinas tendran dos interfaces de red,
la interfaz NAT para que tengan acceso a internet, y la interfaz host-only, para
que puedan "verse" entre ellas.

## Configuración de las interfaces de red
Ahora arrancaremos una maquina virtual con Ubuntu server y accederemos a /etc/network/interfaces
y estableceremos la siguiente configuracion

![img1](https://github.com/NonoK32/SWAP1718/blob/master/P1/ConfiguracionRED.png)

Ahora apagaremos la maquina habiendo guardado dicha configuracion de red.
La clonamos, para tener dos maquinas, alterando eso si, la ip estatica de una de ellas para que sean diferentes.

![img3](https://github.com/NonoK32/SWAP1718/blob/master/P1/Interfaces2maquinas.png)

## Prueba de funcionamiento de interfaces
Una vez arrancadas las dos maquinas, probaremos a hacer ping a www.google.es desde ambas, asi como a hacer ping entre ellas

![img2](https://github.com/NonoK32/SWAP1718/blob/master/P1/ping2maquinas.png)

Como se puede ver en la foto, las interfaces de red funcionan correctamente

Habiendo comprobado esto realizamos las tareas requeridas por la practica

## Tarea 1
### Conexión ssh remota desde las maquinas
Para efectuar una conexion ssh desde una maquina a otra, bastara con usar el comando **ssh** de la siguiente forma
*ssh NombreUsuario@DirIP*
Se nos pedira que si queremos guardar la clave, para que no nos la vuelva a pedir, una vez respondida la peticion bastara con introducir la contraseña
y la conexion quedara efectuada

![img4](https://github.com/NonoK32/SWAP1718/blob/master/P1/conexionssh.png)

## Tarea 2
### Conexion mediante curl
Basta con usar el comando **curl** de la siguiente manera:

*Curl http://IPdestino/hola.html*

Creamos un fichero html de prueba con el siguiente contenido

![img5](https://github.com/NonoK32/SWAP1718/blob/master/P1/ContenidoHTML.png)

Y realizamos la conexion curl

![img6](https://github.com/NonoK32/SWAP1718/blob/master/P1/Conexion%20curl.png)
