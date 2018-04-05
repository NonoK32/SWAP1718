# Práctica 3
## Tarea 1
### Configurar una máquina e instalar el nginx como balanceador de carga
Para realizar esta tarea primeramente introduciremos las siguientes ordenes:
```bash
sudo apt-get update && sudo apt-get dist-upgrade && sudo apt-get autoremove

sudo apt-get install nginx

sudo systemctl start nginx

```

Hecho esto tendremos NGINX instalado en nuestra máquina. A continuación deberemos realizar las siguientes tareas:

**Matar el proceso de Apache (en caso de que este activo)**
**Configurar NGINX**

Para desactivar apache:

```bash
service apache2 stop
```

En la siguiente imágen se puede comprobar como efectivamente apache está desactivado.


![img1](https://github.com/NonoK32/SWAP1718/blob/master/P3/servicios.png)

Ahora pasamos a configurar los ficheros:

*/etc/nginx/conf.d/default.conf*

*/etc/nginx/nginx.conf*

Para que queden de la siguiente manera, como se puede ver en las siguientes imagenes:

![img2](https://github.com/NonoK32/SWAP1718/blob/master/P3/conf1Nginx.png)

![img3](https://github.com/NonoK32/SWAP1718/blob/master/P3/confNGINX2.png)

Una vez hecho esto iniciamos el servicio de NGINX, con la siguiente instrucción:

```bash
service nginx start
```

**IMPORTANTE**:Tanto NGINX, como HAPROXY, y POUND usaran la dirección *192.168.56.160*

![img4](https://github.com/NonoK32/SWAP1718/blob/master/P3/ifconfigNGINX.png)

**IMPORTANTE**:El contenido de los html de los servidores finales es el siguiente:

![img5](https://github.com/NonoK32/SWAP1718/blob/master/P3/htmls.png)

Una vez realizado esto, podemos lanzar peticiones desde una cuarta máquina y el balanceador se encargara de repartir la carga entre los servidores. En el caso de NGINX una de las máquinas a recibido en la configuración el doble de peso, como se puede ver en la imagen2.
Podemos ver su funcionamiento en la siguiente imágen.

![img6](https://github.com/NonoK32/SWAP1718/blob/master/P3/peticionesNGINX.png)

## Tarea 2
### Configurar una máquina e instalar el haproxy como balanceador de carga

El primer paso será instalar haproxy, lo haremos introduciento la siguiente orden:

```bash
sudo apt-get install haproxy
```

Una vez instalado, y de nuevo **habiendo acabado el proceso de apache** pasaremos a configurarlo.
Modificaremos el archivo */etc/haproxy/haproxy.cfg* para que quede de la siguiente manera:

![img7](https://github.com/NonoK32/SWAP1718/blob/master/P3/confHAPROXY.png)

![img8](https://github.com/NonoK32/SWAP1718/blob/master/P3/confHAPROXY2.png)

Y ya podriamos lanzar peticiones. En las siguientes capturas podemos ver su funcionamiento:

![img9](https://github.com/NonoK32/SWAP1718/blob/master/P3/peticionesHAPROXY.png)

## Tarea 3
### Someter a la granja web a una alta carga, generada con la herramienta Apache Benchmark, teniendo primero nginx y despues haproxy

Para realizar esta tarea usaremos la siguiente orden:

```bash
ab -n 1000 -c 10 http://192.168.2.160/index.html
```

Puesto que los balanceadores usan la misma dirección.

#### NGINX

![img10](https://github.com/NonoK32/SWAP1718/blob/master/P3/abNGINX.png)
![img11](https://github.com/NonoK32/SWAP1718/blob/master/P3/abNGINX2.png)
![img12](https://github.com/NonoK32/SWAP1718/blob/master/P3/abNGINX3.png)

#### HAPROXY

![img13](https://github.com/NonoK32/SWAP1718/blob/master/P3/abHAPROXY.png)
![img14](https://github.com/NonoK32/SWAP1718/blob/master/P3/abHAPROXY2.png)
![img15](https://github.com/NonoK32/SWAP1718/blob/master/P3/abHAPROXY3.png)

Como se puede ver, en este caso, el tiempo de respuesta por petición de HAPROXY es ligeramente mejor que el de NGINX

## Tarea EXTRA
### Configurar POUND como balanceador web

Primero instalamos POUND:

```bash
sudo apt-get install pound
```
Y de nuevo, **matamos el servicio apache** y configuramos POUND, para ello modificaremos los siguientes archivos:

*etc/pound/pound.cfg*

![img16](https://github.com/NonoK32/SWAP1718/blob/master/P3/confPOUND.png)


*etc/default/pound*

![img18](https://github.com/NonoK32/SWAP1718/blob/master/P3/defaultPOUND.png)

Y ya podriamos lanzar peticiones para comprobar que funciona.

![img19](https://github.com/NonoK32/SWAP1718/blob/master/P3/peticionesPOUND.png)

Además le realizaremos la prueba de carga, de igual manera que a NGINX y HAPROXY.

![img20](https://github.com/NonoK32/SWAP1718/blob/master/P3/abPOUND.png)
![img21](https://github.com/NonoK32/SWAP1718/blob/master/P3/abPOUND2.png)
![img21](https://github.com/NonoK32/SWAP1718/blob/master/P3/abPOUND3.png)

Podemos comprobar que el tiempo medio por petición es peor que NGINX y HAPROXY.


