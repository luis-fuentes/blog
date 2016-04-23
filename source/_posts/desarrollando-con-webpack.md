title: Desarrollando con Webpack
date: 2015-07-25 01:04:25
tags:
- Guías
- Javascript 
- Webpack
---

En [primeros pasos con Webpack](https://luisfuentes.me/primeros-pasos-webpack/) generamos un proyecto básico pero teníamos que ejecutar *$ npm run build* cada vez que hacíamos un cambio... y adicionalmente refrescar el browser. Con algunos simples cambios intentaremos mejorar nuestro workflow de trabajo.  
Lo primero es instalar webpack-dev-server

    $ npm i webpack-dev-server --save-dev

Ademas debemos modificar nuestro package.json para usarlo:

**package.json**

```
...
"scripts": {
  "build": "webpack",
  "start": "webpack-dev-server --config webpack.development.js --devtool eval-source --progress
 --colors --hot --content-base build"
},
...
```
  Creamos un nuevo archivo de configuración:

**webpack.development.js**

```
var path = require('path');

var ROOT_PATH = path.resolve(__dirname);

module.exports = {
  entry: [
    'webpack/hot/dev-server',
    'webpack-dev-server/client?http://localhost:8080',
    path.resolve(ROOT_PATH, 'app/main.js'),
  ],
  output: {
    path: path.resolve(ROOT_PATH, 'build'),
    filename: 'bundle.js',
  },
};
```

Ahora cuento ejecutes `$ npm start` en tu terminal se ejecutaran los siguientes scripts declarados en package.json

1. **webpack-dev-server** - Inicia el server en localhost:8080
2. **--config webpack.development.js** - Apunta a nuestro archivo de configuración. 
3. **--devtool eval-source** - Crea la ruta de nuestras urls, para que luego las puedas apuntar con el nombre del archivo.
4. **--progress** - Muestra el progreso de el generador. 
5. **--colors** - Agrega colores al terminal. 
6. **--hot** - habilita la carga en caliente o hot loading.
7. **--content-base build** - Apunta a build para seguir ocupando index.html(eliminaremos esto luego)

Ahora cada vez que ejecutes `$ npm start` se iniciara el servidor en el puerto 8080 y cada vez que cambies algún archivo estos se generarán automáticamente.

También podemos configurar Webpack para que busque cambios en nuestros archivos css y los actualiza, primero instalamos:

    $ npm i css-loader style-loader --save-dev

y modificamos nuestro archivo webpack para que busque y cargue todos los archivos terminados en .css.

**webpack.development.js**

```
var path = require('path');

var ROOT_PATH = path.resolve(__dirname);

module.exports = {
  entry: [
    'webpack-dev-server/client?http://localhost:8080',
    'webpack/hot/dev-server',
    path.resolve(ROOT_PATH, 'app/main'),
  ],
  output: {
    path: path.resolve(ROOT_PATH, 'build'),
    filename: 'bundle.js',
  },
  module: {
    loaders: [
      {
        test: /\.css$/,
        loaders: ['style', 'css'],
      },
    ],
  }
};
```

Ahora solo falta un detalle, agregar css a nuestro proyecto...

**app/stylesheets/main.css** 

```
body {
  background: cornsilk;
}
```
**app/main.js**

```
require('./stylesheets/main.css');
...
```

`$ npm start`y ahora podrás modificar el css y los cambios se cargara automagicamente. Pero esto actualmente no esta funcionando en `$ npm run build` por lo que tendrías que hacer los mismo cambios en el archivo *webpack.config.js*... Para ahorrarnos este trabajo podemos unir nuestro archivos de configuración.

Primero instalamos una pequeña utilidad que concatena arrays en lugar de remplazarlos. 

    $ npm i webpack-merge --save-dev

Finalmente modificamos nuestros archivos de configuración:

**webpack.config.js**

```
var path = require('path');
var merge = require('webpack-merge');

var TARGET = process.env.TARGET;
var ROOT_PATH = path.resolve(__dirname);

var common = {
  entry: [path.resolve(ROOT_PATH, 'app/main')],
  output: {
    path: path.resolve(ROOT_PATH, 'build'),
    filename: 'bundle.js',
  },
  module: {
    loaders: [
      {
        test: /\.css$/,
        loaders: ['style', 'css'],
      },
    ],
  },
};

if(TARGET === 'build') {
  module.exports = common;
}

if(TARGET === 'dev') {
  module.exports = merge(common, {
    entry: [
      'webpack-dev-server/client?http://localhost:8080',
      'webpack/hot/dev-server'
    ]
  });
}
```

**package.json**

```
...
"scripts": {
  "build": "TARGET=build webpack",
  "start": "TARGET=dev webpack-dev-server --devtool eval 
--progress --colors --hot --content-base build"
},
...
```

Finalmente nuestro proyecto funciona en base a el archivo *index.html* pero cuando comience a crecer, esto puedo generar problemas. Para mejorar esto instalamos:

    $ npm i html-webpack-plugin --save-dev

Eliminamos nuestro archivo *index.html* y lo generamos automáticamente en cada build.

**webpack.config.js** 

```
var path = require('path');
var HtmlWebpackPlugin = require('html-webpack-plugin');
var merge = require('webpack-merge');

var TARGET = process.env.TARGET;
var ROOT_PATH = path.resolve(__dirname);

var common = {
  ...
  plugins: [
    new HtmlWebpackPlugin({
      title: 'Webpack app',
    }),
  ],
};

...
```

También eliminamos `--content-base`

**package.json**

```
...
"scripts": {
  "build": "TARGET=build webpack",
  "start": "TARGET=dev webpack-dev-server --devtool 
eval-source --progress --colors --hot"
},
...
```

Finalmente ejecutamos `$ npm run build` y nuestro proyecto se generará automáticamente. Debo mencionar que esta no es la única manera de usar Webpack. algunas personas prefieren usar archivos de configuración separados o configurar presets para ocupar en cada proyecto [hjs-webpack](https://github.com/HenrikJoreteg/hjs-webpack). 

Código fuente en [Github](https://github.com/YotaCL/webpack-boilerplate.git) 