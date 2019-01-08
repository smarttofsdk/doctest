ROS灰度显示
=======================

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