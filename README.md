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
<h2>Seguridad LAN</h2>
<h2>Seguridad VLAN</h2>
<h2>Seguridad WLAN</h2>
<h2>Protocolo STP</h2>
<h2>Seguridad AAA</h2>
<h2>Seguridad WAN</h2>
