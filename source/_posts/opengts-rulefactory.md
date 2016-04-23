title: Crear un RuleFactory en OpenGTS
date: 2012-08-02 16:10:17
tags:
---

Primero activamos las casillas en OpenGTS y los campos en la BD

En el archivo StartupInit.java modificamos:

    Device.setRuleFactory(new RuleFactoryExample());


En el archivo config.conf modificamos:

    startupInit.Device.NotificationFieldInfo=true


En el Archivo private.xml modificamos:

    <Property key="deviceInfo.showNotificationFields">true</Property>


En el archivo RuleFactoryExample.java modificamos:

    private static boolean SEND_NOTIFICATION = true;


En el archivo common.conf modificamos:

```
# --- SMTP
# --- (outgoing email configuration parameters)
##smtp.host=localhost
#smtp.debug=false
smtp.host=smtp.gmail.com
smtp.port=465
smtp.user=Mail@gmail.com
smtp.user.emailAddress=Mail@gmail.com
smtp.password=Password
smtp.enableSSL=true
#smtp.enableTLS=true
#smtp.threadModel.show=false
```

Actualizamos la bd:

    bin/dbAdmin.pl -tables=ca

Y finalmenet compilamos :D


Nota: Si no aparecen los nuevos campos, borramos manualmente track.war

Stop Tomcat:
    ``$CATALINA_HOME/bin/shutdown.sh``

Delete the existing "track" servlet:
    ``rm -rf $CATALINA_HOME/webapps/track*``

Deploy the new "track" servlet:
    ``cp $GTS_HOME/build/track.war $CATALINA_HOME/webapps/``

Restart Tomcat:
    ``$CATALINA_HOME/bin/startup.sh")`
