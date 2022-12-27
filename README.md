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

<h2>WLAN</h2>
<h2>Seguridad LAN</h2>
<h2>Seguridad VLAN</h2>
<h2>Seguridad WLAN</h2>
<h2>Protocolo STP</h2>
<h2>Seguridad AAA</h2>
<h2>Seguridad WAN</h2>
