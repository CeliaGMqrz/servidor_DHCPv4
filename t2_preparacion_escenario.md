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
    nodo2.vm.network :private_network, ip: "192.168.200.3",
      virtualbox__intnet: "red_local"
  end
end
  
```



