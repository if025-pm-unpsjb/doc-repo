# Instalar y configurar plugin FreeRTOS Kernel Awareness

Ir al menú **[Help > Install New Software]** en Eclipse. En la ventana que aparece a continuación, en el campo *Work with:* copiar y pegar la siguiente URL:

```
http://freescale.com/lgfiles/updates/Eclipse/KDS
```

Luego, hacer clic en el botón **[Add...]** y en la ventana *Add Repository* que aparece, en el campo *Name:* ingresar "FreeRTOS TAD" (sin las comillas). El campo *"Location"* debería tener la URL ingresada anteriormente. Luego, hacer clic en el botón **[Add]**.

En la ventana de instalación de componentes, debe aparecer ahora una lista de componentes. Expandir el item llamado *FreeRTOS plug-ins* y seleccionar *FreeRTOS Task Aware Debugger for GDB*. Luego, hacer clic en **[Next >]**.

En la siguiente pantalla se presenta un resumen de los componentes a instalar, donde debería aparecer *FreeRTOS Task Aware Debugger for GDB*. Hacer clic en el botón **[Next >]**.

En la siguiente pantalla, se presenta la licencia del componente. Hacer clic en la opción **I accept the terms of the license agreement** y luego hacer clic en el botón **[Finish]**.

Eclipse debería empezar a instalar el componente en segundo plano, y en la esquina inferior derecha se indica el avance. Una vez finalizada la instalación, Eclipse preguntará si se desea reiniciar el IDE, hacer clic en el botón **[Restart now]**.

Luego que reinicie Eclipse, debería aparecer un nuevo menú **[FreeRTOS]** en la perspectiva de _debugging_.

Otra guía de instalación (en inglés):[FreeRTOS Task Aware Debugger (TAD)](https://mcuoneclipse.com/2016/07/06/freertos-kernel-awareness-for-eclipse-from-nxp/).


