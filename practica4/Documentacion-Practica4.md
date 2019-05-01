# Antonio Martín León
# Documentacion Practica 4-Seguridad

# Introducción
En esta práctica se va a trabajar los siguientes aspectos:
+ Instalar un certificado SSL para configurar el acceso HTTPS a los servidores.
+ Configurar las reglas del cortafuegos para proteger la granja web.

# Crear e instalar en la máquina 1 un certificado SSL autofirmado
## Generar e instalar un certificado autofirmado
Para generar un certificado SSL autofirmado en Ubuntu Server solo tenemos que activar el módulo SSL de Apache, generar los certificados y especificarle la ruta a los certificados en la configuración. Así pues, como root ejecutaremos:


  a2enmod ssl
  service apache2 restart
  mkdir /etc/apache2/ssl
  cd /etc/apache2/ssl
  openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout apache.key -out apache.crt




a
