# ROS2_TUTORIAL
## ROS2 Parameters
İlk olarak yeni bir terminal açalım. Açılan yeni terminale ROS2 komutlarına erişmek için ```source /opt/ros/<rosdistro>/setup.bash```yazın.Devamında turtlesimi çalıştırın.
```
$ ros2 run turtlesim turtlesim_node
```
![Screenshot from 2022-12-10 16-24-00](https://user-images.githubusercontent.com/73121257/206857442-8d6920f6-675f-4353-a4fe-2ed24c1addbd.png)
İkinci bir terminal açıp terminale teleop_turtle düğümünü çalıştırın.
```
$ ros2 run turtlesim turtle_teleop_key
```
 file:///home/ali/Pictures/Screenshots/Screenshot%20from%202022-12-10%2016-24-51.png
Üçüncü bir terminal açıp aktif düğümlerin parametrelerini inceleyin.
```
$ ros2 param list
```

