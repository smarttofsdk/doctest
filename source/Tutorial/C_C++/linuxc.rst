Linux下C/C++示例
===================

* 在linux下运行

#. 将SDK文件包中linux下的对应版本的libdmcam.so拷贝到/usr/lib目录下

#. 如果没有安装cmake，需要打开终端，安装cmake::

    sudo apt-get install cmake

#. 在linux/sample/c下新建文件夹build，在终端运行下面命令::

    cd build
    cmake .. -G "Unix Makefiles"
    make -j
	
生成可执行文件后，运行sample_capture_frames采集样例程序如图

.. image:: imageC/lin_C1.jpg

运行sample_set_param参数样例程序如图

.. image:: imageC/lin_C2.jpg

运行sample_save_replay保存录像样例程序如图

.. image:: imageC/lin_C3.jpg

运行录像样例会生成一个名为sample_replay.oni文件,可以通过SmartToFViewer工具进行回放。
生成的录像文件如下图所示

.. image:: imageC/lin_C4.jpg

C++的样例程序的使用跟C一样，具体过程可以参考以上C的使用过程。