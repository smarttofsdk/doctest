dmcam Android扩展概述
=======================

dmcam 提供的Android扩展可方便Android开发人员基于 SmartToF_ 相机进行快速的二次开发,本文档主要描述Android扩展的使用以及API和C的关联和区别。

Android扩展的安装
+++++++++++++++++++++++

* 支持的系统：

  - Android 4.4.2
  
* Android扩展动态库包括(ARM V5和ARM V7架构)

  - libdmcam.so: dmcam core lib
  - libdmcam_java.so: Java dmcam的扩展适配库
  - dmcam_android.jar: android 扩展动态库，可导入Android 工程
  - libusb1.0.so: usb设备驱动库
  
* 安装方式

  - 将以上的所有so库加入到Android工程下的libs
  - Android工程下再加入 `dmcam.jar`
  
Android API 说明
++++++++++++++++++++

Android的app开发是基于Java语言的，所以Android中的主要API说明和Java中的
API说明基本一致，都和C库中的 **dmcam.h** 中定义的API基本一一对应。

- Android中扩展的默认名字空间为: `com.smarttof.dmcam` 。 可通过 `import` 方式导入：

  .. code-block:: Java
  
		import com.smarttof.dmcam.*;
		
		public boolean devSetFrameRate(dev_t dev, int fps){
			if (dev == null)
				return false;
			
			param_item_t wparam = new param_item_t();
			dmcamParamArray wparams = new dmcamParamArray(1);
			
			wparam.setParam_id(dev_param_e.PARAM_FRAME_RATE);
			wparam.getParam_val().getFrame_rate().setFps(fps);
		
			wparams.setitem(0, wparam);
			logUI("DMCAM",
					String.format("set fps = %d\n", wparams.getitem(0)
							.getParam_val().getFrame_rate().getFps()));
			if (!dmcam.param_batch_set(dev, wparams.cast(), 1)) {
				logUI("DMCAM", String.format(" set fps to %d failed\n", fps));
				return false;
			}
			return true;
		}
		
- Android中的调用的API和Java中调用的API基本相同，映射关系都如: **dmcam_xxxxx(...) -> dmcam.xxxxx(...)** 。
  例如 `dmcam_dev_close` 被映射为 `dmcam.dev_close`
  
- 结构体映射关系： **dmcam_xxxxx -> xxxxx()** 。结构体被映射为java中的一个类。例如通过如下方式创建一个 `dmcam_param_item_t` 结构体:
 
  .. code-block:: Java
  
	  wparam = new param_item_t();
	  
  .. caution::
  
      在Android中打开设备时调用的API为 `dmcam.dev_open_by_fd`,不是其他环境下的 `dmcam.dev_open`

- 访问结构体的成员变量： **obj.field -> obj.getField()/setField** 。 成员变量的访问需通过成员变量名对应的 `get/set` 方法进行。例如：

  .. code-block:: Java

     cap_cfg_t cfg = new cap_cfg_t(); 
     cfg.setCache_frames_cnt(10);  // cfg.cache_frame_cnt = 10
     cfg.setOn_error(null);        // cfg.on_error = NULL
     /* ... */

- `NULL` 被映射为 `null` 。例如:
  
  .. code-block:: Java

      cfg.setOn_error(null);

- 以下是在Android中调用API与C中的一些区别，需要注意。

  `dmcam.dev_open_by_fd()`
	在Android下打开设备，需要调用专为Android设计的API dmcam.dev_open_by_fd(),具体使用样例如下：
	
   .. code-block:: Java
   
	   UsbDeviceConnection connection = usbManager.openDevice(usbDevice);
	   fd = connection.getFileDescriptor();
	   dev = dmcam.dev_open_by_fd(fd);
	   
  `dmcam.param_batch_set()`
	需要构造param_item_t实例，具体样例如下:
	
   .. code-block:: Java
   
      param_item_t wparam = new param_item_t();
	  dmcamParamArray wparams = new dmcamParamArray(1);
	  
	  wparam.setParam_id(dev_param_e.PARAM_INTG_TIME);
	  wparam.getParam_val().getIntg().setIntg_us(expoUs);
	  
	  wparams.setitem(0, wparam);
	  if (!dmcam.param_batch_set(dev, wparams.cast(), 1)) {
			logUI("DMCAM",
					String.format(" set exposure to %d us failed\n", expoUs));
			return false;
	  }
	  
  `dmcam.param_batch_get()`
	获取参数也要构造实例，具体样例如下:
	
   .. code-block:: Java
   
	  param_item_t r_fps = new param_item_t();
	  r_fps.setParam_id(dev_param_e.PARAM_FRAME_RATE);
	  
	  dmcamParamArray rparam = new dmcamParamArray(1);
	  rparam.setitem(0,r_fps);
	  
	  if (dmcam.param_batch_get(dev, rparam.cast(), 1)) {
		logUI("DMCAM",
				String.format(" get frame_rate %d fps\n",  (int)rparam.getitem(0).getParam_val().getFrame_rate().getFps()));
	  }
	  
  `dmcam.set_callback_on_frame_ready 和 dmcam.set_callback_on_error`
   Android扩展中不支持回调函数。采集时，可以参考如下设置：

   .. code-block:: Java

        cap_cfg_t cfg = new cap_cfg_t();
        cfg.setCache_frames_cnt(10);
        cfg.setOn_error(null);
        cfg.setOn_frame_ready(null);
        cfg.setEn_save_replay((short)0);
        cfg.setEn_save_dist_u16((short)0);
        cfg.setEn_save_gray_u16((short)0);
        cfg.setFname_replay(null);

        dmcam.cap_config_set(dev, cfg);	  

.. _SmartToF: http://www.smarttof.com






















