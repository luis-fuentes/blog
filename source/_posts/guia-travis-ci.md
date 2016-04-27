title: Guía Travis CI
date: 2016-03-02 20:14:22
tags:
---

### Introducción

[Travis-CI](https://travis-ci.org) Es una un servicio distribuido de integracion continua, se usa para levantar y hacer tests a tu software alojado en GitHub cada vez que haces un git push. Y facilita enormemente el trabajo tanto si eres el unico desarrollador o estas en un team.
<!--more-->
Es gratis para proyectos de codigo abierto y se paga para usarlo en proyectos privados, Tambien hay una version propietaria que permita hacer estas implementaciones en tus equipos. 

### Instalación

Una vez que accedes con tu cuenta de GitHub, travis automaticamente sincroniza todos tus repositorios y solo debes elegir desde tu perfil en cual o cuales deseas activar el servicio.

El siguiente paso es agregar un archivo llamado ***.travis.yml*** a la raiz de tu repositorio. En este archivo le cuentas a travis de que se trata tu repositorio, que lenguaje usas y los test que quieres correr.
Si el archivo no existe o esta mal escrito, travis ignorará tu repositorio. 

Archivos de ejemplo segun hay [acá](https://docs.travis-ci.com/user/language-specific/) y en esta guia usaremos uno para hacer deploy a un blog en [Hexo](https://hexo.io/).

Pero primeros generamos un nuevo token de acceso en [GitHub](https://github.com/settings/tokens)

Luego en travis-ci vamos a settings en nuestro proyecto y generamos una nueva variable de entorno.

**Nombre:** DEPLOY_REPO
**Valor:** https://{token}@github.com:user/repository-name.git

ahora configuramos nuestro archivo ***.travis.yml***

```
language: node_js
node_js:
    - "5"

before_install:
    - npm install -g hexo

install:
    - npm install

before_script:
    - git config --global user.name 'Luis Fuentes'
    - git config --global user.email 'hola@luisfuentes.me'

script:
    - hexo generate

after_success:
    - mkdir .deploy
    - cd .deploy
    - git init
    - git remote add origin $DEPLOY_REPO
    - cp -r ../public/* .
    - git add -A .
    - git commit -m 'Site updated'
    - git push --force --quiet origin master
```

Si usas un theme modificado como en mi caso, debes agregarlo como un submodulo en git, creando un archivo ***.gitmodules*** en el root de tu blog y agregando lo siguiente:

```
[submodule "apollo"]
    path = themes/apollo
    url = https://github.com/luis-fuentes/hexo-theme-apollo.git
```



