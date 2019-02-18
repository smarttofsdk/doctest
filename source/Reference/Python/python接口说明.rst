dmcam python扩展概述
=======================

python 扩展的安装
+++++++++++++++++++++++


dmcam_ 提供了基于标准python wheel的扩展，该扩展可以通过pip直接进行安装，支持Windows和Linux的36位和64位环境，详见 `Pypi项目主页`_ 。安装命令为::

	pip install -U dmcam

python API 说明
++++++++++++++++++++++


Python中的模组API和C库中 **dmcam.h** 中定义的API基本一一对应。

- python扩展中默认的包名为: `dmcam` 。 可通过 `import` 直接导入::

    import dmcam

- API命名映射关系(C->Python)： **dmcam_xxxxx(...) -> dmcam.xxxxx(...)** 。 例如 `dmcam_dev_open` 被映射为 `dmcam.dev_open`

     
- 结构体映射关系(C->Python): **dmcam_xxxxx -> dmcam.xxxx()** 。 结构体被映射为Python中的一个类。例如通过如下方式创建一个 `dmcam_frame_info_t` 结构体::

    finfo = dmcam.frame_info_t()

- `NULL` 被映射为 `None` 。例如::
  
    dmcam.init(None) # dmcam_init(NULL)

- 以下Python接口和C的API有差异，需要注意。
  
  `dmcam.dev_list()`
    Python中对C接口进行了简化，可以直接通过下列方式获取设备列表。其返回值为 `dmcam.dev_t()` 的列表。使用样例如下::

     devs = dmcam.dev_list()
     if devs is None:
        print(" No device found")
     else:
        print("found %d device" % len(devs))
        print(" Device URIs:")
        for i, d in enumerate(devs):
            print("[#%d]: %s" % (i, dmcam.dev_get_uri(d, 256)[0]))

  `dmcam.param_batch_set(dev, dict)`
   Python中对C接口进行了简化，直接传递一个`dict`, 而不必构造比较复杂的 `dmcam_param_item_t` 结构体及其长度参数。 使用样例如下::

      wparams = {
          dmcam.PARAM_FRAME_RATE: dmcam.param_val_u(),
          dmcam.PARAM_INTG_TIME: dmcam.param_val_u(),
      }
      wparams[dmcam.PARAM_FRAME_RATE].frame_rate.fps = 15
      wparams[dmcam.PARAM_INTG_TIME].intg.intg_us = 1000
      
      if not dmcam.param_batch_set(dev, wparams):
          print(" set parameter failed")
    
  `dmcam.param_batch_get(dev, list)`
   Python中对C接口进行了简化，直接传递需要获取参数的`list`, 而不必构造比较复杂的 `dmcam_param_item_t` 结构体及其长度参数。 使用样例如下::

            # get intg from device
            param_vals = dmcam.param_batch_get(dev, [dmcam.PARAM_INTG_TIME])  # type: list[dmcam.param_val_u]
            param_intg_us = param_vals[0].intg.intg_us

  `dmcam.set_callback_on_frame_ready 和 dmcam.set_callback_on_error`
   由于Python回调函数和C的差异。关于采集过程中回调函数的设置, 目前，python只支持通过上述两个接口分别设置 `frame_ready` 和 `error` 两种类型的回调。 不支持通过 `dmcam.cap_config_set(dev, cap_cfg_t)` 中的 `cap_cg_t` 进行回调函数的设置。 使用样例如下::

       def on_frame_rdy(dev, f):
           print("cap: idx=%d, num=%d" % (f.frame_fbpos, f.frame_count))
    
       def on_cap_err(dev, errnumber, errarg):
           print("caperr: %s" % dmcam.error_name(errnumber))

       cap_cfg = dmcam.cap_cfg_t()
       cap_cfg.cache_frames_cnt = 10  # frame buffer = 10 frames
       cap_cfg.on_frame_ready = None  # callback should be set by dmcam.cap_set_callback_on_frame_ready
       cap_cfg.on_cap_err = None      # callback should be set by dmcam.cap_set_callback_on_error
       cap_cfg.en_save_dist_u16 = False  # save dist into ONI file: which can be viewed in openni
       cap_cfg.en_save_gray_u16 = False  # save gray into ONI file: which can be viewed in openni
       cap_cfg.en_save_replay = False  # save raw into ONI file:  which can be simulated as DMCAM device
       cap_cfg.fname_replay = os.fsencode("replay_dist.oni")
       
       dmcam.cap_config_set(dev, cap_cfg)
       
       dmcam.cap_set_callback_on_frame_ready(dev, on_frame_rdy)
       dmcam.cap_set_callback_on_error(dev, on_cap_err)

  
下表列出了一些常用的API接口对比：

.. list-table:: python调用接口对比
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

.. _dmcam: https://pypi.org/project/dmcam/
.. _`Pypi项目主页`: https://pypi.org/project/dmcam/
