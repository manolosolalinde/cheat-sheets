# INSTALACION EN WINDOWS

## PASO 1 COMPILACION

Descargar archivo .exe de https://opencv.org/releases/ (WINDOWS) (opencv-4.1.0-vc14_vc15.exe)

Ejecutar el archivo colocando todo en la carpeta: `E:\LIBRERIAS\opencv-4.1.0`

### Alternativa

    Instalar Opencv usando cmake-gui 
    build: `E:\LIBRERIAS\opencv-4.0.0\build-windows` 
    source: `E:\LIBRERIAS\opencv-4.0.0\` 
    Platform: Visual Studio 2017 x64 
    Luego: Desde OpenCV.sln -> Compilar ALLBuild en release 
    ========== Build: 82 succeeded, 0 failed, 0 up-to-date, 0 skipped ========== 
    -> Compilar Install en release 
    ========== Build: 2 succeeded, 0 failed, 81 up-to-date, 0 skipped ========== 
    Se crea la carpeta `E:\LIBRERIAS\opencv-4.0.0\build-windows\install ` 
    Nota: Compilar en debug mode no funciona porque requiere python36_d.lib que no se instala con anaconda.
    Nota: Incluir en la configuracion `opencv_world` para referirse a una sola libreria en lugar de varias.

## PASO 2 DEFINIR VARIABLES DE ENTORNO:

Editar la variable de sistema "Path" -> Agregar: `E:\LIBRERIAS\opencv-4.1.0\build\x64\vc15\lib` \
                                                y `E:\LIBRERIAS\opencv-4.1.0\build\x64\vc15\bin`

### Alternativa:

    Crear una variable del sistema: OPENCV_DIR=E:\LIBRERIAS\opencv-4.0.0\build-windows\install\x64\vc15
    Editar la variable de sistema "Path" -> Agregar: `%OPENCV_DIR%\lib` y `%OPENCV_DIR%\bin`

## PASO 3 CONFIGURAR PROJECTO DE OPENCV c++ EN VISUAL STUDIO

- Crear projecto en Visual Studio -> Nuevo projecto vacio de c++
- Crear o incluir un archivo c++ en el projecto
- Ir a propiedades de proyecto -> C/C++ -> General -> Directorios de inclusion adicionales -> Incluir `E:\LIBRERIAS\opencv-4.1.0\build\include`
- Propiedades de proyecto -> Vinculador -> General -> Directorios de bibliotecas adicionales -> Incluir `E:\LIBRERIAS\opencv-4.1.0\build\x64\vc15\lib`
- Propiedades de proyecto -> Vinculador -> General -> Entrada -> Dependencias adicionales -> Incluir `opencv_world410.lib` `opencv_world410d.lib`

Nota: Esta creado un template para proyectos OPENCV 4.1.0 en Proyecto OpenCV 4.1.0 C++1

# CORRER EJEMPLOS

    Preconfigurado variables de entorno: (agregado cl.exe a path y VisualStudioVersion=15.0)
    En cmd ejecutar: `cd E:\LIBRERIAS\opencv-4.1.0\sources\samples`
    Ejecutar archivo: `_winpack_build_sample.cmd cpp\create_mask.cpp`
    Se crea un proyecto de Visual Studio en `E:\LIBRERIAS\opencv-4.1.0\sources\samples\cpp\build_create_mask`
    Nota: En Visual Studio, Ir a Proyecto -> propiedades -> Depuracion -> Directorio de Trabajo modificar a $(TargetDir). Revisar el comando.


