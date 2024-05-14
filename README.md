## Cartographer安装编译

教程如下：

### 1.install wstool rosdep ninja

~~~sh
apt-get update
sudo apt-get install -y python-wstool python-rosdep ninja-build
~~~
### 2.Create cartographer workspace

由于编译方式的差异,我们另建一个carto的工作空间来单独编译和运行算法.

~~~sh
mkdir  ~/catkin_carto
解压本仓库的src.zip到 ~/catkin_carto/
#安装依赖
rosdep install --from-paths src --ignore-src --rosdistro=${ROS_DISTRO} -y
~~~

漫长的安装后，正确安装则会出现：

All required rosdeps installed successfully

### 3.Build and install

~~~sh
catkin_make_isolated --install --use-ninja
source install_isolated/setup.bash
~~~
## 仿真xbot运行cartographer建图操作步骤

- 1.启动仿真xbot：
```
cd ~/catkin_ws   #~/为ROS-Academy-for-Beginners-melodic代码工作空间
source devel/setup.bash
roslaunch robot_sim_demo robot_spawn.launch
```
- 2.启动Cartographer
```
cd ~/catkin_carto #~/catkin_carto为Cartographer代码工作空间
source install_isolated/setup.bash
roslaunch cartographer_ros cartographer_demo.launch
```
- 3.启动机器人控制代码，控制建图
```
cd ~/catkin_ws   #~/为ROS-Academy-for-Beginners-melodic代码工作空间
source devel/setup.bash
rosrun robot_sim_demo robot_keyboard_teleop.py
```
