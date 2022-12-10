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
![Screenshot from 2022-12-10 16-24-51](https://user-images.githubusercontent.com/73121257/206857494-32971efe-e2ef-4a17-bfbc-5c29e3a00e49.png)

Üçüncü bir terminal açıp aktif düğümlerin parametrelerini inceleyin.
```
$ ros2 param list
```
![Screenshot from 2022-12-10 16-26-18](https://user-images.githubusercontent.com/73121257/206857513-5baa5656-a657-408a-be69-550100861bb2.png)
Dördüncü bir terminal açıp parametre değerlerini okuyalım.
```
$ ros2 param get /turtlesim background_b
```
![Screenshot from 2022-12-10 16-28-16](https://user-images.githubusercontent.com/73121257/206857633-b8402662-f0b1-4106-beff-fec2c0fb1999.png)
Parametre değeriini değiştirmek için set komutu kullanılır.
```
$ ros2 param set /turtlesim background_b 150
```
