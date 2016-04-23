title: Primeros pasos con Webpack
date: 2015-07-03 02:45:44
tags:
- Guías
- Javascript 
- Webpack
---

Para continuar la [introducción](https://luisfuentes.me/introduccion-webpack/) a Webpack voy a implementar un proyecto básico.
Primero asegúrate que tienes instalado NodeJS y [NPM](https://luisfuentes.me/guia-npm/). Luego en el terminal ejecutamos.

```
$ mkdir webpack-app
$ cd webpack-app
$ npm init
```
Esto iniciará nuestro proyecto y creará un nuevo package.json, luego instalamos Webpack y la librería browser de manera local y lo agregamos como una dependencia de desarrollo. 

    $ npm i webpack node-libs-browser --save-dev

Ahora generamos un poco la estructura de esta nuevo proyecto:


```
-/app
  -main.js
  -component.js
-/build
  -bundle.js (este se genera automagicamente)
  -index.html
-package.json
-webpack.config.js
```

Lo primero será configurar webpack para que genere este archivo bundle.js.

**webpack.config.js**


```
var path = require('path');

module.exports = {
  entry: path.resolve(__dirname, 'app/main'),
  output: {
    path: path.resolve(__dirname, 'build'),
    filename: 'bundle.js',
  },
};
```


#### La primera Build

Ahora que tenemos la configuración básica lista, crearemos la típica app Hello World.

**app/component.js**

```
module.exports = function () {
  var element = document.createElement('h1');
  element.innerHTML = 'Hello world';
  return element;
};
```
**app/main.js**

```
var component = require('./component');
var app = document.createElement('div');

document.body.appendChild(app);
app.appendChild(component());
```

Ahora si corres este comando en la terminal

    $ node_modules/.bin/webpack

Webpack generará el archivo bundle.js en base a nuestros archivos en la carpeta /app. El resultado en el terminal debiera ser parecido a esto:

```
> webpack-app@1.0.0 build /Users/something/projects/webpack-app
> webpack

Hash: e02f97146a15a8a5c3a9
Version: webpack 1.8.4
Time: 44ms
    Asset     Size  Chunks             Chunk Names
bundle.js  1.74 kB       0  [emitted]  main
   [0] ./app/main.js 115 bytes {0} [built]
   [1] ./app/component.js 134 bytes {0} [built]
```

Ahora para usar de verdad este paquete, nos falta definir nuestro archivo index.

**build/index.html**

```
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8"/>
  </head>
  <body>
    <script src="bundle.js"></script>
  </body>
</html>
```
Doble click a nuestro archivo index.html y debería estar funcionando. 

Para terminar podemos agregar webpack a nuestro archivo package.json para que este se ejecute como un comando npm. esto será muy útil en el futuro cuando agreguemos más scripts a nuestra app. Solo agregamos las siguientes lineas:

**package. introducción** 

```
"scripts": {
  "build": "webpack"
}
```

Listo, para terminar solo ejecutas

    $ npm run build

y nuestra app se generará...

