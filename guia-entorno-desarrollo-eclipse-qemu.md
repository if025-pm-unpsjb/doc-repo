# Instalación entorno de desarrollo basado en Eclipse

Este documento es una guía de instalación y configuración de un entorno de desarrollo basado en [Eclipse](http://www.eclipse.org).

Tabla de Contenidos:

- [Carpeta de la cursada](#carpeta-de-la-cursada)
- [Eclipse](#descargar-eclipse)
- [Instalación](#instalacion-del-software-necesario)
- [Configuración](#configurar-eclipse)
- [Plugins adicionales](#plugins-adicionales)
- [pyOCD](#pyocd)
- [Configuración adicional](#configuracion-adicional)
- [Proyecto de prueba](#proyecto-de-prueba)

---

## Carpeta de la cursada

Crear una carpeta donde se descarga todo el software y material necesario para la cursada. En esta guía se asume que este directorio es `~/setr`.

Una vez creada la carpeta, crear dentro los directorios `~setr/workspace` y `~/setr/src`.

## Descargar Eclipse

Descargar la versión más reciente de [_GNU Eclipse IDE for Embedded C/C++_](https://www.eclipse.org/downloads/packages/release/2022-06/r/eclipse-ide-embedded-cc-developers) y descomprimir el archivo en `~/setr/eclipse`.

## Instalación del software necesario

Para esto hay dos opciones: generar una imagen docker con todo el software necesario o descargarlo manualmente.

### Docker

Seguir estos pasos para crear una imagen Docker que contiene todo el software necesario:

- Dentro de la carpeta `~/src`, clonar el repositorio [devenv](https://github.com/if025-pm-unpsjb/devenv).
- Luego, ejecutar el script `~/setr/src/devenv/mkenv.sh`.
- Verificar que se creo una imagen Docker con nombre `setr` ejecutando `docker images | grep setr`.

### Descarga manual

Si se desea no utilzar Docker, se puede descargar el software necesario paso a paso. Para evitar inconvenientes, realizar la instalación siguiendo las siguientes guías en el orden presentado y atendiendo a las aclaraciones indicadas. Se utilizaran en lo posible paquetes _stand-alone_ que no requieren instaladores. De esta manera, se evitan posibles conflictos con instalaciones previas y la actualización o eliminación del entorno es más sencilla.

Crear la carpeta `~/setr/tools`. Luego descargar y descomprimir en este directorio los siguientes programas:

- **Embedded Toolchain**: descargar la versión más reciente correspondiente a la plataforma que utilice (`linux-x64` o `win32-x64`) desde este [enlace](https://github.com/xpack-dev-tools/arm-none-eabi-gcc-xpack/releases) y descomprir en `setr/arm-none-eabi-gcc`.
- **Windows Build Tools**: este paquete solo es requerido para Windows. Descargar el archivo zip correspondiente a la versión de Windows que utilice (32 o 64 bits) desde este [enlace](https://github.com/xpack-dev-tools/windows-build-tools-xpack/releases/tag/v4.3.0-1) y descomprimir en `setr/windows-build-tools`.
- **QEMU**: descargar la versión más reciente desde [este enlace](https://github.com/xpack-dev-tools/qemu-arm-xpack/releases) o desde [este](https://qemu.weilnetz.de/w64/) si se utiliza Windows, y descomprimir en el directorio `setr\qemu`.
- **OpenOCD**: descargar la versión 0.11.0-4 desde [este enlace](https://github.com/xpack-dev-tools/openocd-xpack/releases/tag/v0.11.0-4) y descomprimir en el directorio `setr\openocd`.
- **Java**: es requerido para ejecutar Eclipse. Si no esta instalado, seguir la [guía de instalación de Java](https://eclipse-embed-cdt.github.io/plugins/prerequisites/) para su sistema operativo.

Debería quedar una estructura de directorios como la siguiente:
```
~/setr
├── eclipse                # Eclipse 
├── workspace              # Workspace para Eclipse
├── src                    # Aquí descargaremos los proyectos
└── tools                  # Aquí descargaremos los programas si seguimos la instalación manual
    ├── arm-none-eabi-gcc      # Toolchain (compilador, linker, librerias, etc.)
    ├── windows-build-tools    # Make y otras aplicaciones (solo necesario en Windows)
    ├── qemu                   # QEMU
    └── openocd                # OpenOCD
```

## Configurar Eclipse

Ejecutar Eclipse y cuando solicite la ubicación del _workspace_ indicar el directorio `workspace` anteriormente creado. Luego, abrir las preferencias de Eclipse (**[Window > Preferences]**) y:

- Ir a **[MCU]**:
  - En **[Global Arm Toolchains Paths]**:
    - En **Default Toolchain** seleccionar _xPack GNU Arm Embedded GCC_.
    - En **Toolchain folder** indicar el _path_ completo al directorio `setr/arm-none-eabi-gcc/bin`.
  - En **[Global OpenOCD Path]**:
    - En **Executable** debe decir `openocd`
    - En **Folder** indicar el _path_ completo al directorio `setr/openocd/bin`.
  - En **[Global QEMU Paths]**:
    - En **arm executable** debe decir `qemu-system-arm`
    - En **arm folder** indicar el _path_ completo al directorio `setr/qemu/bin`.
  - En **[Global Build Tool Path]** indicar el _path_ completo al directorio `setr/windows-build-tools/bin` (sólo necesario en Windows).
  - Hacer clic en **[Apply and Close]**.

- Aplicar también los siguientes cambios a la configuración:
    - [Use active build configuration for indexing](https://eclipse-embed-cdt.github.io/eclipse/workspace/preferences/#use-active-build-configuration-for-indexing)
    - [Save automatically](https://eclipse-embed-cdt.github.io/eclipse/workspace/preferences/#save-automatically)
    - [Text file encoding](https://eclipse-embed-cdt.github.io/eclipse/workspace/preferences/#text-file-encoding)
    - [Show line numbers](https://eclipse-embed-cdt.github.io/eclipse/workspace/preferences/#show-line-numbers)
    - [Build console](https://eclipse-embed-cdt.github.io/eclipse/workspace/preferences/#build-console)
    - [Debug previous application](https://eclipse-embed-cdt.github.io/eclipse/workspace/preferences/#debug-previous-application)

## Plugins adicionales

### FreeRTOS Task Aware Debugger

Plugin para Eclipse que permite obtener información acerca del estado de FreeRTOS en tiempo de ejecución, como por ejemplo el estado de las tareas, memoria utilizada, etc. Para instalarlo, seguir las instrucciones en esta [guía](eclipse-freertos-tad.md). Si se tiene la versión 2020-06 de EclipseCDT, descargar el archivo [com.nxp.freertos.gdb.tad_1.0.2.201704260904.jar](https://github.com/if025-pm-unpsjb/doc-repo/raw/master/resources/com.nxp.freertos.gdb.tad_1.0.2.201704260904.jar) y copiarlo dentro de la carpeta `plugins` de Eclipse. Reiniciar Eclipse desde `[File > Restart]`.

### Percepio Tracealyzer para FreeRTOS

[Tracealyzer para FreeRTOS](https://percepio.com/docs/FreeRTOS/manual/index.html#Tracealyzer_for_FreeRTOS) es una aplicación para realizar un seguimiento de la ejecución de sistemas basados en FreeRTOS, generando una traza que puede ser visualizada en línea o posteriormente. Para instalarlo y configurarlo, seguir la [siguiente guía](eclipse-tracealyzer.md).

## Reglas UDEV 

Este paso sólo es requerido en Linux. Seguir [estas instrucciones](https://github.com/mbedmicro/pyOCD/tree/main/udev) para modificar los permisos de acceso a los dispositivos USB mediante las reglas udev, copiando el archivo `50-cmsis-dap.rules` en `/etc/udev/rules.d`.

## pyOCD

[PyOCD](https://github.com/mbedmicro/pyOCD) es una librería para depurar programas sobre microcontroladores ARM Cortex-M mediante CMSIS-DAP y un servidor gdb.

### mbed LPC1768

Para trabajar con las placas mbed LPC1768, utilizaremos la versión 0.10 de PyOCD, ya que las versiones posteriores tiene problemas para conectarse con estas placas de desarrollo. Esta versión de PyOCD requiere el uso de Python 2.7.

En primer lugar verificar si esta instalado Python 2.7. En caso de no ser así, utilizar el administrador de paquetes de la distribución. Por ejemplo, para Ubuntu:
```
$ sudo apt install python2.7
```
A continuación, instalar `pip`:
```
$ wget https://bootstrap.pypa.io/pip/2.7/get-pip.py
$ python2.7 get-pip.py
```
Una vez que se tiene Python2.7 instalado, desde una línea de comandos, instalar `virtualenv`:
```
$ python2 -m pip install --upgrade virtualenv
```
Luego, vamos a crear un entorno desde donde ejecutaremos PyOCD. Ejecutar este comando en el directorio `setr`:
```
$ python2 -m virtualenv pyocd-0.10
```
A continuación, activamos el entorno. En Linux, ejecutar el siguiente comando:
```
$ source pyocd-0.10/bin/activate
```
En Windows, ejecutar este comando:
```
$ pyocd-0.10/Scripts/activate
```
Luego, la línea de comandos debe cambiar, indicando que estan ejecutando en el nuevo ambiente virtual. Para instalar pyOCD y la librería, ejecutar desde la linea de comandos:
```
(pyocd-0.10) $ pip install -U intervaltree==2.1.0 pyocd==0.10
```
Para verificar que se haya instalado correctamente el `pyocd-gdbserver`, ejecutar el siguiente comando desde una linea de comandos, para obtener la versión instalada:
```
(pyocd-0.10)$ pyocd-gdbserver --version
0.10.0
$
```

### FRDM-K64F y otras placas mbed

Para estas placas podemos utilizar la última versión de PyOCD. Recomendamos usar [`pipx`](https://pipx.pypa.io/stable/):
```
$ sudo apt install pipx
$ pipx ensurepath
$ pipx install pyocd
```

## Configuración adicional

### Acceso al puerto serial

En Linux, para poder leer y escribir en el puerto serial sin ser _root_, agregar el usuario al grupo `dialout`:
```
$ sudo adduser user dialout
```

## Prueba

Para probar que todo funcione correctamente, clonar o descargar en un subdirectorio de `src` alguno de los siguientes proyecto y seguir las instrucciones del README:

- [Proyecto de prueba para la placa LM3S6965](https://github.com/if025-pm-unpsjb/lm3s6965evb-helloworld-makefile)

- [Proyecto de prueba para la placa mbed LPC1768](https://github.com/if025-pm-unpsjb/mbed2-base-makefile)
 
