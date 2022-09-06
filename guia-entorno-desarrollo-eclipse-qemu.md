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

- Crear un directorio `setr` (por ejemplo `C:\setr` en Windows o `~/setr` en Linux) donde se van a alojar los programas y paquetes necesarios.
- **Embedded Toolchain**: descargar el archivo `.zip` correspondiente a la plataforma que utilice (`linux-x64` o `win32-x64`) desde este [enlace](https://github.com/xpack-dev-tools/arm-none-eabi-gcc-xpack/releases/tag/v11.3.1-1.1) y descomprir en `setr/arm-none-eabi-gcc`.
- **Windows Build Tools**: este paquete solo es requerido para Windows. Descargar el archivo zip correspondiente a la versión de Windows que utilice (32 o 64 bits) desde este [enlace](https://github.com/xpack-dev-tools/windows-build-tools-xpack/releases/tag/v4.3.0-1) y descomprimir en `setr/windows-build-tools`.
- **Eclipse Embedded CDT**: descargar la versión más reciente de [_GNU Eclipse IDE for Embedded C/C++_](https://www.eclipse.org/downloads/packages/) y descomprimir el archivo en `setr\eclipse`.
- **Java**: es requerido para ejecutar Eclipse. Si no esta instalado, seguir la [guía de instalación de Java](https://eclipse-embed-cdt.github.io/plugins/prerequisites/) para su sistema operativo.
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

- Aplicar también los siguientes cambios a la configuración: [indicada aquí]
    - [Use active build configuration for indexing](https://eclipse-embed-cdt.github.io/eclipse/workspace/preferences/#use-active-build-configuration-for-indexing)
    - [Save automatically](https://eclipse-embed-cdt.github.io/eclipse/workspace/preferences/#save-automatically)
    - [Text file encoding](https://eclipse-embed-cdt.github.io/eclipse/workspace/preferences/#text-file-encoding)
    - [Show line numbers](https://eclipse-embed-cdt.github.io/eclipse/workspace/preferences/#show-line-numbers)
    - [Build console](https://eclipse-embed-cdt.github.io/eclipse/workspace/preferences/#build-console)
    - [Debug previous application](https://eclipse-embed-cdt.github.io/eclipse/workspace/preferences/#debug-previous-application)

## Plugins adicionales

### FreeRTOS Task Aware Debugger

Plugin para Eclipse que permite obtener información acerca del estado de FreeRTOS en tiempo de ejecución, como por ejemplo el estado de las tareas, memoria utilizada, etc. Para instalarlo, seguir las instrucciones en esta [guía](eclipse-freertos-tad.md). 

### Percepio Tracealyzer para FreeRTOS

[Tracealyzer para FreeRTOS](https://percepio.com/docs/FreeRTOS/manual/index.html#Tracealyzer_for_FreeRTOS) es una aplicación para realizar un seguimiento de la ejecución de sistemas basados en FreeRTOS, generando una traza que puede ser visualizada en línea o posteriormente. Para instalarlo y configurarlo, seguir la [siguiente guía](eclipse-tracealyzer.md).

## QEMU

Instalar QEMU (un emulador y virtualizador de distintas plataformas):

- **Windows**: descargar e instalar la última versión desde [este enlace](https://qemu.weilnetz.de/w64/) (versión de 64 bits).
- **Linux**: se puede instalar mediante el administrador de paquetes de la distribución. Por ejemplo, en Ubuntu:

```
$ sudo apt install qemu-system-arm 
```

Para otras distribuciones, seguir las indicaciones en la [página de instalación](https://www.qemu.org/download/#linux). 

## Prueba

Para probar que todo funcione correctamente, clonar o descargar en un subdirectorio de `src` el siguiente proyecto y seguir las instrucciones:

- [Proyecto de prueba para la placa LM3S6965](https://github.com/if025-pm-unpsjb/lm3s6965evb-helloworld-makefile)
