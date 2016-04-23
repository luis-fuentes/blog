title: Ruby On Rails en Debian
date: 2013-06-03 16:05:53
tags:
- ror
- ruby
- debian
- guia
---

### Instalación

El primer paso para instalar [RoR](http://rubyonrails.org) es instalar ruby, abre el terminal y:

    $ aptitude install ruby

Instalamos ruby gems:

    $ aptitude install rubygems

Algunos comandos para manejar las gemas son:
     
    //Actualizar ruby
     $ gem update –system 
     //Ver gemas instaladas
     $ gem list
     // instalar algún módulo
     $ gem install módulo

Instalamos ruby on rails

    $ aptitude install rails 

Si vamos a usar mysql debemos instalar el driver mysql para RoR:

    $ aptitude install mysql-server
     $ aptitude install libmysqlclient-dev
     $ gem install mysql

### Primeros pasos con RoR

Para crear un proyecto ejecutas:

    $ rails nombreDelProyecto

Configuras el proveedor de bases de datos en **config/database.yml**

```
development:
  adapter: mysql
  database: database_dev
  host: localhost
  username: root
  password: password_del_root

test:
  adapter: mysql
  database: database_test
  host: localhost
  username: root
  password: password_del_root

production:
  adapter: mysql
  database: database_prod
  host: localhost
  username: root
  password: password_del_root
```

Para terminar

    $ rake db:create:all

Creamos nuestro primer scaffold de ejemplo en la base de datos

    $ ruby script/generate scaffold Pelicula titulo:string descripcion:text url_caratula:string

Y en el archivo de migraciones **db/migrate/20120107183925_create_peliculas.rb**

```
class CreatePeliculas < ActiveRecord::Migration
  def self.up
    create_table :peliculas do |t|
      t.string :titulo
      t.text :descripcion
      t.string :url_caratula

      t.timestamps
    end
  end

  def self.down
    drop_table :peliculas
  end
end
```
Para terminar ejecutamos la migración. 

    $ rake db:migrate

Y finalmente para revisar nuestro ejemplo activamos el webserver

   $ ruby script/server