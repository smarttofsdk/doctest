C#样例的生成运行
===================

windows平台
+++++++++++++++++++

#. 命令行进入到windows\samples\csharp目录运行下面的命令,<BUILD_TYPE>可以是Release或者Debug::

    mkdir build
    cd build
    cmake .. -G "Visual Studio 12 2013"		//根据自身所装的vs版本
    cd ..
    cmake --build ./build --config <BUILD_TYPE>
	
在build文件下生成了sample_basic.exe和sample_ui.exe两个可执行文件，如下图

.. image:: imageCsharp/win_Cs1.jpg

Linux平台
+++++++++++++++++++

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