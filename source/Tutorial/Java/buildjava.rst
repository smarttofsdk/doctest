编译生成
======================

windows平台
++++++++++++++++++++++

#. 将SDK中windows/java目录下对应位数的java包和windows\lib下对应得libdmcam.dll拷贝到windows/samples/java目录

#. 运行javac命令进行编译::

    javac –cp dmcam.jar .\com\smarttof\dmcam\sample\sampleBasic.java
    javac –cp dmcam.jar .\com\smarttof\dmcam\sample\sampleBasicUi.java

   编译成功后，在windows/samples/java/com/smarttof/dmcam/sample下有相应的class文件生成

在windows/samples/java目录中java命令运行::

	java –cp dmcam.jar com.smarttof.dmcam.sample.sampleBasic

在windows/samples/java目录中java命令运行::

	java –cp dmcam.jar com.smarttof.dmcam.sample.sampleBasicUi


linux平台
+++++++++++++++++++++++

#. 在linux下安装openjdk-7-jdk用于java扩展::

    sudo apt-get install openjdk-7-jdk
	
#. 在SDK中的linux/java目录下的对应位数的java包拷贝到linux/samples/java目录，

#. 运行javac命令进行编译::

    javac –cp .:dmcam.jar ./com/smarttof/dmcam/sample/sampleBasic.java
    javac –cp .:dmcam.jar ./com/smarttof/dmcam/sample/sampleBasicUi.java
	
   编译成功后，在linux/samples/java/com/smarttof/dmcam/sample下有相应的class文件生成


在linux/samples/java目录中java目录运行，如果有些动态库没有找到，需要指定LD_LIBRARY_PATH::

	LD_LIBRARY_PATH=$LD_LIBRARY_PATH:$(pwd) java –cp .:dmcam.jar com.smarttof.dmcam.sample.sampleBasic

在linux/samples/java目录中java目录运行，如果有些动态库没有找到，需要指定LD_LIBRARY_PATH::

	LD_LIBRARY_PATH=$LD_LIBRARY_PATH:$(pwd) java –cp .:dmcam.jar com.smarttof.dmcam.sample.sampleBasicUi