# Data Storage

[Documentación Oficial](http://developer.android.com/training/basics/data-storage/files.html)

## Tipos

http://developer.android.com/guide/topics/data/data-storage.html

### SharedPreferences

http://www.elandroidelibre.com/2010/08/aprendiendo-android-vi-recordando-valores-shared-preferences.html
http://www.javaya.com.ar/androidya/detalleconcepto.php?codigo=142
http://www.sgoliver.net/blog/preferencias-en-android-i-shared-preferences/
http://developer.android.com/reference/android/content/Context.html#getSharedPreferences(java.lang.String,%20int)
http://developer.android.com/guide/topics/data/data-storage.html#pref
http://developer.android.com/reference/android/content/SharedPreferences.html

### Internal Storage

### External Storage

### SQLite Databases

### Network Conection

## Elegir ubicación

Si queremos usar el sistema de ficheros de Android para leer o escribir datos tendremos que elegir la ubicación de esos datos.

Tenemos 2 lugares, almacenamiento interno o almacenamiento externo.

|Almacenamiento Interno|Almacenamiento Externo|
|----------------------|----------------------|
|Siempre disponible|Puede que no este siempre disponible, ya que el usuario puede acceder a los datos y eliminarlos|
|Los datos solo son accesibles por la App|Cualquier App puede leer estos datos|
|Cuando el usuario elimina la App, se borran los datos con ella|Cuando el usuario elimina la App, sólo se borrarán los datos si utilizas el comando ```getExternalFilesDir()```|

[getExternalFilesDir()](http://developer.android.com/reference/android/content/Context.html#getExternalFilesDir(java.lang.String))

### Almacenamiento interno

Podemos acceder a esa información a través del programa Android Device Manager.
Seleccionamos el dispositivo, y después vamos a data/data/<nuestra app>/files
<nuestra app> = com.aitorzubizarreta.counter

### Almacenamiento externo

# Activity

## AndroidManifest.xml

Si queremos que nuestra App solo se ejecute en horizontal o vertical, podremos configurarlo en el documento AndroidManifest.xml dentro del apartado Activity.

Para ello, utilizaremos la etiqueta android:screenOrientation=portrait, para que la App solo se ejecute en vertical.

[Web oficial](http://developer.android.com/guide/topics/manifest/activity-element.html)