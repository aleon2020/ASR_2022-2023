# Arquitectura Software para Robots 2022-2023

¡Bienvenido! En este repositorio se encuentran todos los materiales correspondientes a la asignatura de Arquitectura Software para Robots.

Parte del material que se encuentra subido a este repositorio nos ha sido proporcionado por Francisco Martín Rico, profesor encargado de impartir esta asignatura y coordinador del Grado en Ingeniería de Robótica Software de la Universidad Rey Juan Carlos de Fuenlabrada. A continuación se indican los enlaces correspondientes a todos estos materiales:

Enlace a docencia-fmrico, donde se encuentran repositorios relacionados con ROS2:

[REPOSITORIOS DE ROS2](https://github.com/Docencia-fmrico)

[PAQUETES ROS2 UTILIZADOS EN LA ASIGNATURA](https://github.com/fmrico/book_ros2)

A continuación se detallan brevemente todos los contenidos que se encuentran en este repositorio, con el objetivo de facilitar la preparación del examen final de la asignatura (muchos de ellos se obvian por la clara evidencia en su nombre).

IMPORTANTE: SI OBSERVAS QUE HAY ALGÚN ERROR O ALGO QUE FALTE EN ALGÚN ARCHIVO SUBIDO A ESTE REPOSITORIO (O SI HAY ALGUNA DUDA EN CUANTO A COMPRENSIÓN), DÉJAME UN ISSUE Y TRATARÉ DE RESOLVER EL PROBLEMA LO ANTES POSIBLE. NO TE OLVIDES DEJARME UNA STAR Y ESPERO QUE TODO ESTE MATERIAL TE SEA DE GRAN AYUDA.

## 1. Resumen de los contenidos de teoría

Fichero ['Resumen Teoría ASR.pdf'](https://github.com/aleon2020/ASR_2022-2023/blob/main/Resumen%20Teor%C3%ADa%20ASR.pdf): Resumen de teoría en formato PDF.

IMPORTANTE: Para hacer uso del índice interactivo que viene implementado en el resumen, debes descargar el documento en formato PDF.

## 2. Mini-tests realizados en clase y examen final

Ficheros ['Preguntas Test 1.pdf'](https://github.com/aleon2020/ASR_2022-2023/blob/main/Preguntas%20Test%201.pdf) y ['Preguntas Test 2.pdf'](https://github.com/aleon2020/ASR_2022-2023/blob/main/Preguntas%20Test%201.pdf): Contiene todas las preguntas de los dos mini-tests realizados en momentos intermedios del curso.

Directorio ['Enunciado examen final'](https://github.com/aleon2020/ASR_2022-2023/tree/main/Enunciado%20examen%20final): Contiene el enunciado del examen final de la asignatura, se compone de 2 preguntas, una más teórica y otra más relacionada con las prácticas realizadas a lo largo del curso.

## 3. Paquetes y prácticas

Directorio ['Paquetes'](https://github.com/aleon2020/ASR_2022-2023/tree/main/Paquetes): Contiene todos los paquetes de ejemplo vistos en clase a lo largo de la asignatura.

Directorio ['Prácticas'](https://github.com/aleon2020/ASR_2022-2023/tree/main/Pr%C3%A1cticas): Contiene todas las prácticas realizadas a lo largo de la asignatura.

## 4. Activación de ROS2 en los laboratorios de la universidad

Abre una terminal EN TU HOME y ejecuta los siguientes comandos:

```sh
$ nano ./bashrc
```

Dentro del archivo escribe la siguiente línea: 

```sh
source /opt/ros/humble/setup.bash
```

Guarda y cierra el fichero, y cierra la terminal (de esta forma se guarda todo lo incluido en el bashrc).

Abre una nueva terminal y comprueba que ROS2 funciona correctamente ejecutando el siguiente comando:

```sh
$ ros2
```

## 5. Creación de un workspace, uso y ejecución de un paquete

### 5.1 Creación y activación de un workspace

Es recomendable abrir la terminal desde el HOME (carpeta personal).

```sh
$ mkdir -p <my_workspace>/src
$ cd <my_workspace>/src/
$ git clone https://github.com/fmrico/book_ros2.git
$ cd ..
$ colcon build --symlink-install
$ source install/setup.sh
```
Ejemplo de ejecucion de programa una vez realizado lo anterior:

```sh
$ ros2 run br2_basics logger
```

### 5.2 Creación y ejecución de un paquete

```sh
$ cd ~/<my_workspace>/src
$ ros2 pkg create <my_package> --dependencies <dependencies>
```

Una vez hemos desarrollado nuestro paquete (programas, CMake, etc), realizamos lo siguiente:

```sh
$ cd ~/<my_workspace>
$ colcon build --symlink-install // colcon build --packages-select <my_package>
$ source install/setup.sh
$ ros2 run <my_package> <executable>
```
