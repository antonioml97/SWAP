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
