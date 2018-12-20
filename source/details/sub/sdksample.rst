C Sample 使用流程
---------------------

* 在windows下生成vs工程

#. 在windows/samples/c下新建文件夹vsbuild

#. 使用命令行工具或者msys2下mingw工具，进入vsbuild使用cmake生成vs工程，具体命令如下::

    cd vsbuild
	
    cmake .. -G "Visual Studio 12 2013"  //根据自身所装的vs版本
	
#. 生成工程后打开dmcam_c_sample.sln,编译生成C样例的可执行文件。

生成的vs工程对应关系如下表3-1：

	.. list-table:: 表3-1 VS版本对应关系
		:widths: 60 40
		:header-rows: 1
		
		* - 版本
		  - 数字
		* - Visual Studio 2005
		  - 8
		* - Visual Studio 2008
		  - 9
		* - Visual Studio 2010
		  - 10
		* - Visual Studio 2012
		  - 11
		* - Visual Studio 2013
		  - 12	  
		* - Visual Studio 2015
		  - 14
		* - Visual Studio 2017
		  - 15

* 在windows下生成可执行文件

#. 在windows\samples\c下新建文件夹build

#. 进入build使用cmake生成可执行文件，具体命令参考如下::

    cd build
	
    cmake .. -G "MSYS Makefiles"
	
    make -j
	
#. 编译生成可执行文件后可双击运行

* 在linux下运行

#. 将对应版本的libdmcam.so拷贝到/usr/lib目录下

#. 打开终端，安装cmake::

    sudo apt-get install cmake

#. 在linux/sample/c下新建文件夹build，在终端运行下面命令::

    cd build
    cmake .. -G "Unix Makefiles"
    make -j
	
运行生成的可执行文件。

C++ Sample 使用流程
---------------------

C++ 的Sample使用流程参考上节的C Sample使用流程。

C# Sample 使用流程
---------------------

* 在windows下编译运行

#. 命令行进入到windows\samples\csharp目录运行下面的命令,<BUILD_TYPE>可以是Release或者Debug::

    mkdir build
    cd build
    cmake ..
    cd ..
    cmake --build ./build --config <BUILD_TYPE>
	

#. 运行生成的exe文件::

    cd build
    ./sample_basic.exe
    ./sample_ui.exe
	
* Linux下编译运行

#. 在linux下需要安装mono用于C#的编译扩展::

    sudo apt-get install mono-complete
	
#. 进入到linux/sample/chsarp目录下，运行下面命令::

    mkdir build
	cd build
	cmake .. –DCMAKE_BUILD_TYPE=Debug
	cd ..
	cmake –build build
	
#. 运行可执行文件::

	cd build
	./sample_basic.exe
	./sample_ui.exe

Java Sample 使用流程
---------------------

* 在windows下使用java示例

#. 将SDK中windows\java目录下对应位数的java包拷贝到windows\samples\java目录，运行javac命令进行编译::

    javac –cp dmcam.jar .\com\smarttof\dmcam\sample\sampleBasic.java
    javac –cp dmcam.jar .\com\smarttof\dmcam\sample\sampleBasicUi.java

   编译成功后，在windows\samples\java\com\smarttof\dmcam\sample下有相应的class文件生成
	
#. 在windows\samples\java目录中java命令运行::

	java –cp dmcam.jar com.smarttof.dmcam.sample.sampleBasic
	java –cp dmcam.jar com.smarttof.dmcam.sample.sampleBasicUi
	
* Linux下使用java示例

#. 在linux下安装openjdk-7-jdk用于java扩展::

    sudo apt-get install openjdk-7-jdk
	
#. 在SDK中的linux/java目录下的对应位数的java包拷贝到linux/samples/java目录，运行javac命令进行编译::

    javac –cp .:dmcam.jar ./com/smarttof/dmcam/sample/sampleBasic.java
    javac –cp .:dmcam.jar ./com/smarttof/dmcam/sample/sampleBasicUi.java
	
#. 在linux/samples/java目录中java目录运行，如果有些动态库没有找到，需要指定LD_LIBRARY_PATH::

    LD_LIBRARY_PATH=$LD_LIBRARY_PATH:$(pwd) java –cp .:dmcam.jar com.smarttof.dmcam.sample.sampleBasic
	
    LD_LIBRARY_PATH=$LD_LIBRARY_PATH:$(pwd) java –cp .:dmcam.jar com.smarttof.dmcam.sample.sampleBasicUi
	

Python Sample 使用流程
------------------------

#. 安装python样例所运行的库

   SDK中分别为windows和linux平台提供了支持smarttof模组的python扩展库，并且对应不同的python版本，方便用户选择适合的开发环境。下图是python扩展库的版本支持列表
 
	.. list-table:: windows 扩展
		:widths: 60 80
		:header-rows: 1

		* - 支持版本
		  - 扩展库名
		* - python2.7 32位
		  - dmcam-xxx-cp27-cp27m-win32.whl
		* - python3.4 32位
		  - dmcam-xxx-cp34-cp34m-win32.whl
		* - python3.5 32位
		  - dmcam-xxx-cp35-cp35m-win32.whl
		* - python3.6 32位
		  - dmcam-xxx-cp36-cp36m-win32.whl
		* - python2.7 64位
		  - dmcam-xxx-cp27-cp27m-win_amd64.whl
		* - python3.4 64位
		  - dmcam-xxx-cp34-cp34m-win_amd64.whl
		* - python3.5 64位
		  - dmcam-xxx-cp35-cp35m-win_amd64.whl
		* - python3.6 64位
		  - dmcam-xxx-cp36-cp36m-win_amd64.whl
		  
	.. list-table:: linux 扩展
		:widths: 60 80
		:header-rows: 1

		* - 支持版本
		  - 扩展库名
		* - python2.7 64位
		  - dmcam-xxx-cp27-cp27mu-linux_x86_64.whl
		* - python3.4 64位
		  - dmcam-xxx-cp34-cp34m-linux_x86_64.whl
		* - python3.5 64位
		  - dmcam-xxx-cp35-cp35m-linux_x86_64.whl
   
   .. note::
        上面扩展库中的xxx对应的是发布的版本
 
#. 安装支持样例运行的所需的其他库

   安装numpy、matplotlib、pygame、PyQt5、pyqtgraph,可以通过以下命令安装::
 
     pip install -r requirement.txt
 
   .. note::
        在python2.7或者python3.4环境下安装PyQt5可能回导致失败，可以换成安装PyQt4
 
#. Python 样例使用
 
   在使用python开发时，先安装对导入dmcam包后，python中使用的API函数跟dmcam.h中的函数名有所区别。C库中的API形式如dmcam_xxx_xxx,例如dmcam_dev_open,而在python中调用dmcam库时，形式为dmcam.xxx_xxx,打开设备为dmcam.dev_open。
   
   * Python 下最简采集流程
   
   下面是python下的最简采集流程::
	
	#初始化
	dmcam.init()
	...
	#打开设备
	dev = dmcam.dev_open()
	#设置采集缓存
	dmcam.cap_set_frame_buffer(dev,None,FRAME_SIZE*FRAME_BUF_FCNT)
	...
	#开始采集
	dmcam.cap_start(dev)
	#获得采集数据
	ret = dmcam.cap_get_frames(dev,1,f,finfo)
	w = finfo.frame_info.width
	h = finfo.frame_info.height
	#获得深度数据
	dist_cnt,dist = dmcam.frame_get_distance(dev,w*h,f,finfo.frame_info)
	#获取灰度数据
	gray_cnt,gray = dmcam.frame_get_gray(dev,w*h,f,finfo.frame_info)
	#停止采集
	dmcam.cap_stop(dev)
	...
	dmcam.uninit()
	
   * Python 参数设置
   
   下面是对模组参数设置的示例代码，展示python下对模组的参数设置，这里是设置模式、帧率等::
   
	wparams ={
	dmcam.PARAM_DEV_MODE: dmcam.param_val_u(),
	dmcam.PARAM_FRAME_RATE: dmcam.param_val_u(),
	dmcam.PARAM_ILLUM_POWER: dmcam.param_val_u(),
	}
	wparams[dmcam.PARAM_DEV_MODE].dev_mode = 1
	wparams[dmcam.PARAM_FRAME_RATE].frame_rate.fps = 30
	wparams[dmcam.PARAM_ILLUM_POWER].illum_power.persent = 30
	ret = dmcam.param_batch_set(device,wparams)
	
   * Python下滤波功能的使用
   
   下面是在python下开启模组的幅值滤波、自动积分、多模组消除串扰等功能::
   
	#开启幅值滤波
	amp_min_val = dmcam.filter_args_u()
	amp_min_val.min_amp = 30	#设置幅值滤波阈值
	dmcam.filter_enable(dev,dmcam.DMCAM_FILTER_ID_AMP,amp_min_val,sys.getsizeof(amp_min_val))	#开启幅值滤波

	# 开启自动积分时间
	intg_auto_arg = dmcam.filter_args_u()
	intg_auto_arg.sta_ratio = 5	#设置曝光点参数，一般为5
	dmcam.filter_enable(dev,dmcam.DMCAM_FILTER_ID_AUTO_INTG,intg_auto_arg,sys.getsizeof(intg_auto_arg))	#开启自动曝光

	# 开启消除串扰
	delay = dmcam.filter_args_u()
	delay.sync_delay = 0; #random delay
	if INTERFERENC_CHECK_EN:	#需检测是否使能
	dmcam.filter_enable(dev,dmcam.DMCAM_FILTER_ID_SYNC_DELAY,delay,sys.getsizeof(delay))

OpenNI2 Sample 使用流程
------------------------

* Windows下使用OpenNI2

在windows平台上，需要将支持OpenNI2的smarttof的相关动态库拷贝到安装OpenNI2的指定目录下，这里以OpenNI2 V2.2版本为例，需要将提供的smarttof模组驱动库拷贝到安装目录下的\Redist\OpenNI2\Drivers下。如果直接使用OpenNI2提供的NiViewer工具，则将smarttof的驱动库文件拷贝到NiViewer目录下的Tools\OpenNI2\Drivers下，这时连上模组后可以直接通过NiViewer使用模组进行采集和显示。

需要拷贝的支持OpenNI的文件包括以下几个：

	* smarttof.dll
	* libdmcam.dll
	* libdmcam.h
	
* 使用Openni的smarttof样例

SDK中提供了使用openni进行模组数据采集和参数基本设置的样例工程，样例基本概括展示了如何使用Openni的进行模组的使用，在样例工程中，如果使用采集样例将sample_set_param.cpp从生成中排除，使用参数设置样例则将main.cpp从生成中排除。

	- 采集样例
	
	在采集样例中，展示了通过Openni采集了模组的200帧数据，设备的URI定为SMARTTOFURI,或者直接为ANY_DEVICE。

	- 参数设置样例
	
	参数设置样例主要展示一些模组特有的参数设置和获取以及一些滤波功能的开启和关闭，这里的相关设置主要通过Openni的setProperty和getProperty设置和获取。下面具体展示进行参数设置和获取的具体代码.
	
代码如下::
	
	//获取参数
	dmcam_param_item_t rpm_intg;
	rpm_intg.param_id = PARAM_INTG_TIME;	//读取参数为积分时间
	rpm_intg.param_val_len = sizeof(rpm_intg.param_val.intg.intg_us);
	depth.getProperty(PROPERTY_ID_PARAM_GET, &rpm_intg);//获取积分时间
	printf("INTG is:%d us\n", rpm_intg.param_val.intg.intg_us);

	//设置参数
	dmcam_param_item_t wparam;
	wparam.param_id = PARAM_INTG_TIME;  //设置参数为积分时间
	wparam.param_val.intg.intg_us = 1000;//设置积分时间的大小
	wparam.param_val_len = sizeof(wparam.param_val.intg.intg_us);
	depth.setProperty(PROPERTY_ID_PARAM_SET, (void *)&wparam, sizeof(wparam));

	//开启最小幅值滤波功能
	dmcam_filter_args_u amp_min_val;
	amp_min_val.min_amp = 30;  //设置最小幅值滤波值
	depth.setProperty(PROPERTY_ID_FILTER_AMP_ENABLE,&amp_min_val);//开启设置最小幅值滤波
	printf("frame rate:%d fps\n", rparam.param_val.frame_rate.fps);

ROS Sample 使用流程
------------------------

ROS的具体使用参考SDK中doc下《SmartTof_SDK_ROS用户手册.pdf》。

.. toctree::
	:maxdepth: 1
	
	./rosuseguide.rst
	
	
Android Sample 使用流程
------------------------

* 硬件连接

在原来模组连接PC的基础上，再准备一根手机的OTG连接线,将原来连接PC的那端通过OTG连接线连接手机.

* 软件安装

 #. Android手机安装SDK中Android\tools\bin目录下的SmartTOFViewer.apk文件，安装完成后点即可运行。
 
 #. 用户也可以使用Eclipse导入Android\tools\src下工程，自己生成apk后安装运行，有新版SDK发布时，将SDK中Android\lib目录下的文件更新到工程，即可生成新版的SmartTOFViewer.apk文件。







   

  




