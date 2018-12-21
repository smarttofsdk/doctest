Linux平台Java样例
=====================

#. 在linux下安装openjdk-7-jdk用于java扩展::

    sudo apt-get install openjdk-7-jdk
	
#. 在SDK中的linux/java目录下的对应位数的java包拷贝到linux/samples/java目录，

#. 运行javac命令进行编译::

    javac –cp .:dmcam.jar ./com/smarttof/dmcam/sample/sampleBasic.java
    javac –cp .:dmcam.jar ./com/smarttof/dmcam/sample/sampleBasicUi.java
	
   编译成功后，在linux/samples/java/com/smarttof/dmcam/sample下有相应的class文件生成

运行Java Basic样例
----------------------

在linux/samples/java目录中java目录运行，如果有些动态库没有找到，需要指定LD_LIBRARY_PATH::

	LD_LIBRARY_PATH=$LD_LIBRARY_PATH:$(pwd) java –cp .:dmcam.jar com.smarttof.dmcam.sample.sampleBasic
	
程序运行的结果如下图

.. image:: imageJava/lin_J1.jpg

运行Java UI样例
----------------------

在linux/samples/java目录中java目录运行，如果有些动态库没有找到，需要指定LD_LIBRARY_PATH::

	LD_LIBRARY_PATH=$LD_LIBRARY_PATH:$(pwd) java –cp .:dmcam.jar com.smarttof.dmcam.sample.sampleBasicUi
	
程序运行的结果如下图

.. image:: imageJava/lin_J2.jpg