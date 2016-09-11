title: Guía React Native + Firebase
date: 2016-07-11 19:20:33
tags:
- OS X
- Guías
- React
- React Native
- Firebase
---


![Guía React Native + Firebase](/images/firebase-react.png) 
### Configuración

Los primeros pasos con react native son sencillos, si ya tienes todo configurado puedes saltar estos pasos. 

Lo primero que necesitas es [Homebrew](http://brew.sh/), tambien necesitas [Node.js 4](https://nodejs.org/en/) o superior, el team de react native recomienda usar [NVM](https://github.com/creationix/nvm#installation) para manejar distintas versiones de Node. 

<!--more-->

Una vez tienes todo instalado ejecuta

    $ brew install watchman
     $ npm install -g react-native-cli

Y finalmente puedes iniciar una nueva app con el comando

    $ react-native init SupermercadoApp # o el nombre que quieras. 

Abre el proyecto con tu editor favorito

    $ subl SupermercadoApp o atom SupermercadoApp o el que uses :P

### Compilar y Ejecutar

Para compilar un proyecto en React Native ejecuta

    $ react-native run-ios

Esto ejecutará el emulador y deberías ver la siguiente pantalla:

![React Native Emulador](/images/rn-blank-app.png)

React native viene con hot-reloading instalado lo que significa que puedes editar el código de tu app, luego presionar ***Cmd+R*** y ver tus cambios instantáneamente, si eres un desarrollador iOS o de cualquier plataforma, sabes lo genial que es esto.

Con todo configurado vamos por Firebase.

### Configurar Firebase

React Native maneja las dependencias a través de NPM. Para instalar Firebase, ejecuta lo siguiente en el directorio raíz de tu proyecto

    $ npm install firebase --save

Abre ***index.ios.js*** y agrega lo siguiente a la primera línea.

    import * as firebase from 'firebase';

Luego arriba de el componente, inicializa firebase con tus valores de configuración

```
// Initialize Firebase
const firebaseConfig = {
  apiKey: "<your-api-key>",
  authDomain: "<your-auth-domain>",
  databaseURL: "<your-database-url>",
  storageBucket: "<your-storage-bucket>",,
};
const firebaseApp = firebase.initializeApp(firebaseConfig);
```

¿Que es ***const***?

*const* se usa para referenciar un valor que nunca va a cambiar, que hace sentido en este caso porque no quieres sobreescribir el valor de la configuración de Firebase. Podemos usar esta palabra clave porque estamos usando Node.js 4 o superior. 

Pero una función de ES2015 no es suficiente. En vez de usar *React.createClass()* para declarar componentes, vamos a usar clases.

### ES2015(ES6) Componentes 

Continuará...


