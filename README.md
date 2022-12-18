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
 sudo apt install python3-colcon-common-extensions
 ```
 ### Workspace Oluşturma
 ```
 mkdir -p ~/ros2_ws/src
 cd ~/ros2_ws
 ```
## Hazır Paket Yükleme
 Örnek deposunu srcçalışma alanının dizinine kopyalayalım :
```
 git clone https://github.com/ros2/examples src/examples -b galactic
 ```
 Ana workspace dizinimize geçerek build işlemimizi tamamlayalım.
 ```
 colcon build --symlink-install
```
 Derleme tamamlandıktan sonra src klasörünün yanında, install ve log dizinlerini görmeliyiz.
 Az önce oluşturduğumuz paketlerde testler yapmak için colcon test komutu çalıştırılır.Colcon oluşturmayı başarıyla tamamladığında, çıktı install dizinde olacaktır. Yüklü yürütülebilir dosyalardan veya kitaplıklardan herhangi birini kullanmadan önce, bunları yolunuza ve kitaplık yollarınıza eklemeniz gerekir. colcon install, ortamın kurulumuna yardımcı olmak için dizinde bash/bat dosyaları oluşturmuş olacaktır. Bu dosyalar, gerekli tüm öğeleri yolunuza ve kitaplık yollarınıza ekleyecek ve paketler tarafından dışa aktarılan tüm bash veya kabuk komutlarını sağlayacaktır.
 ```
 . install/setup.bash
 ```
 Kaynaklı ortam ile colcon tarafından oluşturulan yürütülebilir dosyaları çalıştırabiliriz. Örneklerden bir abone düğümü çalıştıralım:
 ```
 ros2 run examples_rclcpp_minimal_subscriber subscriber_member_function
 ```
 Başka bir terminalde, bir yayıncı düğümü çalıştıralım (kurulum betiğini kaynaklamayı unutmayın):
 
 ```
 ros2 run examples_rclcpp_minimal_publisher publisher_member_function
 ```
 Artan sayılarla yayıncı ve aboneden gelen mesajları görmelisiniz.

## Kendi Paketimizi Oluşturma
 ```
 mkdir -p ros2_ws/src
 cd ros2_ws/src
 ros2 pkg create --build-type ament_cmake --node-name my_node my_package
 cd ..
 colcon build
 . install/local_setup.bash #localde worksapce belirtilir.
 ros2 run my_package my_node
 ```
 ## C++ ile Subscriber ve publisher yazma
 ```
cd ros2_ws/src
ros2 pkg --build-type ament_cmake cpp_pubsub
cd cpp_pubsub/src
wget -O publisher_member_function.cpp https://raw.githubusercontent.com/ros2/examples/galactic/rclcpp/topics/minimal_publisher/member_function.cpp
```
 #### publisher_member_function.cpp
 ```
 #include <chrono>
#include <functional>
#include <memory>
#include <string>

#include "rclcpp/rclcpp.hpp"
#include "std_msgs/msg/string.hpp"

using namespace std::chrono_literals;

/* This example creates a subclass of Node and uses std::bind() to register a
* member function as a callback from the timer. */

class MinimalPublisher : public rclcpp::Node
{
  public:
    MinimalPublisher()
    : Node("minimal_publisher"), count_(0)
    {
      publisher_ = this->create_publisher<std_msgs::msg::String>("topic", 10);
      timer_ = this->create_wall_timer(
      500ms, std::bind(&MinimalPublisher::timer_callback, this));
    }

  private:
    void timer_callback()
    {
      auto message = std_msgs::msg::String();
      message.data = "Hello, world! " + std::to_string(count_++);
      RCLCPP_INFO(this->get_logger(), "Publishing: '%s'", message.data.c_str());
      publisher_->publish(message);
    }
    rclcpp::TimerBase::SharedPtr timer_;
    rclcpp::Publisher<std_msgs::msg::String>::SharedPtr publisher_;
    size_t count_;
};

int main(int argc, char * argv[])
{
  rclcpp::init(argc, argv);
  rclcpp::spin(std::make_shared<MinimalPublisher>());
  rclcpp::shutdown();
  return 0;
}
 ```
 #### Adım adım kodları inceleyelim
 Kodun üst kısmı, kullanacağınız standart C başlıklarını içerir. Standart C başlıklarından sonra, ROS 2 sisteminin en yaygın parçalarını kullanmanıza izin veren rclcpp/rclcpp.hpp içerir. Sonuncusu, verileri yayınlamak için kullanacağınız yerleşik mesaj türünü içeren std_msgs/msg/string.hpp'dir.
 ```
 #include <chrono>
#include <functional>
#include <memory>
#include <string>

#include "rclcpp/rclcpp.hpp"
#include "std_msgs/msg/string.hpp"

using namespace std::chrono_literals;
 ```
 Sonraki satır, rclcpp::Node'dan miras alarak MinimalPublisher düğüm sınıfını oluşturur. Koddaki her bu, düğüme atıfta bulunur.
 ```
 class MinimalPublisher : public rclcpp::Node
 ```
 Genel oluşturucu, düğümü minimal_publisher olarak adlandırır ve count_ öğesini 0 olarak başlatır. Yapıcı içinde, yayıncı, bir yedekleme durumunda iletileri sınırlamak için Dize ileti türü, konu adı konusu ve gerekli kuyruk boyutu ile başlatılır. Ardından, timer_callback işlevinin saniyede iki kez yürütülmesine neden olan timer_ başlatılır.,
 ```
 public:
  MinimalPublisher()
  : Node("minimal_publisher"), count_(0)
  {
    publisher_ = this->create_publisher<std_msgs::msg::String>("topic", 10);
    timer_ = this->create_wall_timer(
    500ms, std::bind(&MinimalPublisher::timer_callback, this));
  }
 ```
 timer_callback işlevi, mesaj verilerinin ayarlandığı ve mesajların gerçekten yayınlandığı yerdir. RCLCPP_INFO makrosu, yayınlanan her mesajın konsola yazdırılmasını sağlar.
 ```
 private:
  void timer_callback()
  {
    auto message = std_msgs::msg::String();
    message.data = "Hello, world! " + std::to_string(count_++);
    RCLCPP_INFO(this->get_logger(), "Publishing: '%s'", message.data.c_str());
    publisher_->publish(message);
  }
 ```
 Sonuncusu zamanlayıcı, yayıncı ve sayaç alanlarının bildirimidir.
 ```
 rclcpp::TimerBase::SharedPtr timer_;
rclcpp::Publisher<std_msgs::msg::String>::SharedPtr publisher_;
size_t count_;
 ```
 MinimalPublisher sınıfını takip etmek, düğümün gerçekte yürütüldüğü ana sınıftır. rclcpp::init, ROS 2'yi başlatır ve rclcpp::spin, zamanlayıcıdan gelen geri aramalar da dahil olmak üzere düğümden gelen verileri işlemeye başlar.
 ```
 int main(int argc, char * argv[])
{
  rclcpp::init(argc, argv);
  rclcpp::spin(std::make_shared<MinimalPublisher>());
  rclcpp::shutdown();
  return 0;
}
 ```
## Kaynakları Ekleyin
 pacakge.xml dosyası açılır``` amen_cmake ```buildtooldependency satırının altına 
 ```
 <depend>rclcpp</depend>
<depend>std_msgs</depend>
 ```
 eklenir. Şimdi CMakeLists.txt dosyasını açın. Mevcut bağımlılığın altında find_package(ament_cmake REQUIRED), satırları ekleyin
 ```
 find_package(rclcpp REQUIRED)
find_package(std_msgs REQUIRED)
 ```
 Bundan sonra yürütülebilir dosyayı ekleyin ve konuşmacı olarak adlandırın, böylece düğümünüzü ros2 çalıştırmasını kullanarak çalıştırabilirsiniz:
 ```
 add_executable(talker src/publisher_member_function.cpp)
ament_target_dependencies(talker rclcpp std_msgs)
 ```
 Son olarak, ros2 run'un çalıştırılabilir dosyanızı bulabilmesi için install(TARGETS…) bölümünü ekleyin:
 ```
 install(TARGETS
  talker
  DESTINATION lib/${PROJECT_NAME})
 ```
 Bazı gereksiz bölümleri ve yorumları kaldırarak CMakeLists.txt dosyanızı temizleyebilirsiniz, böylece şöyle görünür:
 ```
 cmake_minimum_required(VERSION 3.5)
project(cpp_pubsub)

Default to C++14
if(NOT CMAKE_CXX_STANDARD)
  set(CMAKE_CXX_STANDARD 14)
endif()

if(CMAKE_COMPILER_IS_GNUCXX OR CMAKE_CXX_COMPILER_ID MATCHES "Clang")
  add_compile_options(-Wall -Wextra -Wpedantic)
endif()

find_package(ament_cmake REQUIRED)
find_package(rclcpp REQUIRED)
find_package(std_msgs REQUIRED)

add_executable(talker src/publisher_member_function.cpp)
ament_target_dependencies(talker rclcpp std_msgs)

install(TARGETS
  talker
  DESTINATION lib/${PROJECT_NAME})

ament_package()
 ```
## Subscriber Düğümü Yazma
 Bir sonraki düğümü oluşturmak için ros2_ws/src/cpp_pubsub/src'ye dönün. Terminalinize aşağıdaki kodu girin:
 ```
 wget -O subscriber_member_function.cpp https://raw.githubusercontent.com/ros2/examples/galactic/rclcpp/topics/minimal_subscriber/member_function.cpp
 ```
```subscriber_member_function.cpp``` dosyasını metin düzenleyicinizle açın.
 ```
 #include <memory>

#include "rclcpp/rclcpp.hpp"
#include "std_msgs/msg/string.hpp"
using std::placeholders::_1;

class MinimalSubscriber : public rclcpp::Node
{
  public:
    MinimalSubscriber()
    : Node("minimal_subscriber")
    {
      subscription_ = this->create_subscription<std_msgs::msg::String>(
      "topic", 10, std::bind(&MinimalSubscriber::topic_callback, this, _1));
    }

  private:
    void topic_callback(const std_msgs::msg::String & msg) const
    {
      RCLCPP_INFO(this->get_logger(), "I heard: '%s'", msg.data.c_str());
    }
    rclcpp::Subscription<std_msgs::msg::String>::SharedPtr subscription_;
};

int main(int argc, char * argv[])
{
  rclcpp::init(argc, argv);
  rclcpp::spin(std::make_shared<MinimalSubscriber>());
  rclcpp::shutdown();
  return 0;
}
 ```
 #### Kodu inceleyelim
 Abone düğümünün kodu, yayıncınınkiyle neredeyse aynıdır. Artık düğüm, minimal_subscriber olarak adlandırılmıştır ve yapıcı, geri aramayı yürütmek için düğümün create_subscription sınıfını kullanır. Zamanlayıcı yoktur, çünkü abone, konu konusuna veri her yayınlandığında yanıt verir.
 ```
 public:
  MinimalSubscriber()
  : Node("minimal_subscriber")
  {
    subscription_ = this->create_subscription<std_msgs::msg::String>(
    "topic", 10, std::bind(&MinimalSubscriber::topic_callback, this, _1));
  }
 ```
 Konu öğreticisinden, yayıncı ve abone tarafından kullanılan konu adı ve mesaj türünün iletişim kurabilmeleri için eşleşmesi gerektiğini hatırlayın. topic_callback işlevi, konu üzerinde yayınlanan dize mesajı verilerini alır ve RCLCPP_INFO makrosunu kullanarak konsola yazar. .Bu sınıftaki tek alan bildirimi aboneliktir.
 ```
 private:
  void topic_callback(const std_msgs::msg::String & msg) const
  {
    RCLCPP_INFO(this->get_logger(), "I heard: '%s'", msg.data.c_str());
  }
  rclcpp::Subscription<std_msgs::msg::String>::SharedPtr subscription_;
 ```
 Ana işlev, MinimalSubscriber düğümünü döndürmesi dışında tamamen aynıdır. Yayıncı düğümü için döndürmek, zamanlayıcıyı başlatmak anlamına geliyordu, ancak abone için bu, yalnızca geldikleri zaman mesajları almaya hazırlanmak anlamına geliyordu. Bu düğüm, yayıncı düğümü ile aynı bağımlılıklara sahip olduğundan, ```package.xml ```dosyasına eklenecek yeni bir şey yok.```CMakeLists.txt``` dosyasını yeniden açın ve yayıncının girişlerinin altındaki abone düğümü için yürütülebilir dosyayı ve hedefi ekleyin.
 ```
 add_executable(listener src/subscriber_member_function.cpp)
ament_target_dependencies(listener rclcpp std_msgs)

install(TARGETS
  talker
  listener
  DESTINATION lib/${PROJECT_NAME})
 ```
 ## Build and Run
 Muhtemelen ROS 2 sisteminizin bir parçası olarak rclcpp ve std_msgs paketlerine zaten sahipsiniz. Oluşturmadan önce eksik bağımlılıkları kontrol etmek için çalışma alanınızın kök dizininde (ros2_ws) rosdep çalıştırmak iyi bir uygulamadır:
 ```
 rosdep install -i --from-path src --rosdistro galactic -y
 ```
 Hala çalışma alanınızın kökünde, ros2_ws, yeni paketinizi oluşturun:
 ```
 colcon build --packages-select cpp_pubsub
 ```
 Yeni bir terminal açın, ros2_ws'ye gidin ve kurulum dosyalarını kaynaklayın:
 ```
 . install/setup.bash
 ```
 Şimdi talker düğümünü çalıştırın:
 ```
 ros2 run cpp_pubsub talker
 ```
 Başka bir terminal açın, kurulum dosyalarını yeniden ros2_ws içinden kaynaklayın ve ardından dinleyici düğümünü başlatın:
 ```
 ros2 run cpp_pubsub listener
 ```
 ## Python ile Subscriber ve publisher yazma
 #### Paket Oluşturalım
 ```
 cd ros2_ws/src
 ros2 pkg create --build-type ament_python py_pubsub
 ```
 #### Publisher düğümü yazalım
  ```
cd ros2_ws/src/py_pubsub/py_pubsub
 wget https://raw.githubusercontent.com/ros2/examples/galactic/rclpy/topics/minimal_publisher/examples_rclpy_minimal_publisher/publisher_member_function.py
 ```
 ##### publisher_member_function.py
 ```
 import rclpy
from rclpy.node import Node

from std_msgs.msg import String


class MinimalPublisher(Node):

    def __init__(self):
        super().__init__('minimal_publisher')
        self.publisher_ = self.create_publisher(String, 'topic', 10)
        timer_period = 0.5  # seconds
        self.timer = self.create_timer(timer_period, self.timer_callback)
        self.i = 0

    def timer_callback(self):
        msg = String()
        msg.data = 'Hello World: %d' % self.i
        self.publisher_.publish(msg)
        self.get_logger().info('Publishing: "%s"' % msg.data)
        self.i += 1


def main(args=None):
    rclpy.init(args=args)

    minimal_publisher = MinimalPublisher()

    rclpy.spin(minimal_publisher)

    # Destroy the node explicitly
    # (optional - otherwise it will be done automatically
    # when the garbage collector destroys the node object)
    minimal_publisher.destroy_node()
    rclpy.shutdown()


if __name__ == '__main__':
    main()
 ```
 #### Kodu inceleyelim
 Yorumlardan sonraki ilk kod satırları rclpy, Nodesınıfının kullanılabilmesi için içe aktarılır.
```
import rclpy
from rclpy.node import Node
 ```
Bir sonraki ifade, düğümün konuyla ilgili aktardığı verileri yapılandırmak için kullandığı yerleşik dize mesaj türünü içe aktarır.
```
from std_msgs.msg import String
 ```
Bu satırlar, düğümün bağımlılıklarını temsil eder. package.xmlBir sonraki bölümde yapacağınız bağımlılıkların eklenmesi gerektiğini hatırlayın .

Ardından, MinimalPublisheröğesinden miras alan (veya onun bir alt sınıfı olan) sınıf oluşturulur Node.
```
class MinimalPublisher(Node):
 ```
Aşağıda, sınıfın yapıcısının tanımı yer almaktadır. super().__init__sınıfın yapıcısını çağırır Nodeve ona sizin düğüm adınızı verir, bu durumda minimal_publisher.

create_publisheradlı bir konu üzerinden düğümün (modülden Stringiçe aktarılan ) türünde mesajlar yayınladığını ve “kuyruk boyutunun” 10 olduğunu beyan eder. bir abone onları yeterince hızlı almıyor.std_msgs.msgtopic

Ardından, her 0,5 saniyede bir yürütülecek bir geri arama ile bir zamanlayıcı oluşturulur. self.igeri aramada kullanılan bir sayaçtır.
```
def __init__(self):
    super().__init__('minimal_publisher')
    self.publisher_ = self.create_publisher(String, 'topic', 10)
    timer_period = 0.5  # seconds
    self.timer = self.create_timer(timer_period, self.timer_callback)
    self.i = 0
 ```
timer_callbackeklenen sayaç değeri ile bir mesaj oluşturur ve bunu konsolda yayınlar get_logger().info.
```
def timer_callback(self):
    msg = String()
    msg.data = 'Hello World: %d' % self.i
    self.publisher_.publish(msg)
    self.get_logger().info('Publishing: "%s"' % msg.data)
    self.i += 1
 ```
Son olarak, ana işlev tanımlanır.
```
def main(args=None):
    rclpy.init(args=args)

    minimal_publisher = MinimalPublisher()

    rclpy.spin(minimal_publisher)

    # Destroy the node explicitly
    # (optional - otherwise it will be done automatically
    # when the garbage collector destroys the node object)
    minimal_publisher.destroy_node()
    rclpy.shutdown()
 ```
Önce rclpykitaplık başlatılır, ardından düğüm oluşturulur ve ardından düğümü "döndürür", böylece geri aramaları çağrılır.
## Bağımlılıkları ekleyelim
 package.xmlMetin düzenleyicinizle açın .
 ```
 <description>Examples of minimal publisher/subscriber using rclpy</description>
<maintainer email="you@email.com">Your Name</maintainer>
<license>Apache License 2.0</license>
 ```
 Yukarıdaki satırlardan sonra, düğümünüzün import ifadelerine karşılık gelen aşağıdaki bağımlılıkları ekleyin:
```
<exec_depend>rclpy</exec_depend>
<exec_depend>std_msgs</exec_depend>
 ```
Bu, paketin ihtiyaçlarını rclpyve std_msgskodunun ne zaman yürütüleceğini bildirir.

Dosyayı kaydettiğinizden emin olun.

setup.py Dosyayı açın . Yine, maintainer, maintainer_emailve descriptionalanlarını licenseaşağıdakilerle eşleştirin package.xml:
 ```
maintainer='YourName',
maintainer_email='you@email.com',
description='Examples of minimal publisher/subscriber using rclpy',
license='Apache License 2.0',
 ```
Alanın console_scriptsköşeli parantezleri içine aşağıdaki satırı ekleyin :entry_points
```
entry_points={
        'console_scripts': [
                'talker = py_pubsub.publisher_member_function:main',
        ],
},
 ```
Kaydetmeyi unutmayın.
 Dosyanın içeriği aşağıdaki setup.cfg gibi otomatik olarak doğru bir şekilde doldurulmalıdır:
```
[develop]
script-dir=$base/lib/py_pubsub
[install]
install-scripts=$base/lib/py_pubsub
 ```
Bu basitçe setuptools'a yürütülebilir dosyalarınızı içine koymasını söylüyor lib, çünkü onları orada arayacaktır.ros2 run

Paketinizi şimdi oluşturabilir, yerel kurulum dosyalarını kaynaklayabilir ve çalıştırabilirsiniz, ancak tüm sistemi iş başında görebilmeniz için önce abone düğümünü oluşturalım.
#### Subscriber Düğümü Yazalım
 ros2_ws/src/py_pubsub/py_pubsubSonraki düğümü oluşturmak için geri dönün . Terminalinize aşağıdaki kodu girin:
 ```
 wget https://raw.githubusercontent.com/ros2/examples/galactic/rclpy/topics/minimal_subscriber/examples_rclpy_minimal_subscriber/subscriber_member_function.py
 ```
 ##### Kodu inceleyin
subscriber_member_function.pyMetin düzenleyicinizle açın .
```
import rclpy
from rclpy.node import Node

from std_msgs.msg import String


class MinimalSubscriber(Node):

    def __init__(self):
        super().__init__('minimal_subscriber')
        self.subscription = self.create_subscription(
            String,
            'topic',
            self.listener_callback,
            10)
        self.subscription  # prevent unused variable warning

    def listener_callback(self, msg):
        self.get_logger().info('I heard: "%s"' % msg.data)


def main(args=None):
    rclpy.init(args=args)

    minimal_subscriber = MinimalSubscriber()

    rclpy.spin(minimal_subscriber)

    # Destroy the node explicitly
    # (optional - otherwise it will be done automatically
    # when the garbage collector destroys the node object)
    minimal_subscriber.destroy_node()
    rclpy.shutdown()


if __name__ == '__main__':
    main()
 ```
Abone düğümünün kodu, yayıncınınkiyle neredeyse aynıdır. Yapıcı, yayıncıyla aynı bağımsız değişkenlere sahip bir abone oluşturur. Yayıncı ve abone tarafından kullanılan konu adı ve mesaj türünün, iletişim kurmalarına izin vermek için eşleşmesi gerektiğini konu eğitiminden hatırlayın .
```
self.subscription = self.create_subscription(
    String,
    'topic',
    self.listener_callback,
    10)
 ```
Abonenin oluşturucusu ve geri araması herhangi bir zamanlayıcı tanımı içermez, çünkü buna ihtiyacı yoktur. Bir mesaj alır almaz geri araması aranır.

Geri arama tanımı, aldığı verilerle birlikte konsola bir bilgi mesajı yazdırır. Yayıncının tanımladığını hatırlayınmsg.data = 'Hello World: %d' % self.i
```
def listener_callback(self, msg):
    self.get_logger().info('I heard: "%s"' % msg.data)
 ```
Tanım neredeyse tamamen aynıdır , mainyayıncının oluşturulması ve döndürülmesinin yerini abone alır.
```
minimal_subscriber = MinimalSubscriber()

rclpy.spin(minimal_subscriber)
 ```
Bu düğüm, yayıncı ile aynı bağımlılıklara sahip olduğundan, eklenecek yeni bir şey yoktur package.xml. setup.cfgDosyaya dokunulmadan da kalabilir .
 Yeniden açın setup.pyve abone düğümü için giriş noktasını yayıncının giriş noktasının altına ekleyin. Alan entry_pointsşimdi şöyle görünmelidir:
```
entry_points={
        'console_scripts': [
                'talker = py_pubsub.publisher_member_function:main',
                'listener = py_pubsub.subscriber_member_function:main',
        ],
},
 ```
Dosyayı kaydettiğinizden emin olun ve ardından pub/sub sisteminiz kullanıma hazır olmalıdır.
 Muhtemelen ROS 2 sisteminizin bir parçası olarak rclpyve paketlerine zaten sahipsiniz . Oluşturmadan önce eksik bağımlılıkları kontrol etmek için çalışma alanınızın kökünde ( ) std_msgsçalıştırmak iyi bir uygulamadır :rosdepros2_ws
 ```
 rosdep install -i --from-path src --rosdistro galactic -y
 ```
 Hala çalışma alanınızın kökünde, ros2_wsyeni paketinizi oluşturun:
 ```
 colcon build --packages-select py_pubsub
```
 Yeni bir terminal açın, konumuna gidin ros2_wsve kurulum dosyalarını kaynaklayın:
```
 . install/setup.bash
```
 Şimdi talker düğümünü çalıştırın:
```
ros2 run py_pubsub talker
```
 Terminal, aşağıdaki gibi her 0,5 saniyede bir bilgi mesajları yayınlamaya başlamalıdır.
Başka bir terminal açın, kurulum dosyalarını tekrar içeriden kaynaklayın ros2_wsve ardından dinleyici düğümünü başlatın:
```
ros2 run py_pubsub listener
```
 Dinleyici, yayıncının o anda açık olduğu mesaj sayısından başlayarak mesajları konsola yazdırmaya başlar.
