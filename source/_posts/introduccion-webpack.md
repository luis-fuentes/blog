title: Introducción a Webpack
date: 2015-06-25 02:48:45
tags:
- Guías
- Javascript 
- Webpack
---

Para entender Webpack voy a hablar un poco de historia y además alternativas, hace algunos años con hacer un concat a algunos scripts bastaba, pero ahora las bibliotecas javascript han crecido demasiado y a nadie le gusta esperar a que se cargue toda la web para que esta se muestre. 

<!--more-->

Este problema se ha intensificado por el aumento de las WebApps single-page. Estas tienden a basarse en varias bibliotecas bastante pesadas ​​y complejas. Y lo ideal sería cargar solo lo que necesitamos.

Para mejorar y automatizar el trabajo con estas librerías nacieron herramientas llamadas Task-Runer, la primera conocida fue [Grunt](http://gruntjs.com/) que se basa en una arquitectura de plugins. Luego fue desplazada por [Gulp](http://gulpjs.com/) que en vez de plugins usaba código para automatizar las tareas. 

Javascript no tiene un concepto claro de módulos hasta ES6 por lo que trabajar con estos siempre fue un problema. y estábamos aun en los años 90 en lo que se refiere a browser environment. 

Intentando solucionar esto aparecieron herramientas como [Browserify](http://browserify.org/) que te dejan requerir módulos en el browser. Y además puedes conectarlo con Gulp para automatizar esta tarea. El ecosistema de Browserify esta compuesto por muchos pequeños módulos, Es un poco más fácil de aprender y es una buena alternativa a Webpack. 

### Webpack

![¿Que es Webpack?](/images/what-is-webpack.png)

[Webpack](http://webpack.github.io/) toma un enfoque más monolítico frente a Browserify. Se puede configurar en base a código y ademas lo puedes extender usando loaders. Básicamente usando 'require' puedes requerir los módulos que necesites: CoffeeScript, Sass, Markdown, etc.. 

Toma todas tus dependencias, las carga a través de loaders y exporta código compatible con el browser. Todo esto se basa en configuración, Aquí les dejo un ejemplo de una configuración del tutorial oficial de Webpack:

```
module.exports = {
  entry: './entry.js',
  output: {
    path: __dirname,
    filename: 'bundle.js'
  },
  module: {
    loaders: [
      {
        test: /\.css$/,
        loader: 'style!css'
      }
    ]
  }
};
``` 

Para [**continuar**](https://luisfuentes.me/primeros-pasos-webpack/) solo queda desarrollar un proyecto en base a Webpack y así facilitar todo el proceso de desarrollo. 