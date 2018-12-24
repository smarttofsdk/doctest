Openni2样例使用
=================

SmartToF SDK目前提供支持OpenNI2的Windows平台相关驱动库，
并且SDK提供了配套运行OpenNI2下的采集样例。

SmartToF Niviewer使用
---------------------------

通过将SDK中openni2包中的libdmcam.dll、smarttof.dll、smarttof.lib、smarttof.pdb等库
拷贝到OpenNI2安装路径下下的Tools/OpenNI2/Drivers下，如下图

.. image:: imageNi/win_N1.jpg

转到Tools目录，管理员运行Tools下NiViewer.exe程序，显示结果如下图

.. image:: imageNi/win_N2.jpg

.. image:: imageNi/win_N3.png


SmartToF Openni2采集样例运行
--------------------------------

进入SDK中的openni2目录下的Smarttof_OpenNI_Sample/Smarttof_OpenNI_Sample,打开VS工程如下图

.. image:: imageNi/win_N4.jpg

编译生成main.cpp,生成后运行结果如下图

.. image:: imageNi/win_N5.jpg

SmartToF Openni2参数样例运行
--------------------------------

将Openni2采集样例中改为sample_set_param.cpp加入编译，编译生成后运行结果如下图

.. image:: imageNi/win_N6.jpg
