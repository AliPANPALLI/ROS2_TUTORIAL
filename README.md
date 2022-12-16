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
![Screenshot from 2022-12-10 16-32-09](https://user-images.githubusercontent.com/73121257/206857828-71297928-dbb5-4c4e-8b6c-aef752eb24f5.png)
 Değiştirlen parametreleri kaydetmek için ``` $ ros2 param dump /turtlesim ``` kullanılır.Paametre yüklemek için ```  ros2 param load /turtlesim turtlesim.yaml ``` kullanılır.

## ROS2 SERVICES
Servisler kullanıcıdan istek geldiği sürece çalışırlar.
![Screenshot from 2022-12-10 18-59-23](https://user-images.githubusercontent.com/73121257/206863929-2ea2425c-ebcb-4055-b8ee-ea2d10be0b29.png)
Bir servise birden fazla client bağlanabilir.
![Screenshot from 2022-12-10 19-00-51](https://user-images.githubusercontent.com/73121257/206864017-19925835-adda-4ab8-a7a9-8a2034088a4c.png)
İlk olarak Turtlesim düğümünü başlatalım
```
$ ros2 run turtlesim turtlesim_node
```
İkinci bir terminalde teleop_turtle düğümünü çalıştıralım.
```
$ ros2 run turtlesim turtle_teleop_key
```
``` ros2 service list ``` komutunu yeni bir terminalde çalıştırılması, sistemde o anda aktif olan tüm servislerin bir listesini döndürür. ``` ros2 service type <service_name> ``` komutu ise servis türünü öğrenmeye yarar.Servisleri komut satırından arayabilirsiniz, ancak önce giriş argümanlarının yapısını bilmeniz gerekir. Giriş argümanlarının yapılarını ``` ros2 interface show <type_name>.srv ``` komut satırı ile öğrenebiliriz.
### Örnek
Bir /spawn çağrı ve isteğindeki bağımsız değişkenleri görmek için şu komutu çalıştırın:
```
$ros2 interface show turtlesim/srv/Spawn
```
Döndürdüğü değerler:
```
float32 x
float32 y
float32 theta
string name 
---
string name
```
Artık bir hizmet türünün ne olduğunu, bir hizmetin türünü nasıl bulacağınızı ve bu türün bağımsız değişkenlerinin yapısını nasıl bulacağınızı bildiğinize göre, aşağıdakileri kullanarak bir hizmeti çağırabilirsiniz:
```
ros2 service call <service_name> <service_type> <arguments>
```
Şimdi /spawn çağırıp argümanlar girerek yeni bir kaplumbağa üretelim. Komut satırından yapılan bir hizmet çağrısında <arguments> girişinin YAML sözdiziminde olması gerekir.
```
ros2 service call /spawn turtlesim/srv/Spawn "{x: 2, y: 2, theta: 0.2, name: ''}"
```
Neler olup bittiğine dair bu yöntem tarzı görünümü ve ardından hizmet yanıtını alacaksınız:
 ```
requester: making request: turtlesim.srv.Spawn_Request(x=2.0, y=2.0, theta=0.2, name='turtle2')

response:
turtlesim.srv.Spawn_Response(name='turtle2')
```
## ROS2 DÜĞÜM
ROS'daki her düğüm, tek bir modül amacından sorumlu olmalıdır (örneğin, tekerlekli motorları kontrol etmek için bir düğüm, bir lazer mesafe bulucuyu kontrol etmek için bir düğüm, vb.). Her düğüm, konular, hizmetler, eylemler veya parametreler aracılığıyla diğer düğümlere veri gönderip alabilir.
![Nodes-TopicandService](https://user-images.githubusercontent.com/73121257/208055253-b2523f3d-6d9e-4baa-9e17-28bb08fa914d.gif)
### Örnek
 ```
 source /opt/ros/<rosdistro>/setup.bash
 #ros2 run <package_name> <executable_name>
 ros2 run turtlesim turtlesim_node
```
 ## ROS2 Düğüm Listesi
  ```ros2 node list ``` çalışan tüm düğümlerin adlarını size gösterecektir.
  ```
 ros2 node list
```
 Komutu sayesinde aktif olan tüm düğümleri listeler.
 ## ROS2 Düğüm Bilgisi
 ```
 ros2 node info /turtlesim #turtlesim konusuna dair çıktıları dinler.
 ```
 ### Örnek
 Yeni Terminal
 ```
 ros2 run turtlesim turtlesim_node
 ```
Başka bir terminal
 ```
 ros2 run turtlesim turtle_teleop_key![Service-SingleServiceClient](https://user-images.githubusercontent.com/73121257/208063141-80385690-11b5-490a-a012-58cef445a2b7.gif)

 ```
 ## rqt_graf
 ```
 rqt graph
 ```
 ### Çıktı
 ![rqt_graph](https://user-images.githubusercontent.com/73121257/208062627-60aabe60-63f0-425d-89ab-9859202bb8c6.png)
 ## ROS2 Konu Bilgisi
 Ros2 konu bilgisi``` ros2 topic info /<topic_name>```  komutu ile alınır.
## Servisler
 Servisler, ROS grafiğindeki düğümler için başka bir iletişim yöntemidir. Hizmetler, konuların yayıncı-abone modeline karşı bir çağrı ve yanıt modeline dayalıdır. Konular, düğümlerin veri akışlarına abone olmasına ve sürekli güncellemeler almasına izin verirken, hizmetler yalnızca bir müşteri tarafından özel olarak çağrıldıklarında veri sağlar.
 ![Service-SingleServiceClient](https://user-images.githubusercontent.com/73121257/208063561-aa8eb7e6-57c3-451b-bedf-892a0df0c3a5.gif)

 
 ![Service-MultipleServiceClient](https://user-images.githubusercontent.com/73121257/208063456-ffe29eea-c44b-4d4c-b6d9-4104d27dc997.gif)
780da7a932.gif)
## Kurulum
 İki kaplumbağa düğümü başlatalım ```/turtlesim``` ve ```/teleop_turtle```
 ```
 ros2 run turtlesim tuertlesim_node #İlk terminal
 ros2 run tutlesim turtle_teleop_key #İkinci Terminal
 ```
 ## ROS2 Hizmet Listesi
 Komutu yeni bir terminalde çalıştırmak , sistemde o anda etkin olan tüm hizmetlerin bir listesini döndürür```ros2 service list```
## Launch Paketi OLuşturma
 touch komutu ile python dosyası oluştrulur.
 ```
 mkdir launch
 touch launch/turtlesim_mimic_launch.py
 gedit launch/turtlesim_mimic_launch.py
 ```
 #### turtlesim_mimic_launch.py
  ```
from launch import LaunchDescription
from launch_ros.actions import Node

def generate_launch_description():
    return LaunchDescription([
        Node(
            package='turtlesim',
            namespace='turtlesim1',
            executable='turtlesim_node',
            name='sim'
        ),
        Node(
            package='turtlesim',
            namespace='turtlesim2',
            executable='turtlesim_node',
            name='sim'
        ),
        Node(
            package='turtlesim',
            executable='mimic',
            name='mimic',
            remappings=[
                ('/input/pose', '/turtlesim1/turtle1/pose'),
                ('/output/cmd_vel', '/turtlesim2/turtle1/cmd_vel'),
            ]
        )
    ])
  ```
 ### ROS2 LAUNCH
 ```
 cd launch
 ros2 launch turtlesim_mimic_launch.py
 ```
 launch dosyamızı yukarudaki komut satırıyla başlatalım çıktımız aşağıdaki şekildeki gibi olacaktır.
 ![multipl_launch_turtlesim](https://user-images.githubusercontent.com/73121257/208149617-2b40c129-474c-435f-9f45-b8d0610d2bad.png)
Sistemi çalışırken görmek için yeni bir terminal açın ve ilk kaplumbağayı hareket ettirmek için konuyla ilgili komutu çalıştırın ```ros2 topic pub``` ```/turtlesim1/turtle1/cmd_vel```
 ```
 ros2 topic pub -r 1 /turtlesim1/turtle1/cmd_vel geometry_msgs/msg/Twist "{linear: {x: 2.0, y: 0.0, z: 0.0}, angular: {x: 0.0, y: 0.0, z: -1.8}}"

 ```
 ![multiple_turtle](https://user-images.githubusercontent.com/73121257/208150191-43e90f98-044c-4b02-85bf-6f4fe01e8f3f.png)
 ### Sistemi rqt_graph ile inceleyelim
 Sistem hala çalışırken, ```rqt_graph```başlatma dosyanızdaki düğümler arasındaki ilişki hakkında daha iyi bir fikir edinmek için yeni bir terminal açın ve çalıştırın.
 ```
 rqt_graph
 ```
 ![rosgraph](https://user-images.githubusercontent.com/73121257/208150659-9cc2f605-d21b-4826-9773-9676bfc955c7.png)

 
## COLCON Paketleri Oluşturmak 
 ```
 sudo aptinstall python3-colcon-common-extensions
 ```
 ### Workspace Oluşturma
 ```
 mkdir -p ~/ros2_ws/src
cd ~/ros2_ws
 ```
