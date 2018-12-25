ROS基本样例
=======================

SDK中提供ros包，主要包括ros系统对smarttof API的封装，
ros中包含有dmcam_ros和cloud_viewer两个包，
dmcam_ros包用来采集与显示深度、灰度数据和动态修改参数，
cloud_viewer包是一个示例，用来显示点云数据。运行ros中的样例步骤如下：

Ubuntu下安装ros
++++++++++++++++++++++++++++

ubuntu下安装ros过程如下：

#. 打开命令行终端，进入SDK中的ros文件夹中，运行如下命令::

	sudo chmod 755 install_ros.sh
	./install_ros.sh
	
#. 出现如下图所示的安装选择版本，手动输入版本名称后按回车开始安装，Ubuntu14.04推荐使用indigo，Ubuntu16.04推荐使用kinetic。

	.. image:: imageR/lin_R1.jpg 

ROS环境配置
++++++++++++++++++++++++++++++++++

每次使用ROS系统前需要初始化安装版本的环境变量，
以Kinetic为例，Kinetic默认安装在/opt/ros/kinetic/目录下，
该环境变量配置文件位置/opt/ros/kinetic/setup.bash,每次使用前需要初始化ros环境，命令如下::

	source /opt/ros/kinetic/setup.bash
	
为了简化配置环境变量的过程，可以选择把环境变量的配置放在~/.bashrc文件中，
这样每次打开一个新终端的时候，ROS的环境变量会自动配置好::

	echo "source /opt/ros/kinetic/setup.bash" >> ~/.bashrc
	
SmartToF ros包编译
+++++++++++++++++++++++++++++++++

#. 进入ros所在目录，通过ls命令查看目录中文件如下::

	install_ros.sh  Makefile  src
	
#. 使用catkin_make(Makefile中实现了catkin_make使用的步骤，也可以使用make命令来编译)::

	source /opt/ros/kinetic/setup.bash(未在bashrc中设置初始化环境需要这一步)
	catkin_make
	
#. 编译完成后会生成devel和build目录，通过ls命令查看编译生成的文件::

	build  devel  install_ros.sh  Makefile  src
	
#. 初始化devel中的环境变量::

	source devel/setup.bash 


smarttof ROS深度图显示
++++++++++++++++++++++++

#. 开启ROS环境::

	roscore&
	
#. 进入ros所在文件夹初始化环境变量::

	source ./devel/setup.bash
	
#. 运行launch文件::

	roslaunch dmcam_ros start.launch
	
#. 显示深度图命令::

	rosrun image_view image_view image:=/smarttof/image_dist

   深度图像显示如下：

   .. image:: imageR/lin_R2.jpg 

smarttof ROS灰度图显示
++++++++++++++++++++++++

#. 开启ROS环境::

	roscore&
	
#. 进入ros所在文件夹初始化环境变量::

	source ./devel/setup.bash
	
#. 运行launch文件::

	roslaunch dmcam_ros start.launch
	
#. 显示灰度图命令::

	rosrun image_view image_view image:=/smarttof/image_gray

   灰度图像显示如下：

   .. image:: imageR/lin_R3.jpg 

smarttof ROS点云显示
++++++++++++++++++++++++

cloud_viewer是一个简单的使用smarttof ros来显示点云数据的样例，
这个样例简单的实现了怎么从smarttof ros发布的话题pointcloud中获取点云数据并显示出来。

#. 开启ROS环境::

	roscore&
	
#. 进入ros所在文件夹初始化环境变量::

	source ./devel/setup.sh
	
#. 运行launch文件::

	roslaunch cloud_viewer start.launch

#. 显示点云图像

	.. image:: imageR/lin_R4.jpg 
	
#. 通过鼠标中间的滑轮和鼠标左键调整点云显示图像，最终效果如图

	.. image:: imageR/lin_R5.jpg 