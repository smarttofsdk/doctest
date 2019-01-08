ROS点云显示
=======================

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