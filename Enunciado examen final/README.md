## 1. Uso de ros2 bag

### 1.1 Configuración del entorno

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

### 1.2 Funciones básicas de ros2 bag

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

### 1.3 Reproducir contenido de un bag 

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
