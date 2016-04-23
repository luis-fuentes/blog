title: Desarrollando con ESLint y Sublime Text
date: 2015-05-24 02:55:52
tags:
- OS X
- Guías
- Javascript
- ESLint
- Sublime Text
- Babel
- ES6
- ES2015
- ReactJS
---

### Introducción

Me imagino que la mayoría conoce [Sublime Text](http://www.sublimetext.com) por lo que les voy a comentar la magia que trae ESlint a nuestro workflow de desarrollo. 

[ESLint](https://github.com/eslint/eslint) es una herramienta que identifica y reporta patrones y errores en código ECMAScript/JavaScript. es similar a JS-Lint y JSHint con algunas diferencias:

- ESLint usa Espree para analizar JavaScript.
- ESLint usa un AST para evaluar patrones en código. 
- ESLint soporta plugins, cada regla es un plugin y puedes agregar más en desarrollo.  

### Instalación
Para instalar eslint globalmente usamos npm(además instalaremos un plugin de [Babel](https://github.com/babel/babel-eslint)).

    $ npm install -g eslint babel-eslint

Pero recomiendo hacerlo localmente en cada proyecto como dev dependencia.

    $ npm install --save-dev eslint@latest babel-eslint@latest

Luego creamos un archivo *.eslintrc* en el directorio raíz de nuestro proyecto.

```
{
  // ¡Quiero usar babel-eslint para el análisis!
  "parser": "babel-eslint",
  "env": {
    // El código es para un browser
    "browser": true,
    // En CommonJS
    "node": true
  },
  // Ejemplo de reglas para encontrar errores:
  "rules": {
    "quotes": [2, "single"],
    "eol-last": [0],
    "no-mixed-requires": [0],
    "no-underscore-dangle": [0]
  }
}
```
Y agregamos el siguiente script a *package.json* para correr el lint mediante npm.
```
  "scripts": {
    "lint": "eslint src"
  },
```

### Configurando Sublime

Lo primero es instalar [Package Control](https://packagecontrol.io/installation) a través de las instrucciones de la web oficial.

Mediante package control instalas [SublimeLinter](http://sublimelinter.readthedocs.org/en/latest/installation.html#installing-via-pc), por defecto este no incluye linters para ningún lenguaje, por lo que instalaremos [SublimeLinter-contrib-eslint](https://github.com/roadhump/SublimeLinter-eslint#plugin-installation) (desinstala otros linters si es que los tenias). 

Luego le enseñaremos a sublime a reconocer ES6  instalando el paquete [babel-sublime](https://github.com/babel/babel-sublime). Posteriormente elige este paquete como la sintaxis por defecto para archivos *.js* y *.jsx*.

Solo nos falta definir en sublime-linter que sublime-babel es una variación de javascript. Para esto vamos a *SublimeLinter Settings — User* en el menu de comandos.

![SublimeLinter Settings — User](/images/1-pq13xAtg6aNY6WPp9PncYA.png)

y agregamos *javascript (babel)* al *syntax_map*

![Syntax Map](/images/1-FQ3xxn5GZM-mv896YEJV7A.png)

¡¡Listo!! solo reinicia sublime y cada vez que grabes analizara tu código. Si quieres cambiar esto para que te avise en mientras escribes. Configuralo en *Choose Lint Mode*

![Choose Lint Mode](/images/1-Cbqe8u-LssZ_JFTArM77NQ.png)

### Extra
Si estas desarrollando en react, puedes agregar el [plugin de react](https://github.com/yannickcr/eslint-plugin-react).

    $ npm install --save-dev eslint-plugin-react@latest

y modificar el archivo *.eslintrc* más o menos así:

```
{
  // Soporte a jsx
  "ecmaFeatures": {
    "jsx": true,
    "modules": true
  },
  // ¡Quiero usar babel-eslint para el análisis!
  "parser": "babel-eslint",
  "env": {
    // El código es para un browser
    "browser": true,
    // En CommonJS
    "node": true
  },
  // Ejemplo de reglas para encontrar errores:
  "rules": {
    "quotes": [2, "single"],
    "eol-last": [0],
    "no-mixed-requires": [0],
    "no-underscore-dangle": [0],
    "strict": [2, "never"],
    "react/jsx-uses-react": 2,
    "react/jsx-uses-vars": 2,
    "react/react-in-jsx-scope": 2
  },
  // Agregamos el plugin
  "plugins": [
    "react"
  ]
}
```
