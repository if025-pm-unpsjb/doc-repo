# Instalar y configurar Percepio Tracealyzer

## Instalar Percepio Tracealyzer

Descargar la versión Tracealyzer desde este [link](https://percepio.com/downloads/TzForFreeRTOS-3.1.2.tgz). Vamos a emplear la versión **3.1.2** ya que las versiones más recientes de Tracealyzer requieren registrarse y no ofrecen una versión gratuita de prueba. Descomprimir el archivo en `setr/tracealyzer`. 

Para comprobar que funciona correctamente, ejecutar el archivo `TzForFreeRTOS.exe`. En la ventana que aparece a continuación, hacer clic en el botón **[Free Edition]**. En la siguiente pantalla, hacer clic en la opción **I accept the EULA** y luego en el botón **[Start Application]**. A continuación debería ejecutar la aplicación.

En Linux debe ser posible ejecutar el programa utilizando [Wine](https://www.winehq.org/).

## Plugin en Eclipse

A continuación se presentan las instrucciones para instalar y configurar un plugin para Eclipse que facilita la captura de una traza de ejecución y su visualización con Tracealyzer.

En primer lugar, ir al menú **[Help > Install New Software]** en Eclipse. En la ventana que aparece a continuación, en el campo *Work with:* copiar y pegar la siguiente URL: http://percepio.com/exporter. Hacer clic en el botón **[Add...]** y, en la ventana *Add Repository* que aparece, en el campo *Name:* ingresar "Percepio" (sin las comillas). El campo *"Location"* debería tener la URL ingresada anteriormente. Luego, hacer clic en el botón **[Add]**.

Nuevamente en la ventana de instalación de componentes, en el area inferior debería aparecer ahora una entrada de nombre *Percepio*. Hacer clic en el símbolo **>** para expandir las opciones. Debería aparecer *Percepio Trace Exporter*. Seleccionarlo y luego hacer clic en el botón **[Next >]**.

En la siguiente pantalla se presenta un resumen de los componentes a instalar, donde debería aparecer *Percepio Trace Exporter*. Hacer clic en el botón **[Next >]**.

En la siguiente pantalla, se presenta la licencia del componente. Hacer clic en la opción **I accept the terms of the license agreement** y luego hacer clic en el botón **[Finish]**.

Eclipse debería empezar a instalar el componente en segundo plano, y en la esquina inferior derecha se indica el avance. Una vez finalizada la instalación, Eclipse preguntará si se desea reiniciar el IDE, hacer clic en el botón **[Restart now]**.

Luego que reinicie Eclipse, debería aparecer un nuevo menú **[Percepio]**.

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
