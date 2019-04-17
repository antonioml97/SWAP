#         Antonio Martin Leon
##        SWAP Práctica 3-Balanceo de carga

# Introducción
Esta práctica 3 de esta asignatura consiste en realizar un balanceo de carga con los dos servidores que tenemos ya creados, y configuraremos dos balanceadores distinto siendo ambos por turnos. Un detalle a tener en cuenta en esta practica es que estos servidores no pueden tener algun servicio que escuche por el puerto 80 que es el que estamos usando con los servidores de producción.

# Balanceador nginx
Para instalar este balenceador esta sencillo como realizar este comando:
*sudo apt-get intall nginx*

Una vez instalado hay que configurarlo editando el archivo que se encuentra en /etc/nginx/conf.d/default.conf, quedando de la siguiente manera:


&nbsp;
![imagen](https://github.com/antonioml97/SWAP/blob/master/practica3/img/Archivo_config_ngax.png)

Con esto ya tendriamos nuestro balencador listo, por tanto, ahora las peticiones se realizan a el que tiene la IP 192.168.1.103.
Un ejemplo de su funcionamiento se refleja en esta imagen:



&nbsp;
![imagen](https://github.com/antonioml97/SWAP/blob/master/practica3/img/Funcionado_curl.png)

# Balanceador haproxy
En este caso tambien basta con hacer este sencillo comando:
*sudo apt-get install haproxy*

Una vez instalado en el equipo hay que  ditando el archivo que se encuentra en /etc/haproxy/haproxy.cfg, quedando esto:


&nbsp;
![imagen](https://github.com/antonioml97/SWAP/blob/master/practica3/img/HAPROXY_CONFIGURADO.png)

Y de nuevo en la siguiente imagen se vuelve a ver su correcto funcionamiento en este caso usando la IP 192.168.1.105:


&nbsp;
![imagen](https://github.com/antonioml97/SWAP/blob/master/practica3/img/Funcionando_haproxy.png)

# Estresando la granja web
Por último, en esta sección vamos a sobrecargar nuestra granja web con el uso de benchmark , habiendo varias opciones yo he optado por usar Apache Benchmark.

Vamos a realizar 2 pruebas usando en cada una un baleanceador distinto.
-Caso nginx:


&nbsp;
![imagen](https://github.com/antonioml97/SWAP/blob/master/practica3/img/Bechamach_nginx.png)

-Caso haproxy:
&nbsp;
![imagen](https://github.com/antonioml97/SWAP/blob/master/practica3/img/Benmachk_haproxy.png)
