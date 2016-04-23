title: Guía Vagrant
date: 2015-01-15 17:48:06
tags:
- OS X
- Guías
- Vagrant
---

#### Introducción
[Vagrant](https://www.vagrantup.com) es una herramienta para crear entornos virtuales de desarrollo, esto viene muy bien para no instalar nada en tu equipo, compartir el mismo entorno entre varios desarrolladores, replicar la exacta configuración de tu servidor de producción en tu maquina local, Tener varios entornos de desarrollo al mismo tiempo, etc...

<!--more-->

![Vagrant Logo](/images/logo_wide-dce715a5.png)

#### Instalación

- El primer paso es descargar e instalar [VirtualBox](https://www.virtualbox.org/wiki/Downloads) (hay otras alternativas pero esta es gratis).

- Descarga e instala [Vagrant](http://www.vagrantup.com/downloads).

#### Primeros pasos

Para comenzar iniciamos una maquina virtual de vagrant, en este caso instalaré Ubuntu LTS 14.04, que es lo que normalmente uso en mi droplet de [Digital Ocean](https://www.digitalocean.com/?refcode=e32ae009945f).

    $ vagrant init ubuntu/trusty64

Solo queda levantar el box (La primera vez toma varios minutos).

    $ vagrant up --provider virtual box


Para ingresar a nuestro box por ssh

    $ vagrant ssh

Para sincronizar otra carpeta con nuestra box modificamos el archivo *Vagrantfile*

    config.vm.synced_folder "/Users/UserName/Carpeta", "/vagrant"

Nota: Siguiendo esta [Guía](https://www.digitalocean.com/community/tutorials/how-to-set-up-apache-virtual-hosts-on-ubuntu-14-04-lts) podemos configurar virtual hosts en nuestro box.
