# Instalar y configurar Percepio Tracealyzer

## Instalar Percepio Tracealyzer

Descomprimir el archivo `TzForFreeRTOS-3.1.2.tgz` en el directorio `setr/tracealyzer`. Para comprobar que funciona correctamente, ejecutar el archivo `TzForFreeRTOS.exe`. En la ventana que aparece a continuación, hacer clic en el botón **[Free Edition]**. En la siguiente pantalla, hacer clic en la opción **I accept the EULA** y luego en el botón **[Start Application]**. A continuación debería ejecutar la aplicación.

En Linux debe ser posible ejecutar el programa utilizando [Wine](https://www.winehq.org/).

## Plugin en Eclipse

A continuación se presentan las instrucciones para instalar y configurar un plugin para Eclipse que facilita la captura de una traza de ejecución y su visualización con Tracealyzer.

Copiar los archivos [`com.percepio.tracealyzer.core_1.0.6.v20180223734.jar`](resources/com.percepio.tracealyzer.core_1.0.6.v20180223734.jar) y [`com.percepio.tracealyzer.ui_1.0.6.v20180223734.jar`](resources/com.percepio.tracealyzer.ui_1.0.6.v20180223734.jar) en el directorio `eclipse/plugins`. Reiniciar Eclipse. Debería aparecer un nuevo menú **[Percepio]**.

### Configuración del Plugin
Hacer clic en el menú **[Percepio > Preferences]**. En la nueva ventana, configurar las siguientes opciones de la siguientes manera:

- *Tracealyzer Path*: indicar el path al ejecutable de Tracealyzer.
- *Version*: seleccionar *Tracealyzer 3.x or older*
- *Trace Directory*: indicar un directorio donde se guardaran por defecto las trazas generadas.
- *Trace Filename*: dejar en blanco para que genere un nuevo nombre para cada traza.
- *Same File Handling*: seleccionar *Ask every time*.
- *RTOS Type*: seleccionar *FreeRTOS* de la lista.
- Marcar la opción **[Automatically Suspend Target]**, si no lo está.

Luego, hacer clic en el botón **[Apply and Close]**.

### Capturar una traza
Luego de ejecutar un proyecto mediante un perfil de debugging, hacer clic en el menú **[Percepio > Save Snapshot Trace]**. Esto automáticamente guardará la traza en un archivo en el directorio especificado anteriormente y ejecutará Tracealyzer para inspeccionar la traza.
