# Antonio Martín León
# Documentación de AMAZON EC2

# INTRODUCCIÓN
En esta documentación se va a indicar qué es Amazon EC2, para qué se usa y finalmente su funcionamiento.
Básicamente, si lo queremos es crear una página web de cara al público, es necesario un servidor que como ya hemos visto en esta asignatura, nosotros o bien quien quiera crearla, tenga que estar configurando el servidor, y mantenimiento entre otras cosas.

La pregunta aquí es, ¿es necesario todo esto para montar una simple página web? Lógicamente no es necesario, pues muchas empresas tienen ya implementado esto de cara al público, por supuesto, por un precio acorde a lo que requieras. Una de estas empresas es la empresa de Seattle, **AMAZON**.  Esta empresa nos permitirá tener un servidor a nuestra total disposición sin necesidad de tener que preocuparnos por el mantenimiento, hardware u otras cuestiones del mismo servidor. Además, nos podemos conectar con SSH sin ningún tipo de problemas.

# CREAR CUENTA
Para empezar con esto será necesario crea una cuenta para poder empezar a usar nuestro servicio en Amazon Web Server, o abreviado **AWS**.
Para crear la cuenta será tan fácil como darle al botón de crear cuenta  y rellenar unas series de formularios.
![img](https://github.com/antonioml97/SWAP/blob/master/Trabajo/img/Trabajo_Crea.png)
Cabe destacar 2 cosas:
+ Nos pedirá una tarjeta de crédito, aunque no se hará ningún cargo si no superas el paquete básico.
+ Nos realizarán una llamada y tendremos que marcar los números que nos aparecen en pantalla conforme vamos avanzando en los formularios.


&nbsp;
Una vez seguidos estos pasos y habiendo confirmado un mensaje que llegará al correo que hayamos indicado, nos saldrá todo ya listo y una ventana como la de la siguiente imagen:
![img](https://github.com/antonioml97/SWAP/blob/master/Trabajo/img/Imagen_2.png)

Una vez aquí, antes de continuar necesitamos crear un usuario de tipo root, para ello buscamos aquí la sección **IAM**:
![img](https://github.com/antonioml97/SWAP/blob/master/Trabajo/img/Imagen%203.png)
![img](https://github.com/antonioml97/SWAP/blob/master/Trabajo/img/Imagen_4.png)
Una vez que le hemos puesto un nombre, lo siguiente es crear un grupo para poder administrar los permisos. Bastaría con seleccionar lo mostrado en la imagen, y por último añadir el usuario a este grupo ya creado.
![img](https://github.com/antonioml97/SWAP/blob/master/Trabajo/img/imagen_5.png)
![img](https://github.com/antonioml97/SWAP/blob/master/Trabajo/img/Imagen_6.png)
![img](https://github.com/antonioml97/SWAP/blob/master/Trabajo/img/Imagen_7.png)
![img](https://github.com/antonioml97/SWAP/blob/master/Trabajo/img/Imagen_8.png)

&nbsp;
# ELEGIR SISTEMA OPERATIVO
Lo primero que tenemos que hacer es buscar en la consola *EC2*, una vez hecho esto habrá que darle a Instances-->Launch Instance
![img](https://github.com/antonioml97/SWAP/blob/master/Trabajo/img/Imagen_9.png)
Una vez aquí saldrán los distintos sistemas operativos, por comodidad mía y ya que es con lo que hemos trabajado en clase he optado por instalar Ubuntu Server 16.04. ![img](https://github.com/antonioml97/SWAP/blob/master/Trabajo/img/Imagen_10.png)
Una vez instalado se quedaría así: ![img](https://github.com/antonioml97/SWAP/blob/master/Trabajo/img/Imagen_11.png)
En el proceso me pide crear una keypair y descargar un archivo de extension .pem

# CONECTARSE AL SERVIDOR
Con SSH nos podríamos conectar a nuestro servidor, para lo que necesitaremos utilizar si trabajamos en Windows, que es mi caso, su **Subsistema de Linux** que básicamente consiste en una consola que nos permite usar los comandos de Windows. Aunque hay otras opciones, como máquinas virtuales con Ubuntu y la herramienta *PuTTy* entre otras.
Para conectarse al servidor necesitaremos el archivo con extensión .pem creado anteriormente, bastaría con realizar lo siguiente:
![img](https://github.com/antonioml97/SWAP/blob/master/Trabajo/img/Imagen_12.png)
Cabe destacar que para poder hacer esto he tenido que usar la orden *cp* y poner el archivo en esa carpeta para que no de ningún tipo de error.
Una vez terminado este proceso, habrá que instalar Apache y MySQL  y ya tendríamos nuestro servidor operativo.
![img](https://github.com/antonioml97/SWAP/blob/master/Trabajo/img/Imagen_13.png)


&nbsp;
Es posible que pueda dar otro tipo de errores a la hora de usar SSH, HTTP, etc…
Por eso he creado las siguientes reglas ![img](https://github.com/antonioml97/SWAP/blob/master/Trabajo/img/Imagen_14.png)
