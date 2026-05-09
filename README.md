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
Los gráficos se encuentran más adelante
### Gráfica de posición de las ruedas frente al tiempo
Observamos 4 valores correspondientes a las 4 ruedas, de los cuales el par de las ruedas traseras se ve solapado por las delanteras obteniendo los mismos valores.
Esta gráfica comienza en el valor 0 en el cual el rover se encuentra en reposo. Observando las rectas, se describen los movimientos cortos teleoperados sobre el topic /cmd_vel en el que el rover se mueve hacia los cubos con la posición correcta para o bien recogerlos o situarlos. EN función de la dificultad para moverse del terreno que resultó más irregular en la posición del cubo aazul (segundo pick), podemos asignar ese pico dispar entre rudas frontales y traseras en los segundos 270 y 400.
Por otro lado observamos un tramo en reposo en el que a través de rviz se realizó la maniobra de place del cubo azul sobre el rojo en el que el rover se encontraba en reposo a excepción del SCARA. Y por último, observamos un aumento casi constante de la posición de las ruedas en la que el rover está recorriendo los 10 metros. La razón por la que se observa un dip de las ruedas frontales frente a las ruedas traseras en ese tramo se trata a que teleoperé el rover para que se moviese en linea recta sobre la rampa para poder utilizar un suelo más regular aunque se trataba de un rampa inclinada.
### Gráfica de aceleración frente al tiempo
Esta gráfica es más sencilla debido a que observamos ciertos intervalos de tiempo corto en el que se observan cambios de aceleración en valores negativos y positivos en los 3 ejes cartesianos debido a los movimientos del rover para llegar a las posiciones debidas. Tambien observamos de nuevo un tramo de tiempo largo en el que el rover necesita aplicar aceleraciones constantes para poder subir la rampa y recorrer los 10 metros de recorrido final.
El pico que se observa entre los segundos 500 y 600 se debe a que al subir la rampa se paró el coche al cambiar de terminal y aumenté la velocidad lineal sin querer.
Al acabar el recorrido se observa que vuelve a sus valores constantes cada eje.
La razón por la que se observa una constante de aceleración en Z 10 unidades mayor que las de X e Y se debe a que el imu mide la aceleración gravitatoria cuando el robot está en reposo, por lo que el sensor registra la gravedad como una aceleración constante en el eje vertical.
### Gráfica de gasto frente a tiempo
En este caso observamos picos positivos de gasto en las ruedas que se generan cuando hay un cambio de dirección. Durante la teleoperación se utilizaron los movimientos marcha atrás y hacia delante del rover para alcanzar las posiciones deseadas, para realizar estos movimientos se giraban ciertas ruedas lo cual corresponde a estos picos. En el último tramo de tiempo más largo se observa que las 4 ruedas no tienen un gasto muy diferente a excepción del momento en el que la velocidad lineal aumenta y hay cierta correción de dirección mínima hacia delante teleoperado para no caer de la rampa.
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
## ![Árbol de transformadas](https://github.com/rumbahuh/SR_Manipulator_V2/blob/main/arbol_transformadas/frames_2026-05-08_17.23.00.pdf)
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
