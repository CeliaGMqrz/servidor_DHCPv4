# Analizando paquetes con tcpdump

## Tarea 5: Realizar una captura, desde el servidor usando tcpdump, de los cuatro paquetes que corresponden a una concesión: DISCOVER, OFFER, REQUEST, ACK.


* Instalamos el paquete **tcpdump** en el servidor:

```sh
apt-get install tcpdump
```

* Para ver las interfaces de red disponibles para tcpdump hacemos lo siguiente:

```sh
root@servidor:/home/vagrant# tcpdump -D
1.eth0 [Up, Running]
2.eth1 [Up, Running]
3.eth2 [Up, Running]
4.any (Pseudo-device that captures on all interfaces) [Up, Running]
5.lo [Up, Running, Loopback]
6.nflog (Linux netfilter log (NFLOG) interface)
7.nfqueue (Linux netfilter queue (NFQUEUE) interface)

```

* Queremos escuchar **eth1** que es donde se produce la redireccion de paquetes desde **eth2**. Necesitamos la opción -n para ver los puertos.

* REQUEST

![tcpdump1.png]()