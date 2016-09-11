title: Guía React Native + Firebase
date: 2016-07-11 19:20:33
tags:
- OS X
- Guías
- React
- React Native
- Firebase
---

### Configuración

Los primeros pasos con react native son sensillos, si ya tienes todo configurado puedes saltar estos pasos. 

Lo primero que necesitas es [Homebrew](http://brew.sh/), tambien necesitas [Node.js 4](https://nodejs.org/en/) o superior, el team de react native recomienda usar [NVM](https://github.com/creationix/nvm#installation) para manejar distintas versiones de Node. 

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

Esto ejecutara el emulador y deberias ver la siguiente pantalla:

![React Native Emulador](/images/rn-blank-app.png)

React native vien con hot-reloading instalado lo que significa que puedes editar el codigo de tu app, luego presionar *Cmd+R* y ver tus cambios instantaneamente, si eres un desarrollador iOS o de cualquier paltaforma, sabes lo genial que es esto.

Con todo configurado vamos por Firebase.

### Configurar Firebase

React Native maneja las dependencias a traves de NPM. Para instalar Firebase, ejecuta lo siguiente en el directorio raiz de tu proyecto

    $ npm install firebase --save

Abre *index.ios.js* y agrega lo siguiente a la primera linea.

    import * as firebase from 'firebase';

Luego arriba de el componente, inicializa firebase con tus valores de configuracion

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


