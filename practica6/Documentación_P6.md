# Documentación Practica 6
El objetivo principal de esta práctica es configurar un servidor NFS para exportar un espacio en disco a los servidores finales (que actuarán como clientes-NFS).

# Configurar el servidor NFS
Para ello he creado una máquina que he llamado SWAP-NFS, y con una IP que es 192.168.1.110. Una vez creada esta máquina hay que realizar lo siguiente:
+ Instalamos las herramientas necesarias
```
sudo apt-get install nfs-kernel-server nfs-common rpcbind
````
+ Después, creamos la carpeta que vamos a compartir y cambiamos el propietario y permisos de esa carpeta:
````
mkdir /dat/compartida
sudo chown nobody:nogroup /dat/compartida/
sudo chmod -R 777 /dat/compartida/
`````
+ Para dar permiso de acceso a las máquinas clientes, debemos añadir las IP correspondientes en el archivo de configuración */etc/exports*


![img](1)
+ Finalmente, debemos reiniciar el servicio:
````
sudo service nfs-kernel-server restart
````
# Configurar los clientes
En nuestras máquinas de trabajo (M1 y M2), debemos instalar los paquetes necesarios y crear el punto de montaje. Hay que realizar los siguientes comandos:
````
sudo apt-get install nfs-common rpcbind
cd /home/antonio
mkdir carpetacliente
chmod -R 777 carpetacliente
````
Ya estamos en el punto en el que podemos montar la carpeta
````
sudo mount 192.168.1.110:/dat/compartida carpetacliente
````
Una vez hecho esto ya tendriamos todo configurado de manera que lo que hagamos en esa carpeta afectara a M1,M2 y la maquina de NFS.

![img](2)

Por último, es necesario editar el archivo */etc/fstab* para que se monte esta carpeta cada vez que se inicien las máquinas.


![img](3)

Con esta modificación ya estaría todo acabado.
