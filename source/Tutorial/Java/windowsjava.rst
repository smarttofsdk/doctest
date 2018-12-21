Windows平台Java样例
======================

#. 将SDK中windows/java目录下对应位数的java包和windows\lib下对应得libdmcam.dll拷贝到windows/samples/java目录

#. 运行javac命令进行编译::

    javac –cp dmcam.jar .\com\smarttof\dmcam\sample\sampleBasic.java
    javac –cp dmcam.jar .\com\smarttof\dmcam\sample\sampleBasicUi.java

   编译成功后，在windows/samples/java/com/smarttof/dmcam/sample下有相应的class文件生成

运行Java basic样例
----------------------

在windows/samples/java目录中java命令运行::

	java –cp dmcam.jar com.smarttof.dmcam.sample.sampleBasic
	
程序运行的结果如下图

.. image:: imageJava/win_J1.jpg

运行Java UI样例
----------------------

在windows/samples/java目录中java命令运行::

	java –cp dmcam.jar com.smarttof.dmcam.sample.sampleBasicUi
	
程序运行的结果如下图

.. image:: imageJava/win_J2.jpg