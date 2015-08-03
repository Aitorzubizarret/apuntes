# Django


## Startproject
```bash
django-admin.py startproject congresomadrid
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

```bash
python manage.py startapp nombre
```

