# Práctica 2
## Tarea 1
### Probar el funcionamiento de la copia de archivos por ssh
Para hacer una copia de un archivo mediante el comando **ssh** introduciremos la orden:
*tar czf -directorio | ssh equipodestino 'cat > ~/tar.tgz'*
En la siguiente imágen se puede ver un ejemplo de uso.
![img1](https://github.com/NonoK32/SWAP1718/blob/master/P2/copiassh.png)

## Tarea 2
### Clonado de una carpeta entre las dos máquinas
Para clonar una carpeta entre dos máquinas, la herramienta **Rsync** nos ofrece una opción tanto fiable, como eficiente.
Para hacer uso de ella realizaremos los siguientes pasos desde la maquina de respaldo:
*rsync -avz -e ssh ipmaquina1:/var/www/ /var/www/* 

Una vez introducida dicha orden, nos pedirá la contraseña del usuario, y tras unos breves segundo podremos comprobar como la carpeta seleccionada se ha clonado.

En la siguiente imágen podemos ver un ejemplo de su uso.
![img2](https://github.com/NonoK32/SWAP1718/blob/master/P2/rsyncmanual.png)

## Tarea 3
### Configuración de ssh para acceder sin que solicite contraseña
Para la realizacion de esta tercera tarea realizaremos los siguientes pasos.
Crearemos unas claves mediante  **ssh-keygen** con el siguiente comando:
*ssh-keygen -b 4096 -t rsa*
Esto dara como resultado la creación de un directorio llamado **.ssh** como se puede ver en la siguiente imágen.
![img2](https://github.com/NonoK32/SWAP1718/blob/master/P2/carpetacredenciales.png)

A continuación usaremos la orden: *ssh-copy-id maquina1* 
Una vez realizado con éxito el paso anterior, podremos usar ssh sin tener que introducir la contraseña para cada conexión.
En la imágen a continuación podemos ver la realización de estos pasos.
![img3](https://github.com/NonoK32/SWAP1718/blob/master/P2/copiacredenciales.png)

##Tarea 4
### Establecer  una  tarea  en  cron  que  se  ejecute  cada  hora  para  mantener actualizado el contenido del directorio /var/www entre las dos máquinas
Para realizar esta última tarea es necesario recurrir al demonio **cron** de linux, para ello realizamos lo siguiente.
Modificaremos el archivo */etc/crontab* de la siguiente manera:
![img4](https://github.com/NonoK32/SWAP1718/blob/master/P2/crontab.png)
En este caso en lugar de cada hora he decidido configurar el demonio para que realice las copias cada minuto (para no perder tiempo esperando para comprobar que efectivamente funciona).
Una vez guardados los cambios en el archivo *crontab*, podremos comprobar que realmente funciona como se ve en la siguiente imágen.
![img5](https://github.com/NonoK32/SWAP1718/blob/master/P2/ejecucioncron.png)



