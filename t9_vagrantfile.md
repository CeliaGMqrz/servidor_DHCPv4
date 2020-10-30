# Fichero Vagrant file

Hemos añadido un nuevo nodo (nodo3) y una nueva red local (red_local_second). Además hemos puesto la autoconfiguración de vagrant **false** para que no se modifique al levantar las máquinas.

```sh
# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

  config.vm.define :nodo1 do |nodo1|
    nodo1.vm.box = "debian/buster64"
    nodo1.vm.hostname = "servidor"
    nodo1.vm.network "public_network"
    nodo1.vm.network "private_network", ip: "192.168.200.2",
      virtualbox__intnet: "red_local",
      auto_config: false
    nodo1.vm.network "private_network", ip: "192.168.200.2",
      virtualbox__intnet: "red_local_second",
      auto_config: false
  end
  config.vm.define :nodo2 do |nodo2|
    nodo2.vm.box = "debian/buster64"
    nodo2.vm.hostname = "nodolan1"
    nodo2.vm.network "private_network",
      virtualbox__intnet: "red_local",
      auto_config: false
  end
    config.vm.define :nodo3 do |nodo3|
    nodo3.vm.box = "debian/buster64"
    nodo3.vm.hostname = "nodolan2"
    nodo3.vm.network "private_network",
      virtualbox__intnet: "red_local_second",
      auto_config: false
  end
end
  
```
