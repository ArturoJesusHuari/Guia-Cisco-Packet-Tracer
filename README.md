<h1>Script de comandos de packet tracer</h1>
<h2>Enrutamiento VLAN</h2>
<p>Las redes de área local virtuales o más conocidas como VLAN, es una tecnología de red que permite crear redes lógicas independientes dentro de la misma red física. El objetivo de usar VLAN en un entorno doméstico o profesional, es para segmentar adecuadamente la red y usar cada subred de una forma diferente.</p>
<h3>Caracteristicas</h3>
<ul>
  <li>Las VLAN permiten dividir la red en grupos con una agrupación o estructura jerárquica lógica en lugar de una física.</li>
  <li>Los miembros de una VLAN pueden compartir recursos como si estuvieran conectados a la misma LAN.</li>
  <li>Las VLAN utilizan puentes y conmutadores, entonces los broadcast son más eficientes porque se dirigen sólo a personas en la VLAN y no a todos los conectados.</li>
</ul>
<h3>Ventajas</h3>
<ul>
  <li>Reducción de costos</li>
  <li>Agregar fácilmente estaciones de trabajo a la LAN</li>
  <li>Cambio rápido de configuración de la LAN</li>
  <li>Controlar el tráfico de red</li>
  <li>Mejorar la seguridad</li>
  <li>Escalable</li>
</ul>
<h3>Tipos de puertos</h3>
<h4>Puertos de acceso</h4>
<p>Son aquellos a los que se conectan directamente los equipos terminales.</p>
<h4>Puertos troncales</h4>
<p>Son enlaces capaces de transportar el tráfico de más de una VLAN y se suelen utilizar para interconectar dos switches o un switch/router. Puede ser un enlace físico o estar conformado por varios, en aquí la trama deberá transportar datos etiquetados.</p>
<h3>Configuración de VLAN sin enlaces troncales</h3>
<p align="center">
  <image src="/src/VLAN.png" alt="VLAN en el simulador Packet Tracer">
</p>
<h4>Configuracion de switch</h4>
<p>Acceso al modo de administrador <br>
  <pre><code>Switch> enable</code></pre>
  Accede al Modo de configuración global <br>
  <pre><code>Switch#configure terminal</code></pre>
  Cambia el nombre del dispositivo <br>
  <pre><code>Switch(config)#hostname SW1</code></pre>
  Se crea la VLAN 10 <br>
  <pre><code>SW1(config)#vlan 10</code></pre>
  Se asigna un nombre a la VLAN<br>
  <pre><code>SW1(config-vlan)#name VLAN10</code></pre> 
  Salir, para terminar la configuración de la VLAN<br>
  <pre><code>SW1(config-vlan)#exit</code></pre>
  Selecionar los puertos que se asignaran a la VLAN<br>
  <pre><code>SW1(config)#interface range fa0/10-15</code></pre> 
  Las interfaces cambia al modo de acceso permanente. Luego,  se asignan los puertos a la VLAN anteriormente creada y se termina la configuracion de los puertos. <br>
  <pre><code>SW1(config-if-range)#switchport mode access
SW1(config-if-range)#switchport access vlan 10
SW1(config-if-range)#exit</code></pre>
<em>De igual forma se crearan cuantas VLANs se necesiten.</em>
</p>
<h3>Configuración de VLAN con enlaces troncales</h3>
<p align="center">
  <image src="/src/VLANt.png" alt="VLAN con enlaces troncales">
</p>
<h4>Configuracion de switch</h4>
<p>Acceso al modo de administrador <br>
  <pre><code>Switch> enable</code></pre>
  Accede al Modo de configuración global <br>
  <pre><code>Switch#configure terminal</code></pre>
  Cambia el nombre del dispositivo <br>
  <pre><code>Switch(config)#hostname SW1</code></pre>
  Se crea la VLAN 10 <br>
  <pre><code>SW1(config)#vlan 10</code></pre>
  Se asigna un nombre a la VLAN<br>
  <pre><code>SW1(config-vlan)#name VLAN10</code></pre> 
  Salir, para terminar la configuración de la VLAN<br>
  <pre><code>SW1(config-vlan)#exit</code></pre>
  Selecionar los puertos que se asignaran a la VLAN<br>
  <pre><code>SW1(config)#interface range fa0/10-15</code></pre> 
  Las interfaces cambia al modo de acceso permanente. Luego,  se asignan los puertos a la VLAN anteriormente creada y se termina la configuracion de los puertos. <br>
  <pre><code>SW1(config-if-range)#switchport mode access
SW1(config-if-range)#switchport access vlan 10
SW1(config-if-range)#exit</code></pre>
<em>De igual forma se crearan cuantas VLANs se necesiten.</em>
</p>
<h4>Configuracion de router</h4>
<p>Acceso al modo de administrador <br>
  <pre><code>Router>enable</code></pre>
  Accede al Modo de configuración global <br>
  <pre><code>Router#configure terminal</code></pre>
  Se selecciona el puerto conectado al switch y se activa <br>
  <pre><code>Router(config)#interface fa 0/0
Router(config-if)#no shut down
Router(config-if)#exit</code></pre>
Se crean las subinterfaces con <code>interface fa 0/0.</code> y el número de la VLAN.
<pre><code>Router(config)#interface fa 0/0.10</code></pre>
Se ejecuta el comando <code>encapsulation dot1q</code> más el numero de la VLAN. Es el protocolo que permite que el router tenga enlace troncal.
<pre><code>Router(config-subif)#encapsulation dot1Q 10</code></pre>
Se asigna una direccion IP en cada subinterfaz.
<pre><code>Router(config-subif)#ip address 192.168.1.10 255.255.255.0
Router(config-subif)#exit</code></pre>
<em>De igual forma se habilitara el protocolo dot1Q para cada VLAN creada en el switch.</em><br>
Se guarda la configuración del router.
<pre><code>Router#copy run start</code></pre>
 </p>
<h2>Enrutamiento entre VLAN con Switches de Capa 3</h2>
Un Switch capa 3 es un switch y un router al mismo tiempo: puede considerarse un router con múltiples puertos Ethernet y con función de conmutación. El Switch capa 3 permite la conmutación de paquetes inspeccionando sus direcciones IP y sus direcciones MAC.
<h3>Configuración para comunicacion inter-VLAN usando switch de capa 3</h3>
<p align="center">
  <image src="/src/SWCapa3.png" alt="Red con switch de capa 3">
</p>
<h4>Configuracion de los switch 2960-24TT</h4>
<p>Acceso al modo de administrador <br>
  <pre><code>Switch> enable</code></pre>
  Accede al Modo de configuración global <br>
  <pre><code>Switch#configure terminal</code></pre>
  Cambia el nombre del dispositivo <br>
  <pre><code>Switch(config)#hostname SW1</code></pre>
  Se crea la VLAN 10 <br>
  <pre><code>SW1(config)#vlan 10</code></pre>
  Se asigna un nombre a la VLAN<br>
  <pre><code>SW1(config-vlan)#name VLAN10</code></pre> 
  Salir, para terminar la configuración de la VLAN<br>
  <pre><code>SW1(config-vlan)#exit</code></pre> 
  <em>De igual forma se crearan cuantas VLANs se necesiten en los demás switch.</em><br>
  Luego, asignar direcciones IP en caso se requiera. En este ejemplo existe una VLAN 90 para la gestión en los 3 switchs.
  Se selecciona la VLAN previamente creada, y con el comando <code>ip address</code> se asigna la dirección IP que le corresponda<br>
  <pre><code>SW1(config)#int vlan 90
SW1(config-if)#ip add 192.168.90.10 255.255.255.0
SW1(config-if)#exit</code></pre>
Después identificar los puertos de enlace troncal para cada uno de los switch. La configuración para cada puerto, ya sea Fast Ethernet o Gigabit Ethernet. <br>
Se selecciona el puerto a configurar con el comando <code>interface</code><br>
<pre><code>SW1(config)#int f0/10</code></pre>
El comando <code>switchport mode trunk</code> configura la interfaz en modo de enlace troncal permanente.
<pre><code>SW1(config-if)#sw mode trunk</code></pre>
El comando <code>switchport trunk native vlan</code> sólo se utiliza con la encapsulación dot1q e identifica que VLAN será nativa.
<pre><code>SW1(config-if)#switchport trunk native vlan 1</code></pre>
Se utiliza el comando <code>switchport trunk allowed vlan</code> para especificar la lista de VLAN que se permiten en el enlace troncal.
<pre><code>SW1(config-if)#switchport trunk allowed vlan 10,20,90,1
SW1(config-if)#exit</code></pre>
<em>De igual forma se configuran los enlaces troncales para cada switch.</em><br>
El siguiente paso es configurar los puertos que serán asignado a cada VLAN en cada Switch.
Selecionar los puertos que se asignaran a la VLAN<br>
<pre><code>SW1(config)#interface range fa0/10-15</code></pre> 
Las interfaces cambia al modo de acceso permanente. Luego,  se asignan los puertos a la VLAN. <br>
<pre><code>SW1(config-if-range)#switchport mode access
SW1(config-if-range)#switchport access vlan 10
SW1(config-if-range)#exit</code></pre>
<em>De igual forma para los demás puertos de las VLANs.</em>
<h4>Configuracion del switch de capa 3</h4>
Primero se configura el puerto que funcionara como enlace troncal. <br>
Acceso al modo de administrador <br>
<pre><code>Switch> enable</code></pre>
Accede al Modo de configuración global <br>
<pre><code>Switch#configure terminal</code></pre>
Cambia el nombre del dispositivo. <br>
<pre><code>Switch(config)#hostname Switch_Core</code></pre>
El switch cumplira la función de enrutamiento. <br>
<pre><code>Switch_Core(config)#ip routing</code></pre>
Se selecciona el puerto de enlace troncal.<br>
<pre><code>Switch_Core(config)#interface g0/1</code></pre>
El comando <code>switchport trunk native vlan</code> sólo se utiliza con la encapsulación dot1q e identifica que VLAN será nativa.<br>
<pre><code>Switch_Core(config-if)#switchport trunk native vlan 1</code></pre>
 El comando <code>encapsulation dot1q</code> es el protocolo que permite que el switch de capa 3 tenga enlace troncal.<br>
<pre><code>Switch_Core(config-if)#switchport trunk encapsulation dot1q</code></pre>
La interfaz cambia al modo de enlace troncal permanente. <br>
<pre><code>Switch_Core(config-if)#switchport mode trunk
Switch_Core(config-if)#exit</code></pre>
Luego, se crean las vlan existentes para el switch de capa 3.<br>
Se crea la VLAN 10 <br>
<pre><code>Switch_Core(config)#vlan 10</code></pre>
Se asigna un nombre a la VLAN<br>
<pre><code>Switch_Core(config-vlan)#name VLAN10</code></pre> 
Salir, para terminar la configuración de la VLAN<br>
<pre><code>Switch_Core(config-vlan)#exit</code></pre> 
<em>De igual forma para las demás VLAN.</em><br>
Despues asignar las respectivas direcciones IP, para cada interface de VLAN. <br>
Seleccionar la interface de VLAN.
<pre><code>Switch_Core(config)#int vlan 10</code></pre> 
Asignar su dirección IP
<pre><code>Switch_Core(config-if)#ip add 192.168.10.1 255.255.255.0
Switch_Core(config-if)#exit</code></pre> 
Finalmente, encender el puerto que funciona como enlace troncal y terminar la configuración.
<pre><code>Switch_Core(config-if)#no shutdown
Switch_Core(config-if)#end</code></pre>
<h2>WLAN</h2>
<p>La WLAN está formada por dispositivos que se conectan en un espacio geográfico reducido mediante ondas de radiofrecuencia. Este tipo de conexión permite que los usuarios tengan mayor movilidad en el espacio que están interconectados, asimismo, se mantiene un mejor orden ya que no hay necesidad del uso de cables. </p>
<h3>Configuración de router inalambrico</h3>
Para configurar el router, se necesita una PC que este conectada a este.
<p align="center">
  <image src="/src/W1.png" alt="Dispositivos ingresados">
</p>
Configurar el IP del PC. 
<p align="center">
  <image src="/src/W2.png" alt="Dispositivos ingresados">
</p>
Verificar conectividad 
<p align="center">
  <image src="/src/W3.png" alt="Dispositivos ingresados">
</p>
Ingresar al navegador: Web Browser, e ingresar en la barra de dirección, la IP del router.
<p align="center">
  <image src="/src/W4.png" alt="Dispositivos ingresados">
</p>
Ingresar con el Usuario: admin y Contraseña: admin
<p align="center">
  <image src="/src/W5.png" alt="Dispositivos ingresados">
</p>
<p align="center">
  <image src="/src/W6.png" alt="Dispositivos ingresados">
</p>
Ingresamos a la pestaña Wireless
<p align="center">
  <image src="/src/W7.png" alt="Dispositivos ingresados">
</p>
Cambiamos Default por FIS_UNCP
<p align="center">
  <image src="/src/W8.png" alt="Dispositivos ingresados">
</p>
<p align="center">
  <image src="/src/W9.png" alt="Dispositivos ingresados">
</p>
Agregamos 3 dispositivos inalámbricos
<p align="center">
  <image src="/src/W10.png" alt="Dispositivos ingresados">
</p>
<h3>Configuracion de dispositivos inalambricos</h3>
<h4>Laptop</h4>
Conectar la antena inalámbrica
<p align="center">
  <image src="/src/W11.png" alt="Dispositivos ingresados">
</p>
Conectamos los usuarios al dispositivo Wireless Router
<p align="center">
  <image src="/src/W12.png" alt="Dispositivos ingresados">
</p>
<p align="center">
  <image src="/src/W13.png" alt="Dispositivos ingresados">
</p>
Dispositivo conectado
<p align="center">
  <image src="/src/W14.png" alt="Dispositivo conectado">
</p>
<h4>Smartphone</h4>
<p align="center">
  <image src="/src/W15.png" alt="Smartphone">
</p>
<h4>Tablet</h4>
<p align="center">
  <image src="/src/W16.png" alt="Tablet">
</p>
<h4>Red final</h4>
<p align="center">
  <image src="/src/W17.png" alt="Red final">
</p>
<h2>Seguridad LAN</h2>
<h3>Configuración de la seguridad</h3>
<p align="center">
  <image src="/src/SL.png" alt="Seguridad LAN">
</p>
Configurar las IP de las PC
<p align="center">
  <image src="/src/SL2.png" alt="Seguridad LAN">
</p>
<h4>Configuración del switch</h4>
Acceso al modo de administrador <br>
<pre><code>Switch> enable</code></pre>
Accede al Modo de configuración global <br>
<pre><code>Switch#configure terminal</code></pre>
Se selecciona la interface que se desea configurar. <br>
<pre><code>Switch(config)#interface fa0/1</code></pre>
Se ingresa al modo acceso. <br>
<pre><code>Switch(config-if)#switchport mode access</code></pre>
Activa la seguridad del puerto. <br>
<pre><code>Switch(config-if)#switchport port-security</code></pre>
El número de dispositivos que se pueden conectar por este puerto, es de 1. <br>
<pre><code>Switch(config-if)#switchport port-security maximum 1</code></pre>
Se asigna la dirección mac del dispositivo que conectaremos al puerto. <br>
<pre><code>Switch(config-if)#switchport port-security mac-address sticky</code></pre>
En caso de una violacion de seguridad, el puerto se deshabilita. <br>
<pre><code>Switch(config-if)#switchport port-security violation shutdown
Switch(config-if)#exit</code></pre>
El puerto es estatico. 
<p align="center">
  <image src="/src/SL3.png" alt="Seguridad LAN">
</p>
Prueba de "PC malisiosa".
<p align="center">
  <image src="/src/SL4.png" alt="Seguridad LAN">
</p>
<h2>SSH</h2>
Secure Shell (SSH) es un protocolo seguro. Proporciona una conexión de administración segura (encriptada) a un dispositivo remoto. SSH reemplaza a las conexiones telnet para las conexiones de administración.
<h3>Configuracion SSH</h3>
<p align="center">
  <image src="/src/SSH.png" alt="Seguridad LAN">
</p>
<h4>Configuración de router</h4>
Acceso al modo de administrador <br>
<pre><code>Router> enable</code></pre>
Accede al Modo de configuración global <br>
<pre><code>Router#configure terminal</code></pre>
Se selecciona la interface que se desea configurar. <br>
<pre><code>Switch(config)#interface fa0/1</code></pre>
Se asigna la direccion IP. <br>
<pre><code>Router(config-if)#ip address 192.168.1.2 255.255.255.0</code></pre>
Se enciende el puerto <br>
<pre><code>Router(config-if)#no shutdown
Router(config-if)#exit</code></pre>
El comando service password-encryption aplica un cifrado débil a todas las contraseñas sin cifrar. El comando enable secret usa un fuerte algoritmo MD5 para cifrar.<br>
<pre><code>Router(config)#service password-encryption
Router(config)#ip domain-name cisco.com</code></pre>
Se asigna un nombre para el router <br>
<pre><code>Router(config)#hostname R1</code></pre>
Para crear una clave de encriptación. Genera las claves RSA con un tamaño de 1024 bits <br>
<pre><code>R1(config)#crypto key generate rsa general-keys modulus 1024</code></pre>
Configura el Tiempo de Espera esto es en Segundos. <br>
<pre><code>R1(config)#ip ssh time-out 30</code></pre>
Intentos validos. <br>
<pre><code>R1(config)#ip ssh authentication-retries 3</code></pre>
Usamos la versión 2, pues es más eficiente que la primera.
<pre><code>R1(config)#ip ssh version 2</code></pre>
Se asigna un usuario y contraseña para la autentificación. <br>
<pre><code>R1(config)#username UNCP secret Sistemas</code></pre>
Las líneas vty permiten el acceso a un dispositivo Cisco de forma remota. Se aplicara SSH a las 16 lineas de terminal. <br>
<pre><code>R1(config)#line vty 0 15</code></pre>
El comando login local en la configuración de línea habilita la base de datos local para la autenticación.<br>
<pre><code>R1(config-line)#login local</code></pre>
Configurar al menos una interface ethernet con conectividad IP para acceso via SSH. <br>
<pre><code>R1(config-line)#transport input ssh
R1(config-line)#exit</code></pre>
Se configura una contraseña para la conexión de consola al modo de usuario. <br>
<pre><code>R1(config)#enable secret Sistemas
R1(config)#exit</code></pre>
<h4>Sesion de SSH</h4>
<p align="center">
  <image src="/src/SSH2.png" alt="Seguridad LAN">
</p>
<h2>Seguridad VLAN</h2>
<h3>Configuracion</h3>
<p align="center">
  <image src="/src/SVL.png" alt="Seguridad LAN">
</p>
Configuramos las direcciones IP de los dispositivos
<p align="center">
  <image src="/src/SVL1.png" alt="Seguridad LAN">
</p>
<h4>Configuracion del switch</h4>

Switch>enable
Switch#config t
Enter configuration commands, one per line.  End with CNTL/Z.
Switch(config)#vlan 10
Switch(config-vlan)#name VLAN10
Switch(config-vlan)#exit
Switch(config)#interface range fastEthernet 0/1-3
// Se selecciona el puerto fa0/1-3
Switch(config-if-range)#switchport access vlan 10
//Asignamos los puertos a la vlan 10
Switch(config-if-range)#switchport port-security
// Se activa la seguridad del puerto
Switch(config-if-range)#switchport port-security mac-address sticky
// Asignamos la dirección mac del dispositivo que conectaremos al puerto
Switch(config-if-range)#switchport port-security maximum 1
// Solo se asignara una dirección mac a cada puerto
Switch(config-if-range)#switchport port-security violation shutdown
// En caso de una violación de seguridad, el puerto se apagara
Switch(config-if-range)#switchport mode access
Switch(config-if-range)#exit

Verificar que los puertos sean estáticos y que hayan sido correctamente asignados a su vlan.
<p align="center">
  <image src="/src/SVL2.png" alt="Seguridad LAN">
</p>
<h4>Prueba de inviolabilidad</h4>
<p align="center">
  <image src="/src/SVL3.png" alt="Seguridad LAN">
</p>
<h2>Seguridad WLAN</h2>
Ingresamos un router.
<p align="center">
  <image src="/src/SWL.png" alt="Seguridad LAN">
</p>
Configuramos su nombre por la interfaz
<p align="center">
  <image src="/src/SWL2.png" alt="Seguridad LAN">
</p>
La opción de seguridad la dejamos deshabilitada, pues el filtrado mac reemplazara esta.
<p align="center">
  <image src="/src/SWL3.png" alt="Seguridad LAN">
</p>
Ingresamos dos dispositivos y les colocamos las antenas.
<p align="center">
  <image src="/src/SWL4.png" alt="Seguridad LAN">
</p>
<p align="center">
  <image src="/src/SWL5.png" alt="Seguridad LAN">
</p>
<p align="center">
  <image src="/src/SWL6.png" alt="Seguridad LAN">
</p>
Conectamos los dos dispositivos a la red.
<p align="center">
  <image src="/src/SWL7.png" alt="Seguridad LAN">
</p>
Obtenemos las direcciones mac de los dispositivos.
<p align="center">
  <image src="/src/SWL8.png" alt="Seguridad LAN">
</p>
<p align="center">
  <image src="/src/SWL9.png" alt="Seguridad LAN">
</p>
Configuramos el filtrado mac e ingresamos la dirección mac solo de la laptop.
<p align="center">
  <image src="/src/SWL10.png" alt="Seguridad LAN">
</p>
Finalmente, la PC al no esta registrada dentro del filtro será desconectada.
<p align="center">
  <image src="/src/SWL11.png" alt="Seguridad LAN">
</p>
<h2>Protocolo STP</h2>
<h3>Configuracion</h3>
<p align="center">
  <image src="/src/STP1.png" alt="STP">
</p>
Desactivar el protocolo STP en los tres switches. Mediante el comando <code>no spanning-tree vlan 1</code>
<pre><code>Switch>enable
Switch#conf t
Enter configuration commands, one per line.  End with CNTL/Z.
Switch(config)#hostname SW1
SW1(config)#no spanning-tree vlan 1</code></pre>
<em>De igual forma en los otros 2 switches.</em><br>
<h4>Configurar las direcciones IP de las PC</h4>
<p align="center">
  <image src="/src/STP2.png" alt="STP">
</p>
<p align="center">
  <image src="/src/STP3.png" alt="STP">
</p>
Se encenderan todos los puertos. 
<p align="center">
  <image src="/src/STP4.png" alt="STP">
</p>
<h4>Prueba de conectividad</h4>
<p align="center">
  <image src="/src/STP5.png" alt="STP">
</p>
Reactivamos el protocolo STP en los tres switches, con el comando <code>spannig-tree vlan 1</code><br>
<pre><code>SW1(config)#spanning-tree vlan 1</code></pre>
<em>De igual forma en los otros 2 switches.</em><br>
Nuevamente hay conectividad
<p align="center">
  <image src="/src/STP6.png" alt="STP">
</p>
<p align="center">
  <image src="/src/STP7.png" alt="STP">
</p>
<h2>Seguridad AAA</h2>
<h3>Concepto</h3>
AAA significa Autenticación, Autorización y Contabilidad, y proporciona el marco para configurar el control de acceso en un dispositivo de red. 
<h3>Servidor</h3>
Con el método basado en el servidor, el enrutador accede a un servidor central AAA. El servidor AAA contiene los nombres de usuario y contraseñas de todos los usuarios. El router AAA usa el protocolo de sistema de control de acceso del controlador de acceso a terminales (TACACS +) o el protocolo de servicio de autenticación remota para usuarios de entrada telefónica (RADIUS) para comunicarse con el servidor de AAA. 
<h3>Configuracion</h3>
<p align="center">
  <image src="/src/AAA1.png" alt="AAA">
</p>
Configurar las IP de los servidores y los Router.
<p align="center">
  <image src="/src/AAA2.png" alt="AAA">
</p>
<p align="center">
  <image src="/src/AAA3.png" alt="AAA">
</p>
<p align="center">
  <image src="/src/AAA4.png" alt="AAA">
</p>
Verificamos las comunicaciones
<p align="center">
  <image src="/src/AAA5.png" alt="AAA">
</p>
Configuracion de router. <br>
<pre><code>Router>enable
Router#config t
Enter configuration commands, one per line.  End with CNTL/Z.
Router(config)#hostname R1
R1(config)#enable secret cisco123
R1(config)#username Arturo password cisco</code></pre>
Configuracion de servidor Tacacs 
<p align="center">
  <image src="/src/AAA6.png" alt="AAA">
</p>
Configuracion de servidor Radius 
<p align="center">
  <image src="/src/AAA7.png" alt="AAA">
</p>
<h4>Configuracion de router</h4>
<pre><code>R1(config)#AAA new-model
R1(config)#tacacs-server host 192.168.10.2 key cisco123
R1(config)#radius-server host 192.168.10.3 key cisco123
R1(config)#AAA authentication login default group tacacs+ group radius local-case</code></pre>
Prueba Tacacs
<p align="center">
  <image src="/src/AAA8.png" alt="AAA">
</p>
Prueba Radius
<p align="center">
  <image src="/src/AAA9.png" alt="AAA">
</p>
<p align="center">
  <image src="/src/AAA10.png" alt="AAA">
</p>
Prueba local
<p align="center">
  <image src="/src/AAA11.png" alt="AAA">
</p>
<p align="center">
  <image src="/src/AAA12.png" alt="AAA">
</p>
<h2>Red WAN</h2>
<h3>Configuracion</h3>
Se conectan los routers mediantes conexion serial
<p align="center">
  <image src="/src/WAN1.png" alt="AAA">
</p>
Configuramos las ip de los router y los dispositivos
<p align="center">
  <image src="/src/WAN2.png" alt="AAA">
</p>
    <p align="center">
  <image src="/src/WAN3.png" alt="AAA">
</p>
Registramos las ip de red
</p>
    <p align="center">
  <image src="/src/WAN4.png" alt="AAA">
</p>
