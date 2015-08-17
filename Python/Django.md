# Django


## Startproject
```bash
django-admin.py startproject holamundo
```

## Run server
```bash
python manage.py runserver
```
Para salir del servidor cuando esta en marcha, pulsar

```bas
control c
```

## Migrate
```bash
python manage.py migrate
```

Creará el fichero **db.sqlite3**


## Crear usuario administrador

```bash
python manage.py syncdb
```

Ejecutará **python manage.py migrate** y además nos dará la opción de crear un administrador si no lo tenemos definido todavía.

A partir de la version 1.9 de django **syncdb** no funcionará.

```bash
python manage.py createsuperuser
```

## App

Las apps en django son pequeñas funcionalidades del proyecto. Realizan una función muy concreta de manera muy eficaz, por lo que se pueden reutilizar en distintos proyectos.

Un ejemplo de app podría ser el panel de administrador "admin", y que es la encargada de gestionar solamente el panel de administrador.

Para crear una app tendremos que ejecutar el siguiente código.

```bash
python manage.py startapp nombre
```
Al crear una app nos creará una carpeta con el nombre que le hemos dado a la app y con los siguientes archivos y directorio:

* Un directorio con el nombre migrations que contendra un archivo init.py.
* 5 archivos, admin.py, models.py, tests.py, views.py y init.py


## Ficheros

### settings.py
Es el archivo de configuración del proyecto.

#### Variables

##### Secret_key

Mirar

##### Debug
Ponerla en off cuando el proyecto este en producción.

##### Allowed_hosts

##### Middleware_classes
Mirar más adelante.

##### Templates

##### Databases
Configuración de la base de datos.

### urls.py
Gestiona las peticiones.
Es un enrutador de urls.

### \_init_.py
Son archivos que python los reconoce como módulos. No hace falta editarlos, ya que normalmente suelen estar vacios.

### admin.py

### models.py
Tiene relación con **django.db** por lo tanto tiene algo que ver con la base de datos y con los datos.

### tests.py
Para crear tests

### views.py
Para mostrar 

## Modelos

Una vez que hemos hecho un modelo tendremos que añadirlo a la BD.

```
python manage.py makemigrations
python manage.py migrate
```