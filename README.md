# MARSIM
MARSIM: 轻量化雷达无人机仿真器
## 目录
[项目简介与成就](#项目简介与成就) 

[更新](#更新) 

[环境配置](#环境配置) 

[单无人机仿真](#单无人机仿真) 

[单无人机仿真的动态避障](#单无人机仿真的动态避障) 

[多无人机仿真](#多无人机仿真) 

[Fuel算法下的仿真](#Fuel算法下的仿真) 

[声明](#声明)

[未来愿景](#未来愿景)

## 项目简介与成就
1. 利用LiDAR扫描，把现实环境重建为点云地图。
2. 硬件平台要求低，可在具有GPU加速的个人电脑上运行。
3. 支持三种类型的动态障碍物仿真、同时可以进行多无人机系统仿真，以及支持旋转LiDAR的扫描的角度
论文链接(Arxiv): https://arxiv.org/abs/2211.10716

YouTube视频: https://youtu.be/hiRtcq-5lN0 

【MARSIM: 轻量化雷达无人机仿真器】 https://www.bilibili.com/video/BV1M84y117KG

<p align="center">
  <a href="https://youtu.be/hiRtcq-5lN0" target="_blank"><img src="figures/coverfigure.png" alt="video" width="800" height="400" border="1" /></a>
</p>

<p align="center">

  <img src="figures/readme_setgoal.gif" width = "400" height = "237"/>

  <img src="figures/readme_dynobs.gif" width = "400" height = "237"/>


  <img src="figures/readme_multiuav.gif" width = "400" height = "237"/>


  <img src="figures/readme_exploration.gif" width = "400" height = "237"/>
</p>

## 更新

现已支持Ubuntu 20.04，可以在ubuntu20分支中找到。


**已在发布包中发布了十个逼真的地图（低分辨率和高分辨率）**

**已在fuel_ubuntu20分支中发布了与FUEL合并的新分支**



## 环境配置

### Ubuntu 和 ROS

Ubuntu 16.04~20.04.  [ROS Installation](http://wiki.ros.org/ROS/Installation).

### PCL && Eigen && glfw3

PCL>=1.6, 参考 [PCL Installation](https://pointclouds.org/). 

Eigen>=3.3.4, 参考 [Eigen Installation](https://eigen.tuxfamily.org/index.php?title=Main_Page).

glfw3:
```
sudo apt-get install libglfw3-dev libglew-dev
```

### Make
```
mkdir -p marsim_ws/src
cd marsim_ws/src
git clone git@github.com:hku-mars/MARSIM.git
cd ..
catkin_make
```

## 单无人机仿真

```
source devel/setup.bash
roslaunch test_interface single_drone_avia.launch
```
在Rviz上点击3Dgoal，就可以给无人机发送位置指令了，我们可以观察到，无人机自动抵达他的目标位置。

目前，我们为用户提供了几个Launch文件，可以在test_interface/launch文件夹中找到。

您可以更改Launch文件中的参数来更改地图, 和需要模拟的LiDAR。地图已上传至此仓库的发布文件中。

```
    <arg name="map_name" value="$(find map_generator)/resource/small_forest01cutoff.pcd"/>

```

**如果想使用MARSIM的GPU加速模式，请将参数"use_gpu"设置为true。**

## 单无人机仿真的动态避障
```
source devel/setup.bash
roslaunch test_interface single_drone_mid360_dynobs.launch
```

## 多无人机仿真
```
source devel/setup.bash
roslaunch test_interface triple_drone_mid360.launch
```

## Fuel算法下的仿真

首先需要将分支切换到fuel_ubuntu20分支。如果使用的是Ubuntu 20.04，您应该首先下载Nlopt并将其安装在您的ROS环境中。然后，可以通过以下命令运行仿真：

```
source devel/setup.bash
roslaunch exploration_manager exploration.launch
```
然后在Rviz上点击2Dgoal工具，随机点击地图，FUEL将自动运行。

## 声明
感谢 [FUEL](https://github.com/HKUST-Aerial-Robotics/FUEL.git)

## 未来愿景
我们将很快发布更高多真实的地图和功能。
