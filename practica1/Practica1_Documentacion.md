#                   Antonio Martin Leon
###                  Practica 1 de SWAP

# Introduccion
Esta primera practica de la asignatura consiste en la preparación de nuestras maquinas virtuales para poder crear una granja web, usando Ubuntu Server.
# Apache + PHP + MySQL + Servicios SSH
Para la instalación de estas herramientas se pueden hacer de varias maneras, instarlo mediante comando una vez instalado Ubuntu Server, o bien, por la que yo he optado que instalar el *LAMP* durante la instalación de Ubuntu Server.
Además, he preferido instalar también *OpenSSH* para no tener que hacerlo por comandos.
![imagen](https://github.com/antonioml97/SWAP/blob/master/practica1/Imagenes/ConfiguracionLAMP.png)
# Prueba de Curl
Lo primero que voy a mostrar son mis 2 direcciones IP de cada maquia:
![image](https://github.com/antonioml97/SWAP/blob/master/practica1/Imagenes/Maquina1_IP.png)
![image](https://github.com/antonioml97/SWAP/blob/master/practica1/Imagenes/Maquina2IP.png)  

Lo siguiente que voy a hacer es comprobar *curl* y *apache* funciona, para ello he generado un archivo de prueba en la maquina 1, y usare *curl* en la maquina 2.
![image](https://github.com/antonioml97/SWAP/blob/master/practica1/Imagenes/PruebaCurl.png)
# Prueba de SSH
Por último, voy a probar la conectividad de ambas maquinas por *SSH* .
![image](https://github.com/antonioml97/SWAP/blob/master/practica1/Imagenes/SSH.png)
Lógicamente no deja crear la carpeta, por tanto sabemos que esta conectada de manera correcta.
