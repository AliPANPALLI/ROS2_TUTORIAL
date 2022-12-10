# ROS2_TUTORIAL
## ROS2 Parameters
İlk olarak yeni bir terminal açalım. Açılan yeni terminale ROS2 komutlarına erişmek için ```source /opt/ros/<rosdistro>/setup.bash```yazın.Devamında turtlesimi çalıştırın.
```
$ ros2 run turtlesim turtlesim_node
```
İkinci bir terminal açıp terminale teleop_turtle düğümünü çalıştırın.
```
$ ros2 run turtlesim turtle_teleop_key
```
Üçüncü bir terminal açıp aktif düğümlerin parametrelerini inceleyin.
```
$ ros2 param list
```
https://user-images.githubusercontent.com/73121257/175230830-7b60e1a8-4418-43b1-b821-5d68d1455288.mp4

