# Arquitectura Software para Robots 2022-2023

¡Bienvenido! En este repositorio se encuentran todos los materiales correspondientes a la asignatura de Arquitectura Software para Robots.

Parte del material que se encuentra subido a este repositorio nos ha sido proporcionado por Francisco Martín Rico, profesor encargado de impartir esta asignatura y coordinador del Grado en Ingeniería de Robótica Software de la Universidad Rey Juan Carlos de Fuenlabrada. A continuación se indican los enlaces correspondientes a todos estos materiales:

Enlace a docencia-fmrico, donde se encuentran repositorios relacionados con ROS2:

https://github.com/Docencia-fmrico

Enlace al repositorio original que contiene todos los paquetes utilizados durante la asignatura:

https://github.com/fmrico/book_ros2

A continuación se detallan brevemente todos los contenidos que se encuentran en este repositorio, con el objetivo de facilitar la preparación del examen final de la asignatura (muchos de ellos se obvian por la clara evidencia en su nombre):

## 1. Resumen de los contenidos de teoría

Resumen Teoría ASR.pdf: Resumen de teoría en formato PDF.

Este enlace te redirigirá a un resumen en Google Docs que comprende todos los contenidos teóricos vistos en la asignatura, en el que cualquiera que tenga acceso a este documento puede añadir cualquier contribución:

https://docs.google.com/document/d/1OVAjoF7pPmQrFZVN-w-QSDjo9j6fItquN1dXVo3j8cg/edit?usp=sharing

IMPORTANTE: Para hacer uso del índice interactivo que viene implementado en el resumen, debes descargar el documento en formato PDF.

## 2. Mini-tests realizados en clase y examen final

Ficheros 'Preguntas Test X.pdf': Contiene todas las preguntas de los dos mini-tests realizados en momentos intermedios del curso.

Directorio 'Enunciado examen final': Contiene el enunciado del examen final de la asignatura, se compone de 2 preguntas, una más teórica y otra más relacionada con las prácticas realizadas a lo largo del curso.

## 3. Activación de ROS2 en los laboratorios de la universidad

```sh
$ source /opt/ros/humble/setup.bash
$ echo “source /opt/ros/humble/setup.bash” » ./bashrc
```

IMPORTANTE: Esto debe hacerse SIEMPRE que abrimos una nueva terminal.

## 4. Uso de ros2 bag

### 4.1 Configuración del entorno

Es recomendable abrir la terminal desde el HOME (carpeta personal) para crear el directorio en el que se guardarán los bags.

```sh
$ mkdir bags
$ cd bags/
```

En otra terminal, lanzamos el nodo que hayamos desarrollado. Por ejemplo:

```sh
$ ros2 run demo_nodes_cpp talker
```

Para asegurarte que todo está yendo bien, ejecuta en una terminal diferente el comando ros2 topic list, en el que debe aparecer el topic que está utilizando el nodo que hemos lanzado.

### 4.2 Funciones básicas de ros2 bag

Para crear un bag y almacenar los mensajes que se están publicando en el topic utilizado por el nodo, debemos ejecutar el siguiente comando:

```sh
$ ros2 bag record <topic>
```

Una vez hayamos almacenado la cantidad de mensajes que se nos pida, detenemos el proceso con Ctrl+c, y vemos como dentro de la carpeta bags se ha creado una nueva carpeta llamada rosbag2_<fecha> (nombre por defecto), que debe incluir un archivo metadata.yaml y otro llamado <bag_name>.db3.

Para crear el bag con un nombre que nosotros queramos ejecutamos el mismo comando que antes pero con la opción -o <bag_name>:

```sh
$ ros2 bag record <topic> -o <bag_name>
```

Además, también existe la posibilidad de incluir más de un topic cuando se está creando el bag (<topic1> ... <topicN> en vez de <topic>). Si queremos tener en cuenta TODOS los topics que se están ejecutando en ese momento, le añadimos la opción -a:

```sh
$ ros2 bag record -a -o <bag_name>
```

Una vez hemos creado nuestro bag, podemos obtener información del mismo (nombre, tamaño, id de almacenamiento, duración, cantidad de mensajes, topics utilizados, etc) ejecutando el siguiente comando:

```sh
$ ros2 bag info <bag_name>
```

### 4.3 Reproducir contenido de un bag 

Para ver el contenido que hemos almacenado en nuestro bag, debemos realizar lo siguiente:

En una primera terminal debemos reproducir el contenido del bag mediante el siguiente comando:

```sh
$ ros2 bag play <bag_name>
```

En una segunda terminal, debemos ejecutar ros2 topic echo <topic>, donde <topic> es el topic al que se han estado enviando mensajes mientras se estaba creando el paquete:

```sh
$ ros2 topic echo <topic>
```

IMPORTANTE: Estos dos últimos comandos deben ejecutarse casi de forma simultánea (siempre primero ros2 bag play <bag_name>), ya que si reproducimos el contenido del bag y tardamos más tiempo en ejecutar ros2 topic echo <topic> que lo que dura el bag, no se podrá ver ningún mensaje ya que la reproducción del bag ha finalizado.

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
