<h1>Script de comandos de packet tracer</h1>
<h2>Enrutamiento VLAN</h2>
<p>Las redes de área local virtuales o más conocidas como VLAN, es una tecnología de red que permite crear redes lógicas independientes dentro de la misma red física. El objetivo de usar VLAN en un entorno doméstico o profesional, es para segmentar adecuadamente la red y usar cada subred de una forma diferente.</p>
<p align="center">
  <image src="/src/VLAN.png" alt="VLAN en el simulador Packet Tracer">
</p>
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
Acceso al modo de administrador
  ```
  Switch> enable
  ```
  ```sh
 composer install 
```
Accede al Modo de configuración global
  ```
  Switch#configure terminal
  ```
Cambia el nombre del dispositivo
  ```
  Switch(config)#hostname SW1
  ```
Se crea la vlan 10
  ```
  SW1(config)#vlan 10
  ```
<h2>Enrutamiento entre VLAN con Switches de Capa 3</h2>
<h2>WLAN</h2>
<h2>Seguridad LAN</h2>
<h2>Seguridad VLAN</h2>
<h2>Seguridad WLAN</h2>
<h2>Protocolo STP</h2>
<h2>Seguridad AAA</h2>
<h2>Seguridad WAN</h2>
