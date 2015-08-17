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

Las apps en django son pequeñas funcionalidades del proyecto.

Un ejemplo de app podría ser el panel de administrador "admin", y que es la encargada de gestionar solamente el panel de administrador.

Para crear una app tendremos que ejecutar el siguiente código.

```bash
python manage.py startapp nombre
```
Al crear una app nos creará una carpeta con el nombre de la app y con los siguientes archivos:

- Un directorio con el nombre **migrations** que contendrá un archivo **\_init_.py**.
- 4 archivos: 
    - admin.py
    - models.py
    - tests.py
    - views.py

## Ficheros

### urls.py

### \_init_.py
Son ficheros que python los reconoce como módulos. No hace falta editarlos, ya que normalmente suelen estar vacios.

### admin.py

### models.py

### tests.py

### views.py

