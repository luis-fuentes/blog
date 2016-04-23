title: Desarrollando sitios estáticos con Hugo
date: 2015-05-08 17:45:29
tags:
- Guías
- Static
- Web
---

### Introducción
[Hugo](http://gohugo.io/) es framework para websites, técnicamente es un generador de sitios estáticos. A continuación te mostraré como instalarlo y los primeros pasos con él. 

<!--more-->

### Instalación 

Primero descarga [Hugo](http://gohugo.io/) desde la web oficial o por terminal ejecuta

    $ brew install hugo

Para crear una web base ejecutamos

    $ hugo new site /path/to/site

Genera la primera pagina de contenido estático

    $ hugo new about.md

Instalamos los themes disponibles

    $ git clone --recursive https://github.com/spf13/hugoThemes themes

Y finalmente ejecutamos nuestro server. (agregamos un theme y generamos las paginas en estado draft)

    $ hugo server --theme=hyde --buildDrafts