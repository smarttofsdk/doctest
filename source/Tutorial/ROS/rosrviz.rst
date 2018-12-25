ROS rviz工具使用
==================

rviz是ros自带的一个图形化工具，可以方便的对ros的程序进行图形化操作，整体界面如下图所示 ：

	.. image:: imageR/lin_Rv1.jpg 
	
界面主要分为左侧的显示设置区域，中间的大的显示区域和右侧的视角设置区域。
最上面是和导航相关的几个工具。最下面是ros状态相关的一些数据的显示。

rviz使用前准备
++++++++++++++++++++

#. 开启ROS环境::

	Roscore&
	
#. 进入ros所在文件夹初始化环境变量::

	source ./devel/setup.bash

#. 运行launch文件::

	roslaunch dmcam_ros start.launch
	
rviz显示深度图像
++++++++++++++++++++	

#. 打开一个终端，运行rviz::

	rviz
	
#. 选中add，By topic中选中image_dist下的Image，最后确认添加，如下图所示：

	.. image:: imageR/lin_Rv2.jpg 
	
#. 显示效果如下图所示：

	.. image:: imageR/lin_Rv3.jpg 
	
rviz显示点云图像
++++++++++++++++++++	

#. 打开一个终端，运行rviz::

	rviz
	
#. 选中add，byTopic中选中pointcloud下的PointCloud2，最后确认添加.

	.. image:: imageR/lin_Rv4.jpg
	
#. 在rviz左上角的displays区域，修改GlobalOptions下的变量FixedFrame值为dmcam_ros，点云显示如下图

	.. image:: imageR/lin_Rv5.jpg