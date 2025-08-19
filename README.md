# Proyecto Robots M&A

## Humble + Classic (Ubuntu 22.04)

### Dependencies
Instalar primero Gazebo Classic.

```bash
sudo apt-get install ros-humble-gazebo-ros-pkgs
```
Instalacion de dependencias

```bash
# Instala lo que necesite segun el package.xml
rosdep install --from-paths src --ignore-src -r -y
```

### Build

```bash
colcon build --packages-select carga_bot
```

### Run

To launch the robot in Gazebo,
```bash
ros2 launch carga_bot gazebo.launch.py
```
Para ver en rviz,
```bash
ros2 launch carga_bot rviz.launch.py
```
### Configuracion
Se lanza la simulacion.
```bash
ros2 launch carga_bot gazebo.launch.py \
	camera_enabled:=True \
	two_d_lidar_enabled:=True \
	stereo_camera_enabled:=False \
	position_x:=0.0 \
	position_y:=0.0 \
	orientation_yaw:=0.0 \
	odometry_source:=world \
	world_file:=small_warehouse.sdf \
	robot_namespace:="carga_bot"
```

### Mapeo con SLAM Toolbox

Iniciar mapeo:
```bash
ros2 launch carga_bot mapping.launch.py
```

Uso de teleop twist keyboard para mover el robot:
```bash
ros2 run teleop_twist_keyboard teleop_twist_keyboard cmd_vel:=/carga_bot/cmd_vel
```

Guardar mapa:
```bash
cd src/carga_bot/config
ros2 run nav2_map_server map_saver_cli -f carga_map
```

### Nav2 con carga_bot

Uso de Nav2:
```bash
ros2 launch carga_bot nav2.launch.py
```
