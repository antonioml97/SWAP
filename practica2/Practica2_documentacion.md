#         Antonio Martin Leon
##        SWAP Práctica 2-Sincronizar archivos

# Introducción
Esta práctica 2 de esta asignatura consiste en realizar la sincronización de archivos usando la orden rsync, creando una clave que compartirán nuestras máquinas y luego una configuración en el crontab.  
*El nombre de las máquinas es distinto a las practica anterior porque me causó problemas y tuve que repetirla.*


# Herramienta Rsync
En mi caso tenía ya la herramienta *rsync* instalada, por tanto, solo tenía que usar la siguiente orden *rsync -avz -e ssh 192.168.1.100:/var/www/ /var/www/* quedando de la siguiente manera:
![imagen](https://github.com/antonioml97/SWAP/blob/master/practica2/Imagenes/rsync.png)

*No pide la contraseña porque yo ya realice el paso siguiente, pero si no la pediría.*

# Acceso sin contraseña
Este procedimiento consiste en configurar rysnc para acceder sin necesidad de introducir la contraseña manualmente, es decir, configurar ssh para poder acceder sin contraseña para ellos he usado la herramienta *ssh-keygen*, para ello he realizado lo siguiente:

![imagen](https://github.com/antonioml97/SWAP/blob/master/practica2/Imagenes/Crear_clave.png)

# Programar tarea Crontab
Ahora vamos a configurar el demonio *crontab*, para ello basta con añadir una línea a su fichero de configuracion quedando de la siguiente manera:
![imagen](https://github.com/antonioml97/SWAP/blob/master/practica2/Imagenes/Editar_CronTab.png)

Con esto ya estaría configurado para que la carpeta /var/www/ se actualize 1 vez por minuto, en el guión se indica 1 hora pero yo por utilidad para comprobar su correcto funcionamiento he optado por darle el tiempo mencionado anteriormente.
