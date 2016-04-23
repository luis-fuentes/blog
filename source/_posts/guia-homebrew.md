title: Guía Homebrew
date: 2014-04-23 15:26:26
tags:
- OS X
- Guías
- Homebrew 
---

### ¿Que es homebrew?
Homebrew es un gestor de paquetes esencial para OSX, desarrollado en ruby y para los que vienen de linux, funciona parecido a `apt-get` o `yum`.

<!--more-->

![Homebrew](http://techtastico.com/files/2013/10/Homebrew.png)

### Instalación

Como OSX ya tiene ruby instalado, solo debemos ejecutar en consola:

    $ ruby -e "$(curl -fsSL https://raw.github.com/Homebrew/homebrew/go/install)"
    
Después de instalar se recomienda correr doctor para buscar algún inconveniente:

    $ brew doctor
    
### ¿Ahora?

En homebrew a los paquetes se les denomina fórmulas, para instalar una solo debes ejecutar:

    $ brew install nombre_formula

Si quieres buscar una fórmula:

    $ brew search nombre_formula
    
Para borrar una fórmula:

    $ brew remove nombre_formula
    
¿Quieres actualizar una fórmula?

    $ brew upgrade nombre_formula
    
¿Quieres actualizar Homebrew?

    $ brew update
    
Para ver las fórmulas que tienes instaladas:

    $ brew list
