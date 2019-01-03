dmcam C#扩展概述
=======================

dmcam 提供的C#扩展可方便基于.net C#的开发人员基于 SmartToF_ 相机进行快速的二次开发。本文档主要描述C#扩展的安装以及API和C的关联和区别。 

C#扩展的安装
+++++++++++++++++++++++


C# 扩展目前支持以下系统

* Windows 32bit/64bit with .Net framework >= 3.5 
* Linux 64bit (Ubuntu 14.04/16.04) with Mono

C# 扩展包括以下文件:

Window
######

* C#扩展动态库包括：

  - dmcam_csharp.dll: C# 扩展动态库，可导入C# 工程.
  - dmcam_csharp_adapter.dll: C# dmcam的扩展适库配
  - libdmcam.dll: dmcam core lib

* 安装方式

  - 将以上dll加入PATH路径或复制到执行文件目录。
  - C# 工程中引用 `dmcam_csharp.dll`

Linux
#####

* C#扩展动态库包括：

  - dmcam_csharp.dll: C# 扩展动态库，可导入C# 工程.
  - dmcam_csharp_adapter.so: C# dmcam的扩展适配库
  - libdmcam.so: dmcam core lib  

* 安装方式

  - 设置 `LD_LIBRAYR_PATH` 包含上述so/dll目录, 或将动态库放入系统库目录下，例如： `/usr/local/lib/`

C# API 说明
++++++++++++++++++++++


C#中的模组API和C库中 **dmcam.h** 中定义的API基本一一对应。

- C#扩展默认的名字空间为: `com.smarttof` 。 可通过 `using` 方式导入:

    .. code-block:: C#
    
        using com.smarttof;
        namespace sampleBasic {
        public class sampleBasic{
            public static void Main(string[] argv) {
                dmcam.init(null);
                /* ... */
                dmcam.uninit();
        }

- API命名映射关系(C->C#)： **dmcam_xxxxx(...) -> dmcam.xxxxx(...)** 。 例如 `dmcam_dev_open` 被映射为 `dmcam.dev_open`

     
- 结构体映射关系(C->C#): **dmcam_xxxxx -> xxxx()** 。 结构体被映射为C#中的一个类。例如通过如下方式创建一个 `dmcam_frame_info_t` 结构体:

    .. code-block:: C#

      finfo = new frame_info_t()

- `NULL` 被映射为 `null` 。例如:
  
    .. code-block:: C#

      dmcam.init(null) // dmcam_init(NULL)

- 以下C#接口和C的API有差异，需要注意。
  
  `dmcam.dev_list()`
    C#中通过如下方式获取设备列表。其返回值为就绪设备数量。使用样例如下:

    .. code-block:: C#

            dmcamDevArray devs = new dmcamDevArray(16);
            int cnt = dmcam.dev_list(devs.cast(), 16);

            Console.Write("found {0} device\n", cnt);
    
  `dmcam.param_batch_set()`
   C#中设置参数相对C比较复杂一些, 需要构造param_item_t实例。 具体使用样例如下:

   .. code-block:: C#

            param_item_t p_fps = new param_item_t();
            p_fps.param_id = dev_param_e.PARAM_FRAME_RATE;
            p_fps.param_val.frame_rate.fps = 15;

            param_item_t p_intg = new param_item_t();
            p_intg.param_id = dev_param_e.PARAM_INTG_TIME;
            p_intg.param_val.intg.intg_us = 1000;
           
            dmcamParamArray wparams = new dmcamParamArray(2);
            wparams.setitem(0, p_fps);
            wparams.setitem(1, p_intg);

            if (!dmcam.param_batch_set(dev, wparams.cast(), 2)) {
                Console.WriteLine(" set param failed\n");
            } 
            

  `dmcam.param_batch_get(dev, list)`
    C#中设置参数相对C比较复杂一些, 需要构造param_item_t实例。 具体使用样例如下:

    .. code-block:: C#

            param_item_t r_fps = new param_item_t();
            r_fps.param_id = dev_param_e.PARAM_FRAME_RATE;
            param_item_t r_intg = new param_item_t();
            r_intg.param_id = dev_param_e.PARAM_INTG_TIME;
           
            dmcamParamArray rparams = new dmcamParamArray(2);
            rparams.setitem(0, r_fps);
            rparams.setitem(1, r_intg);

            if (!dmcam.param_batch_get(dev, rparams.cast(), 2)) {
                Console.WriteLine(" get param failed\n");
            } else {
                Console.WriteLine("fps = {0}, intg = {1}", 
                        (int)rparams.getitem(0).param_val.frame_rate.fps,
                        (int)rparams.getitem(1).param_val.intg.intg_us);
            }

  `dmcam.set_callback_on_frame_ready 和 dmcam.set_callback_on_error`
   C#扩展中不支持回调函数。采集时，可以参考如下设置：

   .. code-block:: C#

            cap_cfg_t cfg = new cap_cfg_t();
            cfg.cache_frames_cnt = 10;
            cfg.on_error= null;
            cfg.on_frame_ready= null;
            cfg.en_save_replay= 0;
            cfg.en_save_dist_u16= 0;
            cfg.en_save_gray_u16= 0;
            cfg.fname_replay= null;

            dmcam.cap_config_set(dev, cfg);

  
.. _`Pypi项目主页`: https://pypi.org/project/dmcam/
.. _SmartToF: http://www.smarttof.com
