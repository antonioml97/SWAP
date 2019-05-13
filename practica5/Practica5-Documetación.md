#Práctica 5: Replicación de bases de datos MySQL
En esta práctica vamos a realizar una configuración de una base de datos sencila en nuestra granja web.

#Crear una BD e insertar datos
Comenzamos en la máquina 1 (cuya ip es 192.168.1.100), creando una base de datos desde mysql llamada contactos. Una vez seleccionada, creamos la tabla de datos que tendrá un nombre y un teléfono, y le insertamos una tupla.
![img](https://github.com/antonioml97/SWAP/blob/master/practica5/img/Crear_BD.png)

#Replicar una BD MySQL con mysqldump
Básicamente lo que vamos a realizar aquí es una clonación de nuestras bases de datos, para tener una copia de seguridad y posteorimente la trasnferiremos a nuestra máquina 2, es decir, nuestra maquina esclava.

Para ello vamos a realizar los siguientes pasos:
+ Bloquear la base de datos con el comando.
```
FLUSH TABLES WITH READ LOCK;
```
+ Usar el comando mysqldump para realizar la copia.
```
mysqldump contactos -u root -p > /tmp/contactos.sql
```
+ Desbloquar la base de datos.
```
UNLOCK TABLES;
```
![img](https://github.com/antonioml97/SWAP/blob/master/practica5/img/Imagen_2.png)

Posteorimente, vamos a copiar esta base de datos a nuestra segunda máquina. Hay que tener cuidado ya que en nuestra máquina 2 tenemos que crear nosotros primero la base de datos. Ahora para copiar nuestra base de datos usaremos la orden *scp*.
En este caso bastaría con hacer lo que esta reflejado en la siguiente imagen:
![img](https://github.com/antonioml97/SWAP/blob/master/practica5/img/Imagen_3.png)

#Replicación de BD mediante una configuración maestro-esclavo
La opción anterior funciona perfectamente, pero es algo que realiza un operador a mano. Sin embargo, MySQL tiene la opción de configurar el demonio para hacer
replicación de las BD sobre un esclavo a partir de los datos que almacena el maestro.

Una vez que ya tenemos clonadas las bases de datos en ambas máquinas, debemos de configurar el archivo de configuración en ambas máquinas,que en mi caso, se encuentra en el path */etc/mysql/mysql.conf.d/mysqld.cnf*
Los cambios a realizar son los siguientes:
+ Comentamos el parámetro bind-address que sirve para que escuche a un servidor.
  ```
  #bind-address 127.0.0.1
  ```
+ Le indicamos el archivo donde almacenar el log de errores.
  ```
  log_error = /var/log/mysql/error.log
  ```
+ Establecemos el identificador del servidor. (1 para la máquina 1, 2 para la máquina 2)
  ```
  server-id = 1
  ```
+ El registro binario contiene toda la información que está disponible en el registro de actualizaciones.
  ```
  log_bin = /var/log/mysql/bin.log
  ```
+ Guardamos el documento y reiniciamos el servicio:
```
/etc/init.d/mysql restart
```
En la siguiente imagen se muestra como ambas máquinas están bien.
![img](https://github.com/antonioml97/SWAP/blob/master/practica5/img/mysql_OK.png)

Por otro lado, tenemos que crear un usuario en la base de datos y realizar los siguientes comandos en la máquina maestro:
![img](https://github.com/antonioml97/SWAP/blob/master/practica5/img/Despues_Crear_Usuario.png)

En la imagen anterior se muestra la obtenemos los datos de la BD que vamos a replicar para posteriormente usarlos en la configuración del esclavo.

El siguiente paso es el siguiente, nos vamos a a máquina escalva y realizamos los siguientes comandos:
```
mysql> CHANGE MASTER TO MASTER_HOST='192.168.31.200',
      MASTER_USER='esclavo', MASTER_PASSWORD='esclavo',
      MASTER_LOG_FILE='mysql-bin.000001', MASTER_LOG_POS=501,
      MASTER_PORT=3306;
```
Por último, arrancamos el esclavo y ya está todo listo para que los demonios de MySQL de las dos máquinas repliquen automáticamente los datos que se
introduzcan/modifiquen/borren en el servidor maestro:
```
mysql> START SLAVE;
```
Una vez desbloquedas las tablas en la máquina maestro podemos usar la orden en la máquina esclavo *mysql> SHOW SLAVE STATUS\G* para comprobar que funciona correctamente, si todo esta bien "Seconds_Behind_Master” es distinto de “null”.
![img](https://github.com/antonioml97/SWAP/blob/master/practica5/img/Seconh.png)

Para acabar la documentación de ésta sesión voy a realizar una prueba de su correcto funcionamiento, que se reflejará en la siguiente imagen:
![img](https://github.com/antonioml97/SWAP/blob/master/practica5/img/Todo_OK.png)
