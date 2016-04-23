title: Guía Yeoman
date: 2014-07-05 15:26:26
tags:
- OS X
- Guías
- Yeoman
---

### Introducción 

El Workflow de Yeoman(YO) se compone de tres herramientas fundamentales para la mejora de la productividad y la satisfacción en la construcción de una aplicación web. Estas herramientas son:

<!--more-->

* **YO** - La herramienta de scaffolding de Yeoman.

* **Bower** - Es una herramienta de gestión de paquetes y dependencias, mantenida por twitter y una comunidad open-source.

* **Grunt** - Es un Task-Runer y sirve para automatizar tareas como compilar o testear.

Cada uno de estos proyectos se mantienen de forma independiente por sus respectivas comunidades, pero funcionan bien juntos como parte de un flujo de trabajo prescriptivo para mantenerte eficaz.

![Como funciona](/images/yeoman-workflow.jpg)

A través de estas herramientas podrás:

* Crear el esqueleto de tu app muy rapido y podras elegir entre cientos de plantillas o generadores como *HTML5, Boilerplate, Bootstrap, MEAN, Angular, etc...*

* Compila automáticamente *Coffeescript* y *Compass*, además refresca automáticamente los cambios en el navegador gracias a *LiveReload* (Chao refresh (╯°□°）╯︵ ┻━┻).

* Compara tus scripts con *JSHint* para comprobar el uso de buenas prácticas.

* Puede optimizar tus imágenes con *OptiPNG* y *JPGTran*.

* Sistema de control de paquetes!

* Te lanza un servidor propio, entorno de pruebas y mucho más!!

### Instalación

Yeoman(YO) es mantenido por el proyecto Yeoman y sirve para generar el scaffolding de aplicaciones web, utilizando plantillas de scaffolding que se llaman generadores. Normalmente se instala YO y luego el generador que necesites a través de npm.

  $ npm install -g yo
    
    
Si usas una version de npm inferior a 1.2.10 debes instalar Bower y Grunt por separado:

  $ npm install -g grunt-cli bower
    
Los generadores oficiales los puedes encontrar en este [Link](http://yeoman.io/official-generators.html). Y para instalarlos debes ejecutar:

  $ npm install -g nombre_generador
    
Luego creas una carpeta para el proyecto y al interior ejecutas:

  $ yo nombre_generador --flags

*Nota: Las flags son opcionales y dependen del generador.*


![Yeoman!](/images/yeoman-banner.png)

