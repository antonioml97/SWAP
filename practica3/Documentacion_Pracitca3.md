#         Antonio Martin Leon
##        SWAP Práctica 3-Balanceo de carga

# Introducción
Esta práctica 3 de esta asignatura consiste en realizar un balanceo de carga con los dos servidores que tenemos ya creados, y configuraremos dos balanceadores distinto siendo ambos por turnos.

# Balanceador nginx
Para instalar este balenceador esta sencillo como realizar este comando:
*sudo apt-get intall nginx*

Una vez instalado hay que configurarlo editando el archivo que se encuentra en /etc/nginx/conf.d/default.conf, quedando de la siguiente manera:


&nbsp;
![imagen](https://github.com/antonioml97/SWAP/blob/master/practica3/img/Archivo_config_ngax.png)

Con esto ya tendriamos nuestro balencador listo, por tanto, ahora las peticiones se realizan a el que tiene la IP 192.168.1.103.
Un ejemplo de su funcionamiento se refleja en esta imagen:



&nbsp;
![imagen](https://github.com/antonioml97/SWAP/blob/master/practica3/img/Funcionado_curl.pngg)
