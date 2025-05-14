# Simulación de la dinámica y el control de un doble péndulo

## Pre requisitos

Este entorno de simulación debería funcionar en cualquier versión de Ubuntu posterior a 20.04.

El uso de Ubuntu no es obligatorio, cualquier entorno que pueda compartir el acceso a la placa de video debería funcionar.
Sin embargo debido a las complejidades que involucra es altamente recomendado utilizar dicha distribución.

### Instalar docker
```
sudo apt install curl
curl -sSL https://get.docker.com/ | sh
sudo usermod -aG docker $(whoami)
```

Cualquier consulta: https://docs.docker.com/get-started/get-docker/

Es importante asegurarse que el sistema tiene el plugin para `docker compose`.
https://docs.docker.com/compose/install/linux/

```
 sudo apt-get update
 sudo apt-get install docker-compose-plugin
```

## Para configurar el espacio:
```
git clone https://github.com/pgonfiuba/ros2_dp.git
cd ros2_dp/docker
docker compose build
```

## Para ejecutar una de las simulaciones:

Existen varias simulaciones. Levantando el contenedor con la opción dp se accede a una simulación del control del doble péndulo que permite cambiar setpoints y ganancias.
La evolución temporal de las variables se pueden configurar en plotjuggler cargando el tópico correspondiente. 

```
$ xhost + && docker compose up dp --force-recreate
```

Deberia inmediatamente inicializar la simulacion con el panel de control de RViz, Gazebo, PlotJuggler y una gui para cambiar parámetros, como se ve:

![](docs/mycobot_280_demo.gif)


## Como usar este repositorio para desarrollo:

Reconstruimos la imagen e inicializamos una nueva imagen:
```
$ docker compose build --no-cache
$ xhost + && docker compose up dev --force-recreate
```

En este caso no se levanta ros2, por lo que se debe hacer manualmente desde una segunda consola, con la opción de levantar otras simulaciones tales como el péndulo doble corriendo sobre un escritorio sin estar fijo en su base.

En una terminal separada nos introducimos en el container.
```
$ docker exec -it robotica_cese_env-dev-1 /bin/bash
```

En esta forma, cualquier cambio en la carpeta `./src/dp` se reflejan en la carpeta `/root/ros2_ws/src/dp` adentro de la imagen.
Asi podemos hacer el cambio que querramos dentro de esa carpeta y ejecutar los cambios en el sistema con el comando desde la segunda terminal:

