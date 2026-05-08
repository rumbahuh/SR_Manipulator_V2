# SR_Manipulator_V2
Para ejecutarlo tuve problemas con lo que tarda en lanzarse moveit, asi que lancé los dos primeros launchers en otro orden:
```
source /opt/ros/jazzy/setup.bash
cd kachau_ws
colcon build --symlink-install
```
```
source ~/kachau_ws/install/setup.bash
ros2 launch robot_moveit_config move_group.launch.py
```
```
source ~/kachau_ws/install/setup.bash
ros2 launch rover_kachau robot_gazebo.launch.py world_name:=urjc_excavation_msr
```
```
source ~/kachau_ws/install/setup.bash
ros2 launch rover_kachau robot_controllers.launch.py
```
```
source /opt/ros/jazzy/setup.bash
ros2 run teleop_twist_keyboard teleop_twist_keyboard 
```
Una vez tuviera todos los topics listos lancé el rosbag:
```
ros2 bag record /cmd_vel /imu /joint_states -o rosbag_kachau
```

## Explicación de gráficas
## Enlaces de descarga del archivo rosbag
### ![Archivo mcap](https://github.com/rumbahuh/SR_Manipulator_V2/blob/main/rosbag_kachau/rosbag_kachau_0.mcap)
### ![Archivo yaml](https://github.com/rumbahuh/SR_Manipulator_V2/blob/main/rosbag_kachau/metadata.yaml)
## Captura de RVIZ
![Captura de rviz modelo de tfs](https://github.com/rumbahuh/SR_Manipulator_V2/blob/main/rviz/rviz_tf_model.png)
![Captura de rviz modelo de completo](https://github.com/rumbahuh/SR_Manipulator_V2/blob/main/rviz/rviz_model.png)
## Imágenes de simulación
### Imagen especificada 1 (cubo verde sostenido en el aire)
![Captura de rviz modelo de completo](https://github.com/rumbahuh/SR_Manipulator_V2/blob/main/imagenes_simulacion/cubo_verde_en_el_aire.png)
### Imagen especificada 2 (cubo azul justo antes de colocarlo sobre el rojo)
El cubo verde se desplazó en el tanque debido al movimiento del rover. Más adelante adjunto una imagen después de colocarlo en el tanque en el que se observa el cubo en reposo correctamente.
![Captura de rviz modelo de completo](https://github.com/rumbahuh/SR_Manipulator_V2/blob/main/imagenes_simulacion/cubo_azul_antes_de_colocarlo.png)
### Extra: Cubo verde después de dejarlo sobre el tanque
![Cubo verde en reposo en el tanque](https://github.com/rumbahuh/SR_Manipulator_V2/blob/main/imagenes_simulacion/cubo_verde_reposo_en_tanque.png)
### Extra: Rover después de recorrer los últimos metros
![Rover en salida](https://github.com/rumbahuh/SR_Manipulator_V2/blob/main/imagenes_simulacion/rover_end.png)
## ![Árbol de transformadas](https://github.com/rumbahuh/SR_Manipulator_V2/blob/main/frames_2026-05-08_17.23.00.pdf)
![Árbol de transformadas](https://github.com/rumbahuh/SR_Manipulator_V2/blob/main/arbol_transformadas/frames_2026-05-08_17.23.00_page-0001.jpg)
## Gráfica posición de ruedas vs tiempo
![Posición ruedas vs tiempo](https://github.com/rumbahuh/SR_Manipulator_V2/blob/main/graficas/ruedas_posicion.png)
## Gráfica aceleración vs tiempo
![Aceleración vs tiempo](https://github.com/rumbahuh/SR_Manipulator_V2/blob/main/graficas/aceleracion.png)
## Gráfica de gasto vs tiempo
![Gasto vs tiempo](https://github.com/rumbahuh/SR_Manipulator_V2/blob/main/graficas/gasto.png)

## Other
Se me rompieron las texturas entre que pasé el modelo de blender a los urdfs. A color el modelo se ve de esta manera:
![Nightwing vroom vroom](https://github.com/rumbahuh/SR_Manipulator_V2/blob/main/modelo/rover.png)
He de decir que hubiera implementado el tanque de otra manera si hubiera podido, pero al ver que los objetos se mantenían con esas medidas mínimas me pareció coherente dejarlo y no complicar demasiado el diseño a estas alturas.
