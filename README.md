# Arquitectura Software para Robots 2022-2023

¡Bienvenido! En este repositorio se encuentran todos los materiales correspondientes a la asignatura de Arquitectura Software para Robots.

A continuación se detallan brevemente todos los contenidos que se encuentran en este repositorio, con el objetivo de facilitar la preparación del examen final teórico de la asignatura:

## 1. Activación de ROS2 en los laboratorios de la universidad

```sh
source /opt/ros/humble/setup.bash
echo “source /opt/ros/humble/setup.bash”
```

IMPORTANTE: Esto debe hacerse siempre que abrimos una nueva terminal.

## 2. Resumen de los contenidos de teoría

Este enlace te redirigirá a un resumen en Google Docs que comprende todos los contenidos teóricos vistos en la asignatura, en el que cualquiera que tenga acceso a este documento puede añadir cualquier contribución:

https://docs.google.com/document/d/1OVAjoF7pPmQrFZVN-w-QSDjo9j6fItquN1dXVo3j8cg/edit?usp=sharing

IMPORTANTE: Para hacer uso del índice interactivo que viene implementado en el resumen, debes descargar el documento en formato PDF.

## 3. Preguntas tipo test realizadas en las pruebas de clase

Preguntas Test 1.pdf: Test realizado el 21/02/2023.

Preguntas Test 2.pdf: Test realizado el 25/04/2023.

## 4. Hoja de comandos de ROS2

Comandos ROS2.pdf: Incluye todos los comandos que hemos visto en el curso.

## 5. Índice de paquetes

Estos son los paquetes que componen cada uno de los directorios correspondientes a cada tema:

Paquetes Tema 1: my_package.

Paquetes Tema 2: br2_basics, br2_tiago.

Paquetes Tema 3: br2_fsm_bumpgo_cpp, br2_fsm_bumpgo_py, br2_tiago.

Paquetes Tema 4: br2_tf2_detector, br2_tiago.

Paquetes Tema 5: br2_tiago, br2_tracking, br2_tracking_msgs, br2_vff_avoidance.

Paquetes Tema 6: br2_bt_bumpgo, br2_bt_patrolling, br2_navigation, br2_tiago.

NOTA: El paquete br2_tiago aparece en prácticamente todos los directorios ya que es el encargado de lanzar la simulación.

## 6. Libro de referencia utilizado en la asignatura

A Concise Introduction to Robot Programming with ROS2 Francisco Martín Rico.pdf

## 7. Creación de un workspace, uso y ejecución de un paquete

### 7.1 Creación y activación de un workspace

```sh
$ cd
$ mkdir -p <my_workspace>/src
$ cd <my_workspace>/src
$ git clone https://github.com/<usuario>/<my_workspace>.git
$ cd ~/<my_workspace>/src
$ vcs import . < <my_workspace>/third_parties.repos
$ cd ~/<my_workspace>
$ rosdep install –from-paths src –ignore-src -r -y
$ cd ~/<my_workspace>
$ colcon build –symlink-install
$ source ~/<my_workspace>/install/setup.bash
$ echo “source ~/<my_workspace>/install/setup.bash” >> /.bashrc
```

### 7.2 Creación y ejecución de un paquete

```sh
$ cd ~/<my_workspace>/src
$ ros2 pkg create –build-type <type> <my_package> –dependencies rclcpp <message_type>_msgs
$ cd ~/<my_workspace>
$ colcon build –symlink-install // colcon build –packages-select <my_package>
$ source install/setup.sh
$ ros2 run <my_package> <executable>
```

## 8. Creación y guardado de un mapa usando Nav2

```sh
$ ros2 launch br2_tiago sim.launch.py
$ rivz2 –ros-args -p use_sim_time:=true
$ ros2 launch slam_toolbox online_async.launch.py params_file:=<path completo a mapper_class_params_online_async.yaml> use_sim_time:=true
$ ros2 launch nav2_map_server map_saver_server.launch.py
$ ros2 run teleop_twist_keyboard teleop_twist_keyboard –ros-args -r cmd_vel:=key_vel -p use_sim_time:=true
$ ros2 run nav2_map_server map_saver_cli –ros-args -p use_sim_time:=true
```
