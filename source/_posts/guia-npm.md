title: Guía NPM
date: 2014-11-22 17:48:32
tags:
- OS X
- Guías
- NPM
---

### ¿Que es NPM?

[NPM](https://www.npmjs.com/) es un gestor de paquetes para javascript, hace algunas versiones es el gestor predeterminado de nodejs y con el podremos gestionar los paquetes para nuestras aplicaciones. 

<!--more-->

![NPM logo](/images/npm.png)

Viene instalado por defecto con la instalación de nodejs pero si no lo tienes, lo puedes instalar a través de [Homebrew](https://luisfuentes.me/guia-homebrew/) con el siguiente comando:

    $ brew install node

### ¿Ahora?

- Primero creamos una aplicación, esto nos generará un archivo **package.json** que contiene la configuración inicial de nuestro proyecto y donde posteriormente guardaremos las dependencias de esta mismo. Para instalar ejecutamos:
    
      $ npm init

- Para buscar otros paquetes utilizamos el parámetro search:

        $ npm search nombre-del-paquete

- Si descargas un paquete/aplicación de internet, este ya tiene un archivo package.json con todas sus dependencias, en este caso ejecutas:

        $ npm install

- Para agregar y guardar una dependencia a tu proyecto debes ejecutar el siguiente comando cuando agregues un paquete.

        $ npm install nombre-del-paquete --save

- En el caso de que el paquete que instalamos solo lo usamos cuando estamos desarrollando agregamos:

        $ npm install nombre-del-paquete --save-dev

- Finalmente para iniciar una aplicación ejecutamos (previamente debemos configurar el archivo package.json) 

        $ npm start 
