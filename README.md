# Aplicación android del proyecto 3A de Zaida Pastor Gonzalez.

## Base de la aplicación para el proyecto, escrita con kotlin.

Esta aplicación es mi apuesta para la base de nuestro proyecto de biometría. 
El uso de kotlin hace que sea más versátil y el uso de json para enviar datos hace que sea más visual.
En su versión inicial, he construido una layout sencillo que te muestra el último beacon recibido.
La app detecta los beacons emitidos por la placa, los muestra por pantalla y los envía al servidor en formato json donde se almacenan en la base de datos.

## Como preparar la app para que funcione con el servidor personal y un arduino diferente al nuestro.

1. Lo primero es clonar este repositorio.
2. Después hay que instalarse la última versión de Android Studio. Yo he usado Giraffe.
3. Luego de abrir el proyecto, hay que cambiar el UUID para que la app filtre los beacons correctamente.
4. Obtenga el UUID de su placa con una app paea detectar beacons. Yo uso NRF Connect. Pulse sobre el beacon 
deseado (lo reconocerá por su nombre) y copie el UUID.
5. En el archivo MainActivity, línea 44-45, pege el UUID en el primer campo de Identifier.parse 
   * // Crear una región para detectar todos los beacons (UUID, major y minor en null)
        val region = Region("myRegion", Identifier.parse("Ponga aquí su UUID completo"), null, null)

6. Ahora hay que modificar la parte de la conexión e ip.
7. Abrir la terminal de windows y ejecutar el comando ipconfig, copiar el campo Dirección IPv4.
8. En MainActivity, línea 90, pegar la nueva ip en el campo correspondiente.
    val url = URL("http://PongaAquiSuIP/bd/recibir_json.php")

### Preparar un dispositivo android para instalar la aplicación 
La aplicación debe instalarse en un dispositivo físico, nunca virtual.
Utilizo un dispositivo samsung, tenga en cuanta que si posee otro distinto puede que las instrucciones 
varíen. 

1. Acceda a las opciones de desarrollador, se activan desde ajustes -> Acerca del teléfono -> información de 
software y pulsando en el número de compliación 5 veces.
2. Acceda a las opciones de desarrollador y habilite la depuración por USB.
3. Conecte el dispositivo a su ordenador y permita la depuración.
4. Desde android studio, en la parte superior debería aparecer el nomre de su dispositivo.
5. Pulse el botón de "play" para instalar la app.
6. Una vez instalada, concédale todos los permisos desde ajustes -> aplicaciones -> BeaconAndroid -> permisos.
7. Una vez instalada y abierta, la app detectará y mostrará los beacons emitidos desde la placa con el UUID 
deseado y los reenviará al servidor, donde se almacernarán en la base de datos.

## Bugs conocidos
### Bugs con la detección de beacons
Si al tener todo funcionando, no aparece nada en la pantalla de la app, asegúrese de que esté en una red 
personal que permita este tráfico de datos. La red de la UPV bloquea algunas conexiones necesarias.
