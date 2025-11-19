# AprilTag ROS 2 - Guia Completo de Instalação e Uso

Este guia mostra como instalar e usar o AprilTag no ROS 2 para detecção de tags fiduciais.
Repositorio de referencia 
https://github.com/christianrauch/apriltag_ros
📋 Pré-requisitos

- Ubuntu 22.04 (Jammy)

- ROS 2 Humble

- Webcam USB

- Python 3.8+

Primeiro vamos criar a worksapce para colocar os pacotes
```ruby
  mkdir -p ~/ros2_ws/src
  cd ~/ros2_ws
```
Agora vamos clonar os repositorios que vamos utilizar para fazer as tags funcionarem

```ruby
   cd ~/ros2_ws/src
  
  # Biblioteca principal AprilTag
  git clone https://github.com/AprilRobotics/apriltag.git
  
  # Wrapper ROS 2
  git clone https://github.com/christianrauch/apriltag_ros.git
```
Instalar dependencias
```ruby
  cd ~/ros2_ws
  
  # Dependências do sistema
  sudo apt update
  sudo apt install libopencv-dev python3-opencv libeigen3-dev
  
  # Dependências ROS 2
  sudo apt install ros-humble-vision-opencv ros-humble-image-transport \
                   ros-humble-camera-calibration-parsers ros-humble-usb-cam
  
  # Instalar dependências com rosdep
  rosdep install --from-paths src --ignore-src -y
```
Compilar e verificar se esta certo
```ruby
  cd ~/ros2_ws
  colcon build --packages-select apriltag
  colcon build --packages-select apriltag_ros
  source install/setup.bash
```
# Teste Basico de funcionamento
TERMINAL 1
Aqui vamos rodar o no de funcionamento da camera
```ruby
  cd ~/ros2_ws
  source install/setup.bash
  ros2 run usb_cam usb_cam_node_exe --ros-args \
    -p video_device:="/dev/video0" \
    -p image_width:=640 \
    -p image_height:=480
```
TERMINAL 2
Rodar o no de detectacao das Apriltags
```ruby
  cd ~/ros2_ws
  source install/setup.bash
  ros2 run apriltag_ros apriltag_node --ros-args \
    -r image_rect:=/image_raw \
    -r camera_info:=/camera_info \
    -p family:=36h11 \
    -p size:=0.1
```
TERMINAL 3 
Monitorar o topico aonde esta sendo publicado as Apriltags
```ruby
  cd ~/ros2_ws
  source install/setup.bash
  ros2 topic echo /detections
```
