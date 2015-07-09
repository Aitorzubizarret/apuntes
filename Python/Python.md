# Python

## Comprobar versión instalada

Utilizaremos la consola para comprobar la versión de Python que tenemos instalada por defecto en nuestro ordenador. Para ello, escribiremos el siguiente comando, que además de mostrarnos la versión también nos abrirá el interprete de Python.

```bash
python
```

Para salir del interprete tan solo tendremos que escribir el siguiente comando.

```bash
exit()
```

## PIP, Sistema de Gestión de Paquetes

PIP es un sistema de gestión de paquetes que se utiliza para instalar y gestionar paquetes de software escritos en Python.

Muchos de esos paquetes de software se pueden encontrar en el [Índice de Paquetes de Python](https://pypi.python.org/pypi).


[PIP en Wikipedia]
[PIP en Wikipedia]: https://en.wikipedia.org/wiki/Pip_(package_manager)

### Instalación de PIP

Para poder usar PIP, primero tendremos que instalarlo, para ello escribiremos el siguiente comando en la consola.

```bash
sudo easy_install pip
```

[Link](https://lcaballero.wordpress.com/2013/03/14/instalacion-de-paquetes-python-con-setuptools-y-easyinstall/)

[Link](http://www.3engine.net/wp/2013/12/python-como-instalar-pip/)

[Link](https://wiki.python.org/moin/CheeseShopTutorial)

[Link](https://plone.org/countries/mx/instalacion-de-setuptools-y-easyinstall-para-python)

## Virtualenv, Herramienta para crear entornos virtuales

[Oficial](https://pypi.python.org/pypi/virtualenv/)

[Link](https://lcaballero.wordpress.com/2012/10/22/creacion-de-entornos-virtuales-python/)

### Instalación

```bash
sudo pip install virtualenv
```

### Creación de un entorno virtual

```bash
virtualenv nombreDirectorio
```

### Activar el entorno virtual

Una vez que estamos en el directorio que se ha creado cuando hemos creado el entorno virtual escribiremos el siguiente comando en la consola.

```bash
source bin/activate
```

