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

Crear una carpeta donde se descarga todo el software y material necesario para la cursada. En esta guía se asume que este directorio es `~/setr`. Dentro de esta carpeta, se espera tener los directorios `~setr/workspace`, `~/setr/src` y `~/setr/tools`:

```sh
$ mkdir -p ~/setr ~/setr/workspace ~/setr/src ~/setr/tools
```

## Descargar Eclipse

Descargar la versión más reciente de [_GNU Eclipse IDE for Embedded C/C++_](https://www.eclipse.org/downloads/packages/release/2022-06/r/eclipse-ide-embedded-cc-developers) y descomprimir el archivo en `~/setr/eclipse`.

Java es necesario para ejecutar Eclipse. Si no esta instalado, seguir la [guía de instalación de Java](https://eclipse-embed-cdt.github.io/plugins/prerequisites/) para su sistema operativo.

## Instalación del software necesario

Para esto hay dos opciones: generar una imagen docker con todo el software necesario o descargarlo manualmente.

### Docker

Seguir estos pasos para crear una imagen Docker que contiene todo el software necesario:

- Dentro de la carpeta `~/src`, clonar el repositorio [devenv](https://github.com/if025-pm-unpsjb/devenv).
- Luego, ejecutar el script `~/setr/src/devenv/mkenv.sh`.
- Verificar que se creo una imagen Docker con nombre `setr` ejecutando `docker images | grep setr`.

### Descarga manual

Para evitar inconvenientes, realizar la instalación siguiendo las siguientes guías en el orden presentado y atendiendo a las aclaraciones indicadas. Se utilizaran en lo posible paquetes _stand-alone_ que no requieren instaladores. De esta manera, se evitan posibles conflictos con instalaciones previas y la actualización o eliminación del entorno es más sencilla.

Descargar y descomprimir en el directorio `~/setr/tools` los siguientes programas:

- **Embedded Toolchain**: descargar la versión más reciente correspondiente a la plataforma que utilice (`linux-x64` o `win32-x64`) desde este [enlace](https://github.com/xpack-dev-tools/arm-none-eabi-gcc-xpack/releases) y descomprir en `~/setr/tools/arm-none-eabi-gcc`.
- **Windows Build Tools**: este paquete solo es requerido para Windows. Descargar el archivo zip correspondiente a la versión de Windows que utilice (32 o 64 bits) desde este [enlace](https://github.com/xpack-dev-tools/windows-build-tools-xpack/releases/tag/v4.3.0-1) y descomprimir en `~/setr/tools/windows-build-tools`.
- **QEMU**: descargar la versión más reciente desde [este enlace](https://github.com/xpack-dev-tools/qemu-arm-xpack/releases) o desde [este](https://qemu.weilnetz.de/w64/) si se utiliza Windows, y descomprimir en el directorio `~/setr/tools/qemu`.
- **OpenOCD**: descargar la versión 0.11.0-4 desde [este enlace](https://github.com/xpack-dev-tools/openocd-xpack/releases/tag/v0.11.0-4) y descomprimir en el directorio `~/setr/tools/openocd`.

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

Ejecutar Eclipse y cuando solicite la ubicación del _workspace_ indicar el directorio `~/setr/workspace`. Luego, abrir las preferencias de Eclipse (**[Window > Preferences]**) y:

- Ir a **[MCU]**:
  - En **[Global Arm Toolchains Paths]**:
    - En **Default Toolchain** seleccionar _xPack GNU Arm Embedded GCC_.
    - En **Toolchain folder** indicar el _path_ completo al directorio `~/setr/tools/arm-none-eabi-gcc/bin`.
  - En **[Global OpenOCD Path]**:
    - En **Executable** debe decir `openocd`
    - En **Folder** indicar el _path_ completo al directorio `~/setr/tools/openocd/bin`.
  - En **[Global QEMU Paths]**:
    - En **arm executable** debe decir `qemu-system-arm`
    - En **arm folder** indicar el _path_ completo al directorio `~setr/tools/qemu/bin`.
  - En **[Global Build Tool Path]** indicar el _path_ completo al directorio `~/setr/tools/windows-build-tools/bin` (sólo necesario en Windows).
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

Este paso sólo es requerido en Linux. Seguir [estas instrucciones](https://github.com/pyocd/pyOCD/tree/main/udev) para modificar los permisos de acceso a los dispositivos USB mediante las reglas udev, copiando el archivo `50-cmsis-dap.rules` en `/etc/udev/rules.d`.

## pyOCD

[PyOCD](https://github.com/mbedmicro/pyOCD) es una librería para depurar programas sobre microcontroladores ARM Cortex-M mediante CMSIS-DAP y un servidor gdb. Recomendamos usar [`pipx`](https://pipx.pypa.io/stable/) para instalarlo:
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
 
