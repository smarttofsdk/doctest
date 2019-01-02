OpenNI2驱动说明
=================

为了支持OpenNI2中的框架实现对SmartToF模组的调用，SDK中提供了相应支持的驱动库samrttof.dll,
该驱动依循OpenNI2在OniDriverAPI.h中的定义，主要包括了DriverService、DriverBase、DeviceBase、StreamBase
这几个类别，smarttof.dll的驱动源码在SDK中一同发布。

SmartToF模组的设置
++++++++++++++++++++

SmartToF中的所有相关的参数设置和滤波功能的使用都通过smarttofStream类中的setProperty函数执行，根据setProperty
中的propertyId进行对应得设置。

下表列出了property的属性ID:

.. list-table::
	:widths: 60 60
	:header-rows: 1
	
	* - 功能ID
	  - 说明
	* - PROPERTY_ID_PARAM_SET
	  - 模组参数设置ID
	* - PROPERTY_ID_PARAM_GET
	  - 模组参数获取ID
	* - PROPERTY_ID_FILTER_LEN_CALIB_ENABLE
	  - 镜头滤波使能
	* - PROPERTY_ID_FILTER_LEN_CALIB_DISABLE
	  - 镜头滤波关闭
	* - PROPERTY_ID_FILTER_PIXEL_CALIB_ENABLE
	  - 像素滤波使能
	* - PROPERTY_ID_FILTER_PIXEL_CALIB_DISABLE
	  - 像素滤波关闭
	* - PROPERTY_ID_FILTER_AMP_CALIB_ENABLE
	  - 幅值滤波使能
	* - PROPERTY_ID_FILTER_AMP_CALIB_DISABLE
	  - 幅值滤波关闭
	* - PROPERTY_ID_FILTER_AUTO_INTG_ENABLE
	  - 自动曝光使能
	* - PROPERTY_ID_FILTER_AUTO_INTG_DISABLE
	  - 自动曝光关闭
	* - PROPERTY_ID_FILTER_TEMP_MONITOR_ENABLE
	  - 温度监控使能
	* - PROPERTY_ID_FILTER_TEMP_MONITOR_DISABLE
	  - 温度监控关闭
	* - PROPERTY_ID_FILTER_HDR_ENABLE
	  - HDR功能使能
	* - PROPERTY_ID_FILTER_HDR_DISABLE
	  - HDR功能关闭

OpenNI2下模组设置示例代码
--------------------------

OpenNI2下可以通过setProperty将以上列表中的属性ID设置到SmartToF模组中去，
具体设置的代码示例可以参考下面的设置积分时间代码::

    dmcam_param_item_t wparam;	//setting integration time
    wparam.param_id = PARAM_INTG_TIME;
    wparam.param_val.intg.intg_us = intg;
    wparam.param_val_len = sizeof(wparam.param_val.intg.intg_us);
    depth.setProperty(PROPERTY_ID_PARAM_SET, (void *)&wparam, sizeof(wparam));

获取模组设置的代码如下::

    dmcam_param_item_t rparam;	//getting framerate
    rparam.param_id = PARAM_FRAME_RATE;
    rparam.param_val_len = sizeof(rparam.param_val.frame_rate.fps);
    depth.getProperty(PROPERTY_ID_PARAM_GET, &rparam);
    printf("frame rate:%d fps\n", rparam.param_val.frame_rate.fps);

    
