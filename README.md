# Servidor DHCPv4

## ¿Qué es Servidor DHCP?

El **servidor DHCP** (Dynamic Host configuration Protocol), es un servidor de Red el cual permite una asignación automática de direcciones IP, gateways predeterminadas, así como otros parámetros de red que necesiten los clientes. 

Es una extensión del protocolo **BOOTP**, (*Protocolo UDP de arranque, utlizado por los clientes para obtener su dirección IP*), que proporciona más flexibilidad en cuanto a la administración de direcciones IP. 

El servidor DCHP cuenta con dos elementos: 

* Un mecanismo para asignar direcciones IP y otros parámetros TCP/IP, como hemos indicado anteriormente.

* Un protocolo para negociar y transmitir información específica del host.

El host que solicita la información de configuración se denomina **cliente DHCP** y el que provee esa información se llama **servidor DHCP**. El DCHP se describe en la norma **RFC 2131**.

## Administración de direcciones con el servidor DCHP.

El protocolo DCHP usa 3 métodos diferentes para asignar direcciones IP. 

Puede usar la **Asignación manual**, como propiamente dice se agrega manualmente en el servidor DCHP la IP del cliente DCHP. 

Puede usar la **Asignación automática**, que no requiere asignación manual, directamente el servidor DCHP le asigna una dirección IP al cliente DCHP, pero esta dirección es permanente, es decir, que cada vez que el cliente se conecte siempre obtendrá la misma dirección. 

Por último tenemos la **Asignación dinámina**, que es la más frecuente y la que vamos a utlizar en esta guía. Consiste en que, el Servidor DCHP asigna una dirección IP al cliente por un tiempo determinado. Esto quiere decir que cuando el cliente solicite una direccion IP el servidor le proporciona una pero cuando se desconecte la devuelve, y cuando se vuelva a conectar le proporciona otra diferente, ya que, la IP anterior puede que la tenga otro cliente.

Como hemos visto, este protocolo permite la reutilización automática de una dirección IP. Si un cliente DCHP ya no necesita esa IP, como por ejemplo cuando apagamos el ordenador, éste libera su dirección y se la entrega al DHCP, el cuál puede reasignar dicha dirección a otro cliente que se la pida.

De esta forma podemos aprovechar un rango de direcciones IP que sea algo limitado para muchos más clientes ya que, la asignación es dinámica y temporal.

ÍNDICE

* Tarea 1: [Funcionamiento del servidor DCHP](https://github.com/CeliaGMqrz/servidor_DHCPv4/blob/main/t1_funcionamiento.md)
* Tarea 2: [Preparación del escenario. Fichero Vagrantfile]()
* Tarea 3: [Configuración del servidor DCHP. Lista de concesiones y configuración del cliente DCHP.]()
* Tarea 4: [Configuración del servidor: Router NAT]()
* Tarea 5: []()
* Tarea 6: []()
* Tarea 7: []()
* Tarea 8: []()
* Tarea 9: []()
* Tarea 10: []()
* Tarea 11: []()