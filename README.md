# AprilTag ROS 2 - Guia Completo de Instalação e Uso

Este guia mostra como instalar e usar o AprilTag no ROS 2 para detecção de tags fiduciais.

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

'''ruby
  cd ~/ros2_ws/src
  
  # Biblioteca principal AprilTag
  git clone https://github.com/AprilRobotics/apriltag.git
  
  # Wrapper ROS 2
  git clone https://github.com/christianrauch/apriltag_ros.git
'''
