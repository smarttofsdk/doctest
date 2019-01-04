dmcam Java扩展概述
=======================

dmcam 提供的Java扩展可方便基于Java的开发人员基于 SmartToF_ 相机进行快速的二次开发。本文档主要描述Java扩展的安装以及API和C的关联和区别。 

Java扩展的安装
+++++++++++++++++++++++

* Window 平台

  * 支持的系统： 

    - Windows 7/8/10 32bit/64bit 
    - JDK >= 1.8

  * Java扩展动态库包括：

    - dmcam.jar: Java 扩展动态库，可导入Java 工程.
    - dmcam_java.dll: Java dmcam的扩展适配库
    - libdmcam.dll: dmcam core lib

  * 安装方式
  
    - 将以上dll加入PATH路径或复制到执行文件目录。
    - Java 工程中引用 `dmcam.jar`

* Linux

  * 支持的系统：

    - Linux 64bit (Ubuntu 14.04/16.04 tested)
    - Open JDK >= 7

  * Java扩展动态库包括：
  
    - dmcam.jar: Java 扩展动态库，可导入Java 工程.
    - libdmcam_java.so: Java dmcam的扩展适配库
    - libdmcam.so: dmcam core lib  
  
  * 安装方式
  
    - 设置 `LD_LIBRAYR_PATH` 包含上述so/dll目录, 或将动态库放入系统库目录下，例如： `/usr/local/lib/`
  
Java API 说明
++++++++++++++++++++++


Java中的模组API和C库中 **dmcam.h** 中定义的API基本一一对应。

- Java扩展默认的名字空间为: `com.smarttof.dmcam` 。 可通过 `import` 方式导入:

  .. code-block:: Java
    
        import com.smarttof.dmcam.*;

        public class sampleBasic{
	    public static void main(String[] args) {
            dmcamDevArray devs = new dmcamDevArray(16);
		    int cnt = dmcam.dev_list(devs.cast(), 16);
        }

- API命名映射关系(C->Java)： **dmcam_xxxxx(...) -> dmcam.xxxxx(...)** 。 例如 `dmcam_dev_open` 被映射为 `dmcam.dev_open`

     
- 结构体映射关系(C->Java): **dmcam_xxxxx -> xxxx()** 。 结构体被映射为Java中的一个类。例如通过如下方式创建一个 `dmcam_frame_info_t` 结构体:

  .. code-block:: Java

      finfo = new frame_info_t()

  .. caution::

      Java扩展加载时候会自动调用 `dmcam.init(null)`， 释放的时候会自动调用 `dmcam.uninit()`。因此不必在程序中使用 `dmcam.init()` 和 `dmcam.uninit()`

- 访问结构体的成员变量： **obj.field -> obj.getField()/setField** 。 成员变量的访问需通过成员变量名对应的 `get/set` 方法进行。例如：

  .. code-block:: Java

     cap_cfg_t cfg = new cap_cfg_t(); 
     cfg.setCache_frames_cnt(10);  // cfg.cache_frame_cnt = 10
     cfg.setOn_error(null);        // cfg.on_error = NULL
     /* ... */

- `NULL` 被映射为 `null` 。例如:
  
  .. code-block:: Java

      dmcam.dev_open(null) // dmcam_dev_open(NULL)

- 以下Java接口和C的API有差异，需要注意。
  
  `dmcam.dev_list()`
    Java中通过如下方式获取设备列表。其返回值为就绪设备数量。使用样例如下:

    .. code-block:: Java

            dmcamDevArray devs = new dmcamDevArray(16);
            int cnt = dmcam.dev_list(devs.cast(), 16);

            System.out.printf("found {0} device\n", cnt);
    
  `dmcam.param_batch_set()`
   Java中设置参数相对C比较复杂一些, 需要构造param_item_t实例。 具体使用样例如下:

   .. code-block:: Java

      int pwr_percent = 100;
      param_item_t wparam = new param_item_t();
      dmcamParamArray wparams = new dmcamParamArray(1);
   
      wparam.setParam_id(dev_param_e.PARAM_ILLUM_POWER);
      wparam.getParam_val().getIllum_power().setPercent((short) pwr_percent);
   
      wparams.setitem(0, wparam);
      if (!dmcam.param_batch_set(dev, wparams.cast(), 1)) {
          System.out.printf(" set illu_power to %d %% failed\n", pwr_percent);
      }

  `dmcam.param_batch_get(dev, list)`
    Java中设置参数相对C比较复杂一些, 需要构造param_item_t实例。 具体使用样例如下:

    .. code-block:: Java

            param_item_t r_fps = new param_item_t();
            r_fps.setParam_id(dev_param_e.PARAM_FRAME_RATE);
            param_item_t r_intg = new param_item_t();
            r_intg.setParam_id(dev_param_e.PARAM_INTG_TIME);
           
            dmcamParamArray rparams = new dmcamParamArray(2);
            rparams.setitem(0, r_fps);
            rparams.setitem(1, r_intg);

            if (dmcam.param_batch_get(dev, rparams.cast(), 2)) {
                System.out.printf("fps = %d, intg = %d", 
                        (int)rparams.getitem(0).getParam_val().getFrame_rate().getFps(),
                        (int)rparams.getitem(1).getParam_val().getIntg().getIntg_us());
            }

  `dmcam.set_callback_on_frame_ready 和 dmcam.set_callback_on_error`
   Java扩展中不支持回调函数。采集时，可以参考如下设置：

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
