# Funcionamiento de dhcp

## PASOS PREVIOS 

* Hemos agregado un cliente windows a la red local

![win1.png](https://github.com/CeliaGMqrz/servidor_DHCPv4/blob/main/capturas/win1.png)

* Comprobamos que el cliente windows tiene una dirección ip dada por el servidor DHCP y tiene acceso a internet, ya que nuestro servidor actúa tambien como router nat.

![clientewin.png]()

 
## Tarea 6 : Los clientes toman una configuración, y a continuación apagamos el servidor dhcp. ¿qué ocurre con el cliente windows? ¿Y con el cliente linux?

* Apagamos el servidor dhcp y vemos que, primero perdemos la conexión a internet con los dos clientes

![t61.png](https://github.com/CeliaGMqrz/servidor_DHCPv4/blob/main/capturas/t61.png)

![t62.png](https://github.com/CeliaGMqrz/servidor_DHCPv4/blob/main/capturas/t62.png)


* Si reinciamos ambas máquinas e intentamos hacer una peticion *DHCPDIISCOVER* comprobamos que no obtenemos la dirección ip desde dchp puesto que nuestro servidor está apagado. 

* En windows toma una dirección aleatoria

![clientewin6.png](https://github.com/CeliaGMqrz/servidor_DHCPv4/blob/main/capturas/clientewin6.png)


* En linux directamente no obtiene ip

![clientelinux6.png](https://github.com/CeliaGMqrz/servidor_DHCPv4/blob/main/capturas/clientelinux6.png)

## Tarea 7 : Los clientes toman una configuración, y a continuación cambiamos la configuración del servidor dhcp (por ejemplo el rango). ¿qué ocurriría con un cliente windows? ¿Y con el cliente linux?


* Si cambiamos el rango en el servidor dhcp:

![rango.png](https://github.com/CeliaGMqrz/servidor_DHCPv4/blob/main/capturas/rango.png)

* Reiniciamos el servicio

```sh
root@servidor:/home/vagrant# /etc/init.d/isc-dhcp-server restart
[ ok ] Restarting isc-dhcp-server (via systemctl): isc-dhcp-server.service.

```

* Vemos que cambia en nuestros clientes:

Cliente Debian10 

![rangolinux.png](https://github.com/CeliaGMqrz/servidor_DHCPv4/blob/main/capturas/rangolinux.png)

Cliente Windows
![rangowindows.png](https://github.com/CeliaGMqrz/servidor_DHCPv4/blob/main/capturas/rangowindows.png)
