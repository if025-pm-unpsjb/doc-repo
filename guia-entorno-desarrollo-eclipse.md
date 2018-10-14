# Instalación entorno de desarrollo basado en Eclipse
Esta documento presenta una una guía de instalación y configuración de un entorno de desarrollo basado en [Eclipse](http://www.eclipse.org).

Tabla de Contenidos:
- [GNU MCU Eclipse](#gnu-mcu-eclipse)
- [Plug-ins adicionales](#plug-ins-adicionales)
- [Percepio Tracealyzer para FreeRTOS](#percepio-tracealyzer-para-freertos)
- [pyOCD](#pyocd)
- [Git](#git)
- [Proyecto de prueba](#proyecto-de-prueba)

---

## GNU MCU Eclipse
Como primer paso, se instalará Eclipse CDT, el GNU ARM Embedded Toolchain, Windows Build Tools (si se utiliza Windows), Java (en caso de no estar ya instalado), y la serie de extensiones [GNU MCU Eclipse](https://gnu-mcu-eclipse.github.io/) (anteriormente denominadas GNU ARM Eclipse).

Para evitar inconvenientes o demoras, recomendamos realizar una instalación siguiendo estas guías en este orden, y con las aclaraciones indicadas:
* [GNU ARM Embedded Toolchain](https://gnu-mcu-eclipse.github.io/toolchain/arm/install/). Descargar la versión más reciente distribuida por el proyecto, y seguir las instrucciones en la sección [Manual install](https://gnu-mcu-eclipse.github.io/toolchain/arm/install/#manual-install).
* [Windows Build Tools](https://gnu-mcu-eclipse.github.io/windows-build-tools/install/) (requerido sólo para Windows). Seguir las instrucciones en la sección [Manual install](https://gnu-mcu-eclipse.github.io/windows-build-tools/install/#manual-install).
* [OpenOCD](https://gnu-mcu-eclipse.github.io/openocd/install). Seguir las instrucciones en [Manual install](https://gnu-mcu-eclipse.github.io/openocd/install/#manual-install).
* [Eclipse CDT](https://gnu-mcu-eclipse.github.io/plugins/install/). Descargar la versión más reciente de _GNU MCU Eclipse IDE for C/C++ Developers_ distribuida por el proyecto, que contiene los plug-ins necesarios.
* [GNU ARM Eclipse Plug-ins](https://gnu-mcu-eclipse.github.io/plugins/install/)
* [Configuración adicional del workspace](https://gnu-mcu-eclipse.github.io/eclipse/workspace/preferences) (aunque no es obligatorio, es recomendado)

No es necesario por el momento realizar los pasos para instalar SEGGER J-Link o QEMU.

Si se desea realizar otra configuración, por ejemplo utilizar una versión de Eclipse ya instalada, recomendamos seguir **paso a paso** la guía de instalación de [GNU MCU Eclipse](https://gnu-mcu-eclipse.github.io/install/).

---

## Plug-ins adicionales
Instalar los siguientes plugins:
* [FreeRTOS Task Aware Debugger (TAD)](https://mcuoneclipse.com/2016/07/06/freertos-kernel-awareness-for-eclipse-from-nxp/) de NXP.
* [Percepio FreeRTOS Tracealyzer Plugin](https://percepio.com/docs/FreeRTOS/manual/Recorder.html#eclipse). Consultar esta [guía](https://mcuoneclipse.com/2017/03/08/percepio-freertos-tracealyzer-plugin-for-eclipse/) para información adicional.

---

## Percepio Tracealyzer para FreeRTOS
Instalar la aplicación [Percepio Tracealyzer para FreeRTOS](https://percepio.com/tz/freertostrace/):
* Para Windows ofrece un instalador.
* Para Linux / MacOS, un paquete `tar.gz`.

---

## pyOCD

PyOCD es una librería para programar y depurar programas sobre microcontroladores ARM Cortex-M mediante CMSIS-DAP. Esta librería puede se utilizada como reemplazo de OpenOCD con placas mbed. Además, integra un servidor GDB.

La librería requiere Python 2.7 (no soporta Python 3). Si no esta ya instalado, descargar la última versión de Python 2.7 desde [www.python.org](http://www.python.org). Durante la instalación, seleccionar la opción **[Add to path]**, o agregar posteriormente el directorio de instalación al *path* del sistema.

Para verificar que Python ha sido instalado correctamente, ejecutar el siguiente comando desde una linea de comandos, para obtener la versión instalada:
```
$ python --version
Python 2.7.10
$
```
Luego, para instalar pyOCD, ejecutar desde una linea de comandos:
```
$ pip install -U pyocd
```
Para verificar que se haya instalado correctamente el `pyocd-gdbserver`, ejecutar el siguiente comando desde una linea de comandos, para obtener la versión instalada:
```
$ pyocd-gdbserver --version
0.12.0
$
```

---

## Git
Descargar Git desde [https://git-scm.com](https://git-scm.com) e instalarlo.

Se puede utilizar la interfaza gráfica `git-gui` ya incluida con Git, o seleccionar algún [cliente de terceros](https://git-scm.com/downloads/guis).

En esta guía solo se utilizarán comandos básicos de Git. Se pueden consultar estos tutoriales para conocer con más detalle su operación:
* Git in 15 minutes: [https://try.github.io/](https://try.github.io/)
* Colección de tutoriales: [https://www.atlassian.com/git/tutorials](https://www.atlassian.com/git/tutorials)
* Git Tutorial: [https://git-scm.com/docs/gittutorial](https://git-scm.com/docs/gittutorial)
* Pro Git book: [https://book.git-scm.com/book/en/v2](https://book.git-scm.com/book/en/v2)

---

## Proyecto de prueba
* Para probar que todo funcione correctamente, importar y compilar el [proyecto de prueba para la placa LPC1768](https://github.com/if025-pm-unpsjb/mbed-blinky-makefile).

---

Eso sería todo :)
