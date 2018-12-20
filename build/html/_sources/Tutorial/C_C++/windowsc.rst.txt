Windows下C/C++示例
=====================

* 在windows下生成vs工程

#. 在windows/samples/c下新建文件夹vsbuild

#. 使用命令行工具或者msys2下mingw工具，进入vsbuild使用cmake生成vs工程，具体命令如下::

    cd vsbuild
	
    cmake .. -G "Visual Studio 12 2013"  //根据自身所装的vs版本
	
#. 生成工程后打开dmcam_c_sample.sln,编译生成C样例的可执行文件。

* 在windows下生成可执行文件

#. 在windows\samples\c下新建文件夹build

#. 进入build使用cmake生成可执行文件，具体命令参考如下::

    cd build
	
    cmake .. -G "MSYS Makefiles"
	
    make -j
	
#. 编译生成可执行文件后可双击运行



