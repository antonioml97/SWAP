# Antonio Martín León
# Documentacion Practica 4-Seguridad

# Introducción
En esta práctica se va a trabajar los siguientes aspectos:
+ Instalar un certificado SSL para configurar el acceso HTTPS a los servidores.
+ Configurar las reglas del cortafuegos para proteger la granja web.

# Crear e instalar en la máquina 1 un certificado SSL autofirmado
## Generar e instalar un certificado autofirmado
Para generar un certificado SSL autofirmado en Ubuntu Server solo tenemos que activar el módulo SSL de Apache, generar los certificados y especificarle la ruta a los certificados en la configuración. Así pues, como root ejecutaremos:
```
a2enmod ssl
service apache2 restart
mkdir /etc/apache2/ssl
cd /etc/apache2/ssl
openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout apache.key -out apache.crt
```

Editamos el archivo de configuración del sitio default-ssl:
```
nano /etc/apache2/sites-available/default-ssl.conf
```
Y agregamos estas lineas debajo de donde pone SSLEngine on:
```
SSLCertificateFile /etc/apache2/ssl/apache.crt SSLCertificateKeyFile /etc/apache2/ssl/apache.key
```
Activamos el sitio default--ssl y reiniciamos apache:
```
a2ensite default-ssl
service apache2 reload
```
Una vez reiniciado Apache, accedemos al servidor web mediante el protocolo HTTPS , si estamos accediendo con un navegador web en la barra de dirección sale en rojo el https, ya que se trata de un certificado autofirmado.

Al entrar a la web nos aparecerá un mensaje avisando de que la web no es segura:
![img](https://github.com/antonioml97/SWAP/blob/master/practica4/img/Screenshot_2.png)

Ahora vamos a copiar el certificado a la otra maquina en produccíon,M2.
```
sudo a2enmod ssl
sudo rsync -avz -e ssh antonio@192.168.1.100:/etc/apache2/ssl /etc/apache2/
sudo rsync -avz --delete -e ssh antonio@192.168.1.100:/etc/apache2/sites-available/default-ssl.conf /etc/apache2/sites-available/default-ssl.conf
a2ensite default-ssl
service apache2 reload
service apache2 restart
```
![img](https://github.com/antonioml97/SWAP/blob/master/practica4/img/Copia_m1_m2.png)

Por último,también tenemos que configurar **NGINX** para que acepete las peticiones HTTPS, para ello es necesario pasarle los certificado yo he vuelto a usar la orden rsync, además hay que añadir lo siguiente al archivo de configuración:
![img](https://github.com/antonioml97/SWAP/blob/master/practica4/img/Nginx.png)

Con esto ya tendríamos nuestro baleanceador listo para usarse, en la siguiente imagen se ve su correcto funcionamiento:
![img](https://github.com/antonioml97/SWAP/blob/master/practica4/img/Ngix__ok.png)

# Configurar el cortafuegos
Un cortafuegos es un componente esencial que protege la granja web de accesos indebidos. Son dispositivos colocados entre subredes para realizar diferentes tareas
de manejo de paquetes. Actúa como el guardián de la puerta al sistema web, permitiendo el tráfico autorizado y denegando el resto.
## Usar la herramienta iptables
Primero, vamos a configurar una máquiuna de produccíon en mi caso M1 que tiene la IP 192.168.1.100. Para ello he elaborado este script:
```
# Eliminar todas las reglas
iptables -F
iptables -X
iptables -Z
iptables -t nat -F
# Política por defecto: denegar todo el tráfico
iptables -P INPUT DROP
iptables -P OUTPUT DROP
iptables -P FORWARD DROP
# Permitir cualquier acceso desde localhost (lo)
iptables -A INPUT -i lo -j ACCEPT
iptables -A OUTPUT -o lo -j ACCEPT
#  Abrir el puerto 22 para permitir el acceso por SSH
iptables -A INPUT -p tcp --dport 22 -j ACCEPT
iptables -A OUTPUT -p tcp --sport 22 -j ACCEPT
# Abrir los puertos HTTP (80) de servidor web
iptables -A INPUT -p tcp --dport 80 -j ACCEPT
iptables -A OUTPUT -p tcp --sport 80 -j ACCEPT
#  Abrir los puertos HTTPS (443) de servidor web
iptables -A INPUT -p tcp --dport 443 -j ACCEPT
iptables -A OUTPUT -p tcp --sport 443 -j ACCEPT
````

Con esto ya tendríamos nuestra M1 configurada, la siguiente imagen muestra la M1 sin denegando todo los servicios:
![img](https://github.com/antonioml97/SWAP/blob/master/practica4/img/Prueba_tras_limpiar_iptables.png)

Y esto después de aplicar el script:
![img](https://github.com/antonioml97/SWAP/blob/master/practica4/img/Tras_script.png)

Lo ultimo seria editar el fichero /etc/rc.local para que se haga cada vez que se reincia el sistema
![img](https://github.com/antonioml97/SWAP/blob/master/practica4/img/IPTables_Script.png)
