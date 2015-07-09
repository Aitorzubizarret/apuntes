# Bluetooth

Toda la información sobre la API de Bluetooth en Android está disponíble en las siguientes webs oficiales.

- [Classic Bluetooth](http://developer.android.com/guide/topics/connectivity/bluetooth.html)
- [Bluetooth Low Energy](http://developer.android.com/guide/topics/connectivity/bluetooth-le.html)

**Classic Bluetooth** se utiliza para operaciones intensivas como pueden ser streming y/o comunicación constante entre dispositivos, y consume mucha batería.

**Bluetooth Low Energy** se utiliza para operaciones en las que el consumo de energia debe ser mínimo. Esta disponible a partir de Android 4.3 (API level 18).

|API|Descripción|
|---|-----------|
|BluetoothAdapter|Representa el hardware Bluetooth del dispositivo|
|BluetoothdDevice|Representa un dispositivo remoto|
|BluetoothServerSocket|Se usa para abrir un socket para escuchar conexiones entrantes.<br> Cuando se crea una conexión provee de un objeto de tipo BluetoothSocket.|
| BluetoothSocket|Usado por el cliente para establecer una conexión con un dispositivo remoto. <br>Una vez que el dispositivo esta conectado, se utilizará un objeto del tipo BluetoothSocket por las dos partes para controlar la conexión y recibir la información entrante y saliente.|

### Bluetooth Adapter

- [Bluetooth Adapter](http://developer.android.com/reference/android/bluetooth/BluetoothAdapter.html)

### Bluetooth Device

### Bluetooth Server Socket y Bluetooth Socket


1 - Turn on Bluetooth for the device

2 - Find paired or available devices within range

3 - Connect to the device

4 - Transfer data between devices

[Ejemplo 1](http://www.egr.msu.edu/classes/ece480/capstone/spring14/group01/docs/appnote/Wirsing-SendingAndReceivingDataViaBluetoothWithAnAndroidDevice.pdf)

[Ejemplo 2](http://www.egr.msu.edu/classes/ece480/capstone/)

[Ejemplo 3](http://www.instructables.com/id/Android-Bluetooth-Control-LED-Part-2/?ALLSTEPS)


## 1 - Permisos para usar el Bluetooth

Para poder usar la API de Bluetooth en Android primero necesitamos añadir los permisos a la aplicación.
Añadiremos los siguientes permisos en el documento ``AndroidManifest.xml``, dentro de *manifest* pero fuera de *aplication*.

```java
<uses-permission android:name="android.permission.BLUETOOTH" />
<uses-permission android:name="android.permission.BLUETOOTH_ADMIN" />
```

El permiso **BLUETOOTH** nos dará acceso a la comunicación mediante Bluetooth, para poder solicitar o aceptar una petición de emparejamiento y para transferir datos.

El permiso **BLUETOOTH_ADMIN** nos permitirá buscar dispositivos Bluetooth y cambiar las propiedades del Bluetooth de nuestro dispositivo como activarlo o desactivarlo sin salir de nuestra App y sin tener que ir a las preferencias del móvil.

[Etiqueta *uses-permission*](http://developer.android.com/guide/topics/manifest/uses-permission-element.html)

[Estructura del fichero *AndroidManifest.xml*](http://developer.android.com/guide/topics/manifest/manifest-intro.html)

## 2 - Comprobar si el dispositivo tiene Bluetooth

Antes de que nuestra aplicación haga uso del Bluetooth tendremos que asegurarnos de que el dispositivo realmente dispone de él. Para ello, crearemos una variable de tipo **BluetoothAdapter** y pediremos el adaptardor de Bluetooth del dispositivo. Si recibimos *null* significará que nuestro dispositivo no dispone de Bluetooth.

```java
BluetoothAdapter myBluetoothAdapter = BluetoothAdapter.getDefaultAdapter();
if (myBluetoothAdapter == null) {
    // El dispositivo no tiene Bluetooth
} else {
    // El dispositivo SI tiene Bluetooth
}
```

## 3 - Comprobar el estado del Bluetooth (encendido o apagado)

Una vez que tenemos constancia de que el dispositivo dispone de Bluetooth tendremos que comprobar si se encuentra encendido o apagado. Para ello utilizaremos la función *isEnabled* que tiene el adaptador que hemos creado, *myBluetoothAdapter*, para saber si el dispositivo tenía Bluetooth o no.

```java
if (myBluetoothAdapter.isEnabled()) {
	// El Bluetooth está encendido
} else {
	// El Bluetooth está apagado
}
```

## 4 - Encender / apagar el Bluetooh

### 4.1 - Encender el Bluetooth

Utilizaremos un Intent para encender el Bluetooth del dispositivo sin tener que salir de nuestra App y sin tener que ir a la configuración del dispositivo.

```java
Intent enableBTIntent = new Intent(BluetoothAdapter.ACTION_REQUEST_ENABLE);
startActivityForResult(enableBTIntent, REQUEST_ENABLE_BT);
```

Dependiendo de la versión habrá que lanzar uno u otro intent.

- http://stackoverflow.com/questions/28365260/detect-bluetooth-le-devices-in-android
- https://developer.android.com/about/versions/android-4.3.html

Para saber cuando cambia el estado del Bluetooth (de on a off y/o viceversa) podemos usar [*ACTION\_STATE\_CHANGED*](http://developer.android.com/reference/android/bluetooth/BluetoothAdapter.html#ACTION_STATE_CHANGED) Broadcast Action.

### 4.2 - Apagar el Bluetooth

Para apagar el Bluetooth tan solo tendremos que decirle a nuestro ``BluetoothAdapter`` que se desabilite.

```java
myBTAdapter.disable();
```

### 4.3 - Resultados del *startActivityForResult*

Como hemos utilizado un *intent* del tipo *startActivityForResult* para encender el Bluetooth, podremos capturar el resultado de este utilizando la función ``onActivityResult``.

## 5 - Hacer visible nuestro dispositivo

Una vez que tenemos el Bluetooth encendido tenemos la opción de estar visible, para que otros dispositivos con Bluetooth puedan vernos, o estar ocultos, para que no nos puedan ver a la hora de hacer una busqueda.

```java
Intent makeBTVisibleIntent = new Intent(BluetoothAdapter.ACTION_REQUEST_ENABLE);
startActivityForResult(makeBTVisibleIntent, ACTION_REQUEST_DISCOVERABLE);
```

- [Link 1](http://www.compiletimeerror.com/2013/11/turn-on-and-off-bluetooth-in-android.html#.VXCABZ_I1p8)
- [Link 2](http://alvinalexander.com/java/jwarehouse/apps-for-android/BTClickLinkCompete/src/net/clc/bt/StartDiscoverableModeActivity.java.shtml)

## 7 - Buscar dispositivos con Bluetooth cerca de nosotros

[startDiscovery](http://developer.android.com/reference/android/bluetooth/BluetoothAdapter.html#startDiscovery())

[Tutorial 1](http://www.londatiga.net/it/programming/android/how-to-programmatically-scan-or-discover-android-bluetooth-device/)

[Web 1](http://www.londatiga.net/it/programming/android/how-to-programmatically-scan-or-discover-android-bluetooth-device/)

[Web 2](http://alvinalexander.com/java/jwarehouse/apps-for-android/BTClickLinkCompete/src/net/clc/bt/StartDiscoverableModeActivity.java.shtml)

Para empezar la busqueda utilizaremos la función *startDiscovery()*. Este proceso es asincrono asi que tendremos que utilizar un *BroadcastReceiver* para escuchar ``ACTION_FOUND``, ``ACTION_DISCOVERY_STARTED`` y ``ACTION_DISCOVERY_FINISHED``.

```java
myBTAdapter.startDiscovery()
```

## 8 - Comunicación entre dispositivos

[Ejemplo 1](http://www.londatiga.net/it/programming/android/how-to-programmatically-pair-or-unpair-android-bluetooth-device/)

Para que pueda haber una comunicación entre 2 dispositivos a través de Bluetooth, primero tienen que estar **emparejadores** o **paired**.

getBondState() -> http://developer.android.com/reference/android/bluetooth/BluetoothDevice.html#getBondState()

### Lista de dispositivos emparejados

Para poder acceder a la lista de dispositivos emparejados necesitamos tener el Bluetooth encendido.

```
Set<BluetoothDevice> pairDevices = myBTAdapter.getBondedDevices();
```

### Emparejar / Pair

```java
private void pairDevice(BluetoothDevice device) {
	try {
		Method method = device.getClass().getMethod("createBond", (Class[]) null);
		method.invoke(device, (Object[]) null);
	} catch (Exception e) {
		e.printStackTrace();
	}
}
```

[Link 1](http://www.londatiga.net/it/programming/android/how-to-programmatically-pair-or-unpair-android-bluetooth-device/)

[Ejemplo](http://mobile.antonio081014.com/2013/05/how-to-implement-pair-and-unpair-with.html)

[Pairing](http://stackoverflow.com/questions/7337032/how-can-i-avoid-or-dismiss-androids-bluetooth-pairing-notification-when-i-am-do)

[Pairing](http://stackoverflow.com/questions/5885438/bluetooth-pairing-without-user-confirmation)

[Pairing](https://code.google.com/p/android/issues/detail?id=26041)

[Pairing](http://kenneththorman.blogspot.com.es/2013/06/android-403-and-404-bluetooth-pairing.html)


### Desemparejar / Unpair

```java
private void unpairDevice(BluetoothDevice device) {
	try {
		Method method = device.getClass().getMethod("removeBond", (Class[]) null);
		method.invoke(device, (Object[]) null);
	} catch (Exception e) {
		e.printStackTrace();
	}
}
```

### Enviar datos

[Ejemplo](http://www.javacodegeeks.com/2013/09/bluetooth-data-transfer-with-android.html)

[Ejemplo 2 A](https://wingoodharry.wordpress.com/2014/04/07/anrdroid-sendreceive-data-with-arduino-via-bluetooth-part-1/)

[Ejemplo 2 B](https://wingoodharry.wordpress.com/2014/04/15/android-sendreceive-data-with-arduino-using-bluetooth-part-2/)

## Escuchar los cambios de estado del Bluetooth

Crearemos un **IntentFilter** para escuchar todos los mensajes sobre lo que definamos a través del filtro.
En nuestro caso, el filtro será, mensajes del adaptador del Bluetooth relacionados con cambios,
esto es, cuando cambie el estado del Bluetooth capturaremos ese Intent.

```java
IntentFilter filterBTStatusChanged = new Intent(myBTAdapter.ACTION_STATE_CHANGED);
registerReceiver(myReceiver, filterBTStatusChanged);
```

Una vez que tengamos el *IntentFilter* tendremos que crear un *BroadcastReceiver*.

```java
private final BroadcastReceiver myReceiver = new BroadcastReveiver() {
	@Override
	public void onReceive(Context context, Intent intent) {
		String action = intent.getAction();
		if (action.equals(myBTAdapter.ACTION_STATE_CHANGED)) {
			int state = intent.getIntExtra(myBTAdapter.EXTRA_STATE, myBTAdapter.ERROR);
			switch (state) {
				case BluetoothAdapter.STATE_OFF:
					connDescriptionTextView.setText(BT_STATE_OFF);
					break;
				case BluetoothAdapter.STATE_TURNING_ON:
					connDescriptionTextView.setText(BT_STATE_TURNING_ON);
					break;
				case BluetoothAdapter.STATE_ON:
					connDescriptionTextView.setText(BT_STATE_ON);
					break;
				case BluetoothAdapter.STATE_TURNING_OFF:
					connDescriptionTextView.setText(BT_STATE_TURNING_OFF);
					break;
			}
		}
	}
};
```

## Bluetooth Class

http://developer.android.com/reference/android/bluetooth/BluetoothClass.html

## UI Switch Button

- [Ejemplo 1](http://www.mysamplecode.com/2013/04/android-switch-button-example.html)

### Modificar estado (activado o desactivado)

Podemos cambiar el estado del switch a activado o desactiva con esta función.

```Java
mySwitch.setChecked(true); // Aparecerá On
mySwitch.setChecked(false); // Aparecerá Off
```

### Comprobar su estado

Si queremos saber si el switch esta activado o desactivado tan solo tendremos que llamar a la función *isChecked()*.

```java
if (mySwitch.isChecked()) {
	// Esta activado
} else {
	// Esta desactivado
}
```

## UI Progress Dialog

### Mostrar el Progress Dialog

```java
myProgressDialog.show();
```

### Ocultar el Progress Dialog

```java
myProgressDialog.dismiss();
```