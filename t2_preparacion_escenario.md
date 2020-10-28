# Preparación del escenario. Fichero Vagrantfile

Vamos a crear un escenario usando Vagrant que defina las siguientes máquinas:

* Servidor: Tiene dos tarjetas de red: una pública y una privada que se conectan a la red local
* nodolan1: Un cliente conectado a la red local.

## Servidor dhcp

Vamos a instalar un servidor dhcp en un nodo **"servidor"** que de servicio a los ordenadores de la red local, teniendo en cuenta que el tiempo de concesión sea de **12 horas** y que la red local tiene el direccionamiento **192.168.200.0/24.** 

*NOTA: El direccionamiento de mi máquina anfitriona es el 192.168.100.0 por lo que en esta práctica para la red local he usado el 192.168.200.0.*


## Fichero Vagrantfile

```sh
# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

  config.vm.define :nodo1 do |nodo1|
    nodo1.vm.box = "debian/buster64"
    nodo1.vm.hostname = "servidor"
    nodo1.vm.network "public_network"
    nodo1.vm.network "private_network", ip: "192.168.200.2",
      virtualbox__intnet: "red_local"
  end
  config.vm.define :nodo2 do |nodo2|
    nodo2.vm.box = "debian/buster64"
    nodo2.vm.hostname = "nodolan1"
    nodo2.vm.network "private_network",
      virtualbox__intnet: "red_local"
  end
end
  
```
* Mostramos las direcciones de nuestro servidor:

```sh
vagrant@servidor:~$ ip a
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host 
       valid_lft forever preferred_lft forever
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UP group default qlen 1000
    link/ether 08:00:27:8d:c0:4d brd ff:ff:ff:ff:ff:ff
    inet 10.0.2.15/24 brd 10.0.2.255 scope global dynamic eth0
       valid_lft 85581sec preferred_lft 85581sec
    inet6 fe80::a00:27ff:fe8d:c04d/64 scope link 
       valid_lft forever preferred_lft forever
3: eth1: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UP group default qlen 1000
    link/ether 08:00:27:2c:e4:a6 brd ff:ff:ff:ff:ff:ff
    inet 192.168.100.151/24 brd 192.168.100.255 scope global dynamic eth1
       valid_lft 2790sec preferred_lft 2790sec
    inet6 fe80::a00:27ff:fe2c:e4a6/64 scope link 
       valid_lft forever preferred_lft forever
4: eth2: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UP group default qlen 1000
    link/ether 08:00:27:fe:37:c3 brd ff:ff:ff:ff:ff:ff
    inet 192.168.200.2/24 brd 192.168.200.255 scope global eth2
       valid_lft forever preferred_lft forever
    inet6 fe80::a00:27ff:fefe:37c3/64 scope link 
       valid_lft forever preferred_lft forever

```

* Mostramos las direcciones de nuestro cliente: (previamente hemos configurado una dirección estática para nuestro cliente "192.168.200.3")

```sh
vagrant@nodolan1:~$ ip a
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host 
       valid_lft forever preferred_lft forever
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UP group default qlen 1000
    link/ether 08:00:27:8d:c0:4d brd ff:ff:ff:ff:ff:ff
    inet 10.0.2.15/24 brd 10.0.2.255 scope global dynamic eth0
       valid_lft 85623sec preferred_lft 85623sec
    inet6 fe80::a00:27ff:fe8d:c04d/64 scope link 
       valid_lft forever preferred_lft forever
3: eth1: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UP group default qlen 1000
    link/ether 08:00:27:96:c3:4c brd ff:ff:ff:ff:ff:ff
    inet 192.168.200.3/24 brd 192.168.200.255 scope global eth1
       valid_lft forever preferred_lft forever
    inet6 fe80::a00:27ff:fe96:c34c/64 scope link 
       valid_lft forever preferred_lft forever

```

* Comprobamos que el cliente y el servidor se hacen ping por la red local

Del cliente al servidor:
```sh
vagrant@nodolan1:~$ ping 192.168.200.2
PING 192.168.200.2 (192.168.200.2) 56(84) bytes of data.
64 bytes from 192.168.200.2: icmp_seq=1 ttl=64 time=0.337 ms
64 bytes from 192.168.200.2: icmp_seq=2 ttl=64 time=0.283 ms
^C
--- 192.168.200.2 ping statistics ---
2 packets transmitted, 2 received, 0% packet loss, time 83ms
rtt min/avg/max/mdev = 0.283/0.310/0.337/0.027 ms

```
Del servidor al cliente:
```sh
vagrant@servidor:~$ ping 192.168.200.3
PING 192.168.200.3 (192.168.200.3) 56(84) bytes of data.
64 bytes from 192.168.200.3: icmp_seq=1 ttl=64 time=0.398 ms
64 bytes from 192.168.200.3: icmp_seq=2 ttl=64 time=0.312 ms
^C
--- 192.168.200.3 ping statistics ---
2 packets transmitted, 2 received, 0% packet loss, time 14ms
rtt min/avg/max/mdev = 0.312/0.355/0.398/0.043 ms

```

* En las dos máquinas tenemos acceso a la red exterior. Ya que vagrant por defecto crea una interfaz para poder acceder por ssh a ellas, usando nat, con el direccionamiento 10.0.2.15/24. Aprovechamos esta característica para poder actualizar las máquinas e instalar DCHP.

En ambas máquinas:
```sh
apt-get update
apt-get upgrade
```

* Seguir la guía: [Configuración del servidor y el cliente. Lista de concesiones.](https://github.com/CeliaGMqrz/servidor_DHCPv4/blob/main/t3_configuracion_servidor_y_cliente_dchp.md)