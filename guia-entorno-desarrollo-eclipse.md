# Instalación entorno de desarrollo basado en Eclipse
Esta documento presenta una una guía de instalación y configuración de un entorno de desarrollo basado en [Eclipse](http://www.eclipse.org).

Tabla de Contenidos:
- [Instalación entorno de desarrollo basado en Eclipse](#instalaci%c3%b3n-entorno-de-desarrollo-basado-en-eclipse)
  - [GNU MCU Eclipse](#gnu-mcu-eclipse)
  - [FreeRTOS Task Aware Debugger](#freertos-task-aware-debugger)
  - [Percepio Tracealyzer para FreeRTOS](#percepio-tracealyzer-para-freertos)
    - [Plugin para Eclipse](#plugin-para-eclipse)
  - [pyOCD](#pyocd)
  - [Git](#git)
  - [Proyecto de prueba](#proyecto-de-prueba)

---

## GNU MCU Eclipse
Como primer paso, se instalará Eclipse CDT, el GNU ARM Embedded Toolchain, Windows Build Tools (si se utiliza Windows), Java (en caso de no estar ya instalado), y la serie de extensiones [GNU MCU Eclipse](https://gnu-mcu-eclipse.github.io/) (anteriormente denominadas GNU ARM Eclipse).

Para evitar inconvenientes, recomendamos realizar la instalación siguiendo las siguientes guías, en el orden presentado, y atendiendo a las aclaraciones indicadas. De esta manera, se instalarán los programas necesarios utilizando las versiones que ofrece GNU MCU Eclipse, empleando, siempre que sea posible, los paquetes _stand-alone_, que no requieren instaladores. De esta manera, se evitan posibles conflictos con instalaciones previas, y es más sencilla la actualización o eliminación del entorno.

Guias de instalación a seguir:
* [GNU ARM Embedded Toolchain](https://gnu-mcu-eclipse.github.io/toolchain/arm/install/). Seguir las instrucciones en la sección [Manual install](https://gnu-mcu-eclipse.github.io/toolchain/arm/install/#manual-install), instalando la versión más reciente distribuida por el proyecto.
* [Windows Build Tools](https://gnu-mcu-eclipse.github.io/windows-build-tools/install/) (requerido sólo para Windows). Seguir las instrucciones en la sección [Manual install](https://gnu-mcu-eclipse.github.io/windows-build-tools/install/#manual-install).
* [OpenOCD](https://gnu-mcu-eclipse.github.io/openocd/install). Seguir las instrucciones en [Manual install](https://gnu-mcu-eclipse.github.io/openocd/install/#manual-install).
* [QEMU](https://gnu-mcu-eclipse.github.io/qemu/install/). Seguir las instrucciones en [Manual install](https://gnu-mcu-eclipse.github.io/qemu/install/#manual-install).
* [Eclipse CDT](https://gnu-mcu-eclipse.github.io/plugins/install/). Descargar la versión más reciente de _GNU MCU Eclipse IDE for C/C++ Developers_ distribuida por el proyecto, que contiene los plug-ins necesarios.
* [Configuración adicional del workspace](https://gnu-mcu-eclipse.github.io/eclipse/workspace/preferences) (aunque no es obligatorio, es recomendado)

_Nota_: No es necesario por el momento realizar los pasos para instalar SEGGER J-Link.

Si se desea realizar la instalación de otra manera, por ejemplo utilizando una versión de Eclipse que ya se tenga instalada, recomendamos seguir **paso a paso** la guía de instalación de [GNU MCU Eclipse](https://gnu-mcu-eclipse.github.io/install/).

---

## FreeRTOS Task Aware Debugger
Plugin para Eclipse que permite obtener información acerca del estado de FreeRTOS en tiempo de ejecución, como por ejemplo estado de las tareas, memoria utilizada, _timers_, etc.

Para instalarlo, seguir las instrucciones en este sitio: [FreeRTOS Task Aware Debugger (TAD)](https://mcuoneclipse.com/2016/07/06/freertos-kernel-awareness-for-eclipse-from-nxp/).

---

## Percepio Tracealyzer para FreeRTOS
[Tracealyzer para FreeRTOS](https://percepio.com/docs/FreeRTOS/manual/index.html#Tracealyzer_for_FreeRTOS) es una aplicación para realizar un seguimiento de la ejecución de sistemas basados en FreeRTOS, generando una traza que puede ser visualizada en línea o posteriormente.

Descarga la aplicación desde [la página de Percepio](https://percepio.com/tz/freertostrace/), e instalarla. Para Windows ofrece un instalador, y para Linux / MacOS, un paquete `tar.gz` con los ejecutables correspondientes.

### Plugin para Eclipse
Esta herramienta ofrece también un plugin para Eclipse que facilita generar trazas desde una sesión de _debug_. Para instalarlo, seguir cualquiera de las siguientes guía de instalación:
* [Percepio FreeRTOS Tracealyzer Plugin](https://percepio.com/docs/FreeRTOS/manual/Recorder.html#eclipse)
* [Percepio FreeRTOS Tracealyzer for Eclipse](https://mcuoneclipse.com/2017/03/08/percepio-freertos-tracealyzer-plugin-for-eclipse/)

---

## pyOCD

[PyOCD](https://github.com/mbedmicro/pyOCD) es una librería para depurar programas sobre microcontroladores ARM Cortex-M mediante CMSIS-DAP y un servidor gdb. Puede se utilizada como reemplazo de OpenOCD, al momento de trabajar con placas mbed. Require Python 2.7.9 o Python 3.6.0, o posterior.

Utilizaremos la versión 0.10 de PyOCD, ya que con las posteriores se han encontrado problemas para trabajar con las placas mbed LPC1768. Como PyOCD requiere la librería IntervalTree, también con una versión específica, vamos a crear un entorno virtual de Python, para no introducir problemas en la instalación del sistema.

Primero, desde una línea de comandos, instalar `virtualenv`:
```
$ pip install --upgrade virtualenv
```
Luego, vamos a crear un entorno desde donde ejecutaremos PyOCD:
```
$ virtualenv pyocd-python
```
A continuación, activamos el entorno. En Linux, ejecutar el siguiente comando:
```
$ source pyocd-python/bin/activate
```
En Windows, ejecutar este comando:
```
$ pyocd-python/Scripts/activate
```
Luego, la línea de comandos debe cambiar, indicando que estan ejecutando en el nuevo ambiente virtual. Para instalar pyOCD y la librería, ejecutar desde la linea de comandos:
```
(pyocd-python) $ pip install -U intervaltree==2.1.0 pyocd==0.10
```
Para verificar que se haya instalado correctamente el `pyocd-gdbserver`, ejecutar el siguiente comando desde una linea de comandos, para obtener la versión instalada:
```
(pyocd-python)$ pyocd-gdbserver --version
0.10.0
$
```

---

## Git
Descargar Git desde [https://git-scm.com](https://git-scm.com) e instalarlo.

Se puede utilizar la interfaza gráfica `git-gui` ya incluida con Git, o seleccionar algún [cliente de terceros](https://git-scm.com/downloads/guis).

Se pueden consultar estos tutoriales para aprender más acerca de Git:
* Git in 15 minutes: [https://try.github.io/](https://try.github.io/)
* Colección de tutoriales: [https://www.atlassian.com/git/tutorials](https://www.atlassian.com/git/tutorials)
* Git Tutorial: [https://git-scm.com/docs/gittutorial](https://git-scm.com/docs/gittutorial)
* Pro Git book: [https://book.git-scm.com/book/en/v2](https://book.git-scm.com/book/en/v2)

---

## Proyecto de prueba
Para probar que todo funcione correctamente, probar alguno de los siguientes proyectos:
* [Proyecto de prueba para la placa LPC1768](https://github.com/if025-pm-unpsjb/mbed-blinky-makefile).
* [Proyecto de prueba para la placa EDU-CIAA-NXP](https://github.com/if025-pm-unpsjb/ciaa-example-makefile).
