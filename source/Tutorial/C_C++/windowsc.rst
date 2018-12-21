Windows下C/C++示例
=====================

在windows下生成vs工程
+++++++++++++++++++++++++

#. 在windows/samples/c下新建文件夹vsbuild
#. 使用命令行工具或者msys2下mingw工具，进入vsbuild使用cmake生成vs工程，具体命令如下::

    cd vsbuild
	
    cmake .. -G "Visual Studio 12 2013"  //根据自身所装的vs版本
#. 生成工程后打开dmcam_c_sample.sln,编译生成C样例的可执行文件。

生成的VS工程如下图：

.. image:: imageC/win_C1.jpg

成功生成VS工程后，使用VS打开工程，生成解决方案，下图展示了生成解决方案后，运行sample_capture_frames程序

.. image:: imageC/win_C2.jpg

其他生成的几个sample程序同样可以运行，运行效果跟windows生成的可执行文件效果一样，具体可查看下面的附图。

在windows下生成可执行文件
++++++++++++++++++++++++++++

#. 在windows\samples\c下新建文件夹build
#. 进入build使用cmake生成可执行文件，具体命令参考如下::

    cd build
	
    cmake .. -G "MSYS Makefiles"
	
    make -j	
#. 编译生成可执行文件后可双击运行

生成可执行文件后，在build文件夹下显示如下图所示的可执行文件：

.. image:: imageC/win_C3.jpg

运行sample_capture_frames采集样例程序如图

.. image:: imageC/win_C4.jpg

运行sample_set_param参数样例程序如图

.. image:: imageC/win_C5.jpg


运行sample_save_replay保存录像样例程序如图

.. image:: imageC/win_C6.jpg

运行录像样例会生成一个名为sample_replay.oni文件,可以通过SmartToFViewer工具进行回放。

C++的样例程序的使用跟C一样，具体过程可以参考以上C的使用过程。























