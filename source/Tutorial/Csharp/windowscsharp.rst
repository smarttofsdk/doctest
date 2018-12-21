Windows平台C#样例
===================

#. 命令行进入到windows\samples\csharp目录运行下面的命令,<BUILD_TYPE>可以是Release或者Debug::

    mkdir build
    cd build
    cmake .. -G "Visual Studio 12 2013"		//根据自身所装的vs版本
    cd ..
    cmake --build ./build --config <BUILD_TYPE>
	
在build文件下生成了sample_basic.exe和sample_ui.exe两个可执行文件，如下图

.. image:: imageCsharp/win_Cs1.jpg

C# basic样例展示
--------------------

运行生成的sample_basic.exe程序，运行结果如下图

.. image:: imageCsharp/win_Cs2.jpg


C# UI样例展示
--------------------

运行生成的sample_ui.exe程序，运行结果和gui界面如下图

.. image:: imageCsharp/win_Cs3.jpg