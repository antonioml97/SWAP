#Tema 4
##Buscar información sobre precio y características de balanceadores hardware específicos. Compara las prestaciones que ofrecen unos y otros
        Precio	Rendimiento	Puertos Eth	Conex.simultaneas capa4	Hot-swap?
LM-X3 	4.000$     	3.4Gbps	   8          	8,600,000	            N/A

LM-3400	7.000$	    3.4Gbps	   8	          8,600,000	            N/A

LM-X15	9.800$	    15Gbps	  16            35,000,000            SÍ

LM-8000	30.000$	    20Gbps  	0	            75,800,000	          SÍ

LM-8020	40.000$   	30Gbps	  0            	75,800,000	          SÍ

##Instala y configura en una máquina virtual el balanceador ZenLoadBalancer.
Nos descargamos la ISO desde https://sourceforge.net/projects/zenloadbalancer/files/latest/download, lo instalamos
y seguimos un procedimiento parecido al de la tercera práctica, para asi poder entrar desde otra maquina y conseguir
balancear la carga.

##Buscar información sobre los métodos de balanceo que implementan los dispositivos recogidos en el ejercicio 4.2
SDN Adaptive, Round Robin, Weighted Round Robin, Menos conexión, Conexión menos ponderada,Adaptativo basado en el agente
Failover encadenado (ponderación fija), Source-IP Hash, Conmutación de contenido de Capa 7, Equilibrio global de carga del servidor (GSLB)
Dirección de tráfico basada en el grupo AD

##Probar las diferentes maneras de redirección HTTP. ¿Cuál es adecuada y cuál no lo es para hacer balanceo de carga global? ¿Por qué?
La 301 movera la pagina a otra URL nueva permanentemente y la 302 lo hara temporalmente por lo que la anterior
URL seguira siendo valida.

##Buscar información sobre los bloques de IP para los distintos países o continentes.
Implementar en JavaScript o PHP la detección de la zona desde donde se conecta un usuario.
En esta pagina web se encuentra los bloques de IP para distintos paises -https://www.countryipblocks.net/country_selection.php

##Buscar información sobre métodos y herramientas para implementar GSLB
Primero hay que crear una VPN para que los dos servidores se puedan comunicar de forma segura.
Luego configuramos lo típico para que haya balancceo entre ambos servidores.
