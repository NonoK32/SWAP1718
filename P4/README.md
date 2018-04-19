# PRÁCTICA 4
## Tarea 1: Crear e instalar en la máquina 1 un certificado SSL autofirmado para configurar el acceso HTTPS a los servidores. Una vez configurada la máquina 1, se debe copiar al resto de máquinas servidoras y  al balanceador de carga. Se debe configurar nginx adecuadamente para aceptar y balancear correctamente tanto el tráfico HTTP como el HTTPS. 

Para generar un certificado SSL realizaremos los pasos que podemos ver en la siguiente imágen:

Una vez hecho esto modificaremos el archivo */etc/apache2/sites-available/default-ssl.conf* para que quede de la siguiente manera:

Finalmete activamos el sitio defualt-ssl y reiniciamos el servicio de apache

![img1](https://github.com/NonoK32/SWAP1718/blob/master/P4/Captura%20de%20pantalla%20(134).png)

```bash
a2ensite default-ssl

service apache2 reload
```
Ahora, ese mismo certificado y la key, deben copiarse al balanceador y a cada uno de los servidores de la granja web.
En cada servidor web repetiremos los pasos descritos anteriormente,y nos llevaremos los certificados a */etc/apache2/ssl*, ya que este directorio no es accesible para los clientes.
Además, deberemos de modificar el archivo de configuración del balanceador(en este caso nginx) para que quede así:

![img2](https://github.com/NonoK32/SWAP1718/blob/master/P4/Captura%20de%20pantalla%20(138).png)

Una vez todo quede configurado, podremos comprobar desde otra máquina como efectivamente podemos hacer peticiones https. En la siguiente imágen podemos ver un ejemplo:

![img3](https://github.com/NonoK32/SWAP1718/blob/master/P4/Captura%20de%20pantalla%20(139).png)


## TAREA 2: Configurar las reglas del cortafuegos con IPTABLES para asegurar el acceso a uno de los servidores web, permitiendo el acceso por los puertos de HTTP y HTTPS a dicho servidor. Esta configuración se hará en una de las máquinas servidoras finales (p.ej. en la máquina 1), y se debe poner en un script con las reglas del cortafuegosque se ejecute en el arranque del sistema(según  la versión de Linux, se llevará a cabo de una forma u otra).

Para realizar esta tarea crearemos un script, que se ejecute durante el arranque de la máquina, el contenido básico sera el siguiente:

![img4](https://github.com/NonoK32/SWAP1718/blob/master/P4/Captura%20de%20pantalla%20(137).png)

Esta configuración de IPtables en concreto, abre los puertos http y https (80 y 443), y cualquier conexión desde localhost. En mi caso adicionalmente a lo requerido en el ejercicio,
he decido bloquear cualquier petición al puerto 22 (ssh), que no provenga de la dirección de otra de mis máquinas, para asi dar más "seguridad" al servidor.
Para hacer que este script se ejecute en el inicio de la máquina tenemos varias opciones:
### Opción 1

Añadimos nuestro script a */etc/init.d/* 

```bash
mv miScript.sh /etc/init.d/ 

chmod +x /etc/init.d/miScript.sh
```
Si esta opción que es la mas "clásica", no funcionase podriamos probar la siguiente opción

### Opción 2

Hacemos los pasos de la Opción 1, y además lo siguiente:
```bash
ln -s /etc/init.d/miScript.sh /etc/rc.d/
```

### Opción 3
Como tercera opción, podemos hacer que el demonio cron se encargue de que se ejecute el script añadiendo al crontab la siguiente linea:

```bash
#crontab -e 
@reboot /home/user/miScript.sh
```

Para comprobar que las reglas firewall funcionan correctamente, en la defensa de la práctica, se mostrará como es imposible acceder mediante ssh a dicha máquina, a no se que se haga desde la que tiene la dirección que esta excenta de dicha regla.