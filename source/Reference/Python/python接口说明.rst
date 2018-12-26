python扩展接口说明
=======================

在python下进行smarttof模组的二次开发，需要安装封装了模组api接口的dmcam包，
适用于各个python版本的dmcam已经上传Pypi网站，直接输入下面命令进行安装更新::

	pip install -U dmcam
	
python相关API
++++++++++++++++++++++

Python中的模组API接口和dmcam.h中的定义的API接口格式上有些不同，python中
所有模组相关的API接口都以dmcam.开头。如C中定义一个帧数据类型 ``dmcam_frame_t finfo``,
在python中数据类型则如下表示 ``finfo = dmcam.frame_t()``,如果调用C库中的 ``dmcam_init(NULL)``,
在python中调用则为 ``dmcam.init(None)``,如打开默认设备调用C库为 ``dmcam_dev_open(NULL)``,
在python中则为 ``dmcam.dev_open(None)``。所以在python下开发时，注意相关AP接口的书写格式。

下表列出了一些常用的API接口对比：

.. list-table::
	:widths: 60 60
	:header-rows: 1
	
	* - C库核心函数
	  - python调用函数
	* - dmcam_init
	  - dmcam.init
	* - dmcam_dev_list
	  - dmcam.dev_list	  
	* - dmcam_dev_open
	  - dmcam.dev_open
	* - dmcam_dev_close
	  - dmcam.dev_close	
	* - dmcam_cap_config_set
	  - dmcam.cap_config_set
	* - dmcam_cap_set_callback_on_error
	  - dmcam.cap_set_callback_on_error	  
	* - dmcam_param_batch_set
	  - dmcam.param_batch_set	  
	* - dmcam_cap_get_frames
	  - dmcam.cap_get_frames
	* - dmcam_frame_get_distance
	  - dmcam.frame_get_distance
	* - dmcam_frame_get_gray
	  - dmcam.frame_get_gray