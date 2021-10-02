# Instalación entorno de desarrollo basado en Eclipse

Este documento es una guía de instalación y configuración de un entorno de desarrollo basado en [Eclipse](http://www.eclipse.org).

Tabla de Contenidos:

- [Instalación](#instalacion-del-software-necesario)
- [Configuración](#configurar-eclipse)
- [Plugins adicionales](#plugins-adicionales)
- [Proyecto de prueba](#proyecto-de-prueba)

---

## Instalación del software necesario

Para evitar inconvenientes, realizar la instalación siguiendo las siguientes guías en el orden presentado y atendiendo a las aclaraciones indicadas. Se utilizaran en lo posible paquetes _stand-alone_ que no requieren instaladores. De esta manera, se evitan posibles conflictos con instalaciones previas y la actualización o eliminación del entorno es más sencilla.

- Crear un directorio `setr` (por ejmplo `C:\setr` en Windows o `~/setr` en Linux) donde se van a alojar los programas y paquetes necesarios.
- **Java**: si no esta instalado, seguir la [guía de instalación de Java](https://eclipse-embed-cdt.github.io/plugins/prerequisites/) para su sistema operativo.
- **Embedded Toolchain**: seguir las [instrucciones de instalación manual](https://xpack.github.io/arm-none-eabi-gcc/install/#manual-install), pero descomprimiendo el archivo en `setr/arm-none-eabi-gcc`.
- **Windows Build Tools**: este paquete solo es requerido para Windows. Seguir las [instrucciones de instalación manual](https://xpack.github.io/windows-build-tools/install/#manual-install), pero descomprimiendo el archivo en `setr/windows-build-tools`.
- **Eclipse Embedded CDT**: descargar la versión más reciente de [_GNU Eclipse IDE for Embedded C/C++_](https://www.eclipse.org/downloads/packages/) y descomprimir el archivo en `setr\eclipse`.
- Crear los directorios `workspace` y `src` dentro de `setr`.

Una vez descargado los programas, debería quedar una estructura de directorios como la siguiente:
```
setr\
├── eclipse\                # Eclipse 
├── arm-none-eabi-gcc\      # Toolchain (compilador, linker, librerias, etc.)
├── windows-build-tools\    # Make y otras aplicaciones (solo necesario en Windows)
├── workspace\              # Workspace para Eclipse
└── src\                    # Aquí descargaremos los proyectos
```

## Configurar Eclipse

Ejecutar Eclipse y cuando solicite la ubicación del _workspace_ indicar el directorio `workspace` anteriormente creado. Luego, abrir las preferencias de Eclipse (**[Window > Preferences]**) y:

- Ir a **[MCU]**:
  - En **[Global Arm Toolchain path]**:
    - En **Default Toolchain** seleccionar _xPack GNU Arm Embedded GCC_.
    - En **Toolchain folder** indicar el _path_ completo al directorio `setr/arm-none-eabi-gcc/bin`.
  - En **[Global Build Tool Path]** indicar el _path_ completo al directorio `setr/windows-build-tools/bin` (sólo necesario en Windows).
  - Hacer clic en **[Apply and Close]**.
- A continuación, realizar la configuración adicional [indicada aquí](https://gnu-mcu-eclipse.github.io/eclipse/workspace/preferences).

## Plugins adicionales

### FreeRTOS Task Aware Debugger

Plugin para Eclipse que permite obtener información acerca del estado de FreeRTOS en tiempo de ejecución, como por ejemplo estado de las tareas, memoria utilizada, _timers_, etc. Para instalarlo, seguir las instrucciones en este sitio: [FreeRTOS Task Aware Debugger (TAD)](https://mcuoneclipse.com/2016/07/06/freertos-kernel-awareness-for-eclipse-from-nxp/).

### Percepio Tracealyzer para FreeRTOS

[Tracealyzer para FreeRTOS](https://percepio.com/docs/FreeRTOS/manual/index.html#Tracealyzer_for_FreeRTOS) es una aplicación para realizar un seguimiento de la ejecución de sistemas basados en FreeRTOS, generando una traza que puede ser visualizada en línea o posteriormente. Para instalarlo y configurarlo, seguir la [siguiente guía](eclipse-tracealyzer.md).

## QEMU

Instalar QEMU (un emulador y virtualizador de distintas plataformas):

- **Windows**: descargar e instalar la última versión desde [este enlace](https://qemu.weilnetz.de/w64/) (versión de 64 bits).
- **Linux**: seguir las indicaciones en la [página de instalación](https://www.qemu.org/download/#linux) según la distribución.

## Prueba

Para probar que todo funcione correctamente, clonar o descargar en un subdirectorio de `src` el siguiente proyecto y seguir las instrucciones:

- [Proyecto de prueba para la placa LM3S6965](https://github.com/if025-pm-unpsjb/lm3s6965evb-helloworld-makefile)
