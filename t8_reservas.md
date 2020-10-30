# Reservas

## Crea una reserva para el que el cliente tome siempre la dirección 192.168.100.100.

## Tarea 8 : Indica las modificaciones realizadas en los ficheros de configuración y entrega una comprobación de que el cliente ha tomado esa dirección.

* En el servidor modificamos el fichero de configuracion **dhcpd.conf**

```sh
host cliente_linux {
  hardware ethernet 08:00:27:cf:b2:45;
  fixed-address 192.168.200.100;
}
```

* Reiniciamos el servicio

```sh
root@servidor:/home/vagrant# /etc/init.d/isc-dhcp-server restart
[ ok ] Restarting isc-dhcp-server (via systemctl): isc-dhcp-server.service.

```

* Vamos a comprobar en la máquina cliente que ha adoptado esta dirección

![reservalinux.png]()

* Lo hacemos con windows y además comprobamos que tenemos internet

```sh
host cliente_win {
  hardware ethernet 08:00:27:ED:01:E2;
  fixed-address 192.168.200.100;
}
```

![reservawin.png]()

