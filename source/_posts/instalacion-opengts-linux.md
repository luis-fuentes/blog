title: Instalar OpenGTS en Linux
date: 2012-02-24 15:52:26
tags:
- OpenGTS
- Linux
- Java
---

### Introducción

OpenGTS™ ("Open GPS Tracking System") es el primer proyecto código abierto diseñado para proporcionar mediante un entorno web el seguimiento de una "flota" de vehículos a través de GPS.

Diseñado en Java y JavaScript utilizando tecnologías tales como Apache Tomcat para el despliegue de servicios web y MySQL para el almacenamiento de datos. Como tal, OpenGTS se ejecutará en cualquier S.O. que soporte estas tecnologías (incluyendo Linux, Mac OS X, FreeBSD, OpenBSD, Solaris, Windows XP, Windows Vista, 20XX de Windows, y más).

### Instalación 

#### 1. Instalando el Software necesario para correr OpenGTS en linux

**1.1 Descarga Java Compiler**

Package: JDK 6 Update XX

[Descargar](http://www.oracle.com/technetwork/java/javase/downloads/jdk-6u26-download-400750.html)

Nota: Descarga solo el JDK 6 Update XX

o en terminal ingresamos:

    $ aptitude install sun-java6-jdk sun-java6-fonts

luego verificamos la versión instalada con:

    $ java -version

Asegúrate de estos datos:
```
java version "1.6.0_26"
Java(TM) SE Runtime Environment (build 1.6.0_26-b03)
Java HotSpot(TM) Server VM (build 20.1-b02, mixed mode)
```
Luego creamos una variable de entorno de java en el archivo /etc/profile

    $ export JAVA_HOME=/usr/lib/jvm/java-1.6.0-openjdk

(Asegúrate que */usr/lib/jvm/java-1.6.0-openjdk* sea la ruta correcta)

Se recomienda generar un enlace simbólico de "Java" en */usr/local/* que apunte a la dirección del JDK:

    $ cd /usr/local
     $ ln -s $JAVA_HOME java

**1.2 Descarga JavaMail Support**

Package: Sun JavaMail API (v1.4.4)

[Descargar]( http://www.oracle.com/technetwork/java/javamail/index.html)

Zip: javamail1_4_4.zip

Instalar el Archivo Mail.jar en la librería extendida de Java

    $ cd /Downloads/javamail-1.4.4
     $ cp mail.jar $JAVA_HOME/jre/lib/ext/

**1.3 Apache Ant Build Tool**

Package: Ant v1.8.2
[Descargar](http://ant.apache.org/bindownload.cgi) o
[Descargar Zip]( http://apache.freeby.pctools.cl//ant/binaries/apache-ant-1.8.2-bin.tar.gz)

o en terminal:

    $ aptitude install ant

**1.4 Apache "Tomcat" Servlet Container**

Package: Apache Tomcat v7.x servlet container
[Descargar](http://tomcat.apache.org/download-70.cgi) o 
[Descargar Zip](http://apache.freeby.pctools.cl/tomcat/tomcat-7/v7.0.26/bin/apache-tomcat-7.0.26.tar.gz)

Se recomienda instalarlo en el directorio *usr/local/*

    $ tar -zxvf apache-tomcat-7.0.26.tar.gz
     $ mv apache-tomcat-7.0.26 /usr/local/
     $ cd /usr/local/
     $ chmod -R a+r apache-tomcat-7.0.26 

Crear la variable de entorno en el archivo */etc/profile/*

    $ export CATALINA_HOME=/usr/local/apache-tomcat-7.0.26

Se recomienda generar un enlace simbólico de "Tomcat" en */usr/local/*

    $ ln -s /usr/local/apache-tomcat-7.0.26 /usr/local/tomcat


Verificamos que los archivos en *CATALINA_HOME/bin* tienen permisos de ejecución:

    $ cd $CATALINA_HOME/bin
     $ chmod a+x *.sh

**1.5 MySQL Database Provider**

Package: MySQL v5.X.X
[Descargar](http://dev.mysql.com/downloads/mysql/)

o en terminal:

    $ aptitude install mysql-server

**1.6 MySQL JDBC Driver**

Package: MySQL Connector/J v5.1.XX JDBC driver
[Descargar](http://dev.mysql.com/downloads/connector/j/) el Zip: mysql-connector-java-5.1.XX.tar.gz


    $ cp mysql-connector-java-5.1.17-bin.jar       JAVA_HOME/jre/lib/ext/

#### 2. Instalando y compilando OpenGTS

Copiamos la versión de OpenGTS descargada a */usr/local/*

    $ cp OpenGTS_2.3.7.zip /usr/local/
     $ unzip OpenGTS_2.3.7.zip
     $ chown -R root:staff OpenGTS_2.3.7

Crear la variable de entorno en el archivo */etc/profile/*

    $ export CATALINA_HOME=/usr/local/apache-tomcat-7.0.26

Se recomienda generar un enlace simbolico de "OpenGTS" en */usr/local/*

    $ cd /usr/local
     $ ln -s $GTS_HOME gts

**2.1 Inicializamos las tablas de la base de datos SQL**

    $ cd $GTS_HOME
     $ bin/initdb.sh -rootUser=root -rootPass=root

**2.2 Comprobamos la instalación con el siguiente script**

    $ cd $GTS_HOME
     $ bin/checkInstall.sh

El resultado debe ser No errors reported, No warnings reported.

**2.3 Creamos la cuenta "sysadmin"**

    $ cd $GTS_HOME
     $ bin/admin.sh Account -account=sysadmin -pass=123456 -create

#### 3. Instalando "track.war"

Para generar track.war se debe ejecutar

    $ cd $GTS_HOME
     $ ant track

Una vez creado el archivo, se instala con

    $ cd $GTS_HOME
     $ ant track.deploy

Para terminar reiniciamos Tomcat

    $ CATALINA_HOME/bin/shutdown.sh
     $ CATALINA_HOME/bin/startup.sh

ingresamos a nuestro servidor OpenGTS

http://localhost:8080/track/Track
