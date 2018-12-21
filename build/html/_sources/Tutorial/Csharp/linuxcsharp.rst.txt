Linux平台C#样例
===================

#. 在linux下需要安装mono用于C#的编译扩展::

    sudo apt-get install mono-complete
	
#. 进入到linux/sample/chsarp目录下，运行下面命令::

    mkdir build
	cd build
	cmake .. –DCMAKE_BUILD_TYPE=Debug
	cd ..
	cmake –build build
	
在build文件下生成了sample_basic.exe和sample_ui.exe两个可执行文件，如下图

.. image:: imageCsharp/lin_Cs1.jpg

C# basic样例
++++++++++++++++

运行basic命令::

	cd build
	./sample_basic.exe
	
运行sample_basic结果如下图

.. image:: imageCsharp/lin_Cs3.jpg

C# UI样例
++++++++++++++++

运行UI命令::

	cd build
	./sample_ui.exe
	
运行sample_ui结果如下图

.. image:: imageCsharp/lin_Cs2.jpg