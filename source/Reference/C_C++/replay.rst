录像生成与读取回放代码说明
==========================

在模组的算法评估中，评估前的一个主要准备工作就是录像文件的
获取，在SmartToFViewer中已经介绍如何获取通过SmartToFViewer进行
录像以及播放，这里介绍如何通过程序进行录像和读取录像文件，以及主要
API的介绍。

录像文件的设置
++++++++++++++++

是否保存录像文件以及录像文件保存何种数据主要通过在程序中设置 ``dmcam_cap_cfg_t`` 的数据
结构，具体代码如下

.. code-block:: C

    /* set capture config */
   dmcam_cap_cfg_t cap_cfg = {
    .cache_frames_cnt = FRAME_BUF_FCNT, /* FRAME_BUF_FCNT frames can be cached in frame buffer*/
    .on_error = NULL,      /* No error callback */
    .on_frame_ready = NULL, /* No frame ready callback*/
    .en_save_replay = false, /* false save raw data stream to replay file */
    .en_save_dist_u16 = false, /* disable save dist stream into replay file */
    .en_save_gray_u16 = false, /* disable save gray stream into replay file*/
    .fname_replay = NULL, /* replay filename */
   };

上述结构体参数中跟录像文件相关的主要是 ``en_save_replay`` ``en_save_dist_u16`` ``en_save_gray_u16`` 这几个
参数，这几个参数的具体说明如下：

- 支持SmartToF SDK标准回放
  
  如果只要支持SmartToF SDK标准的回放，只要将上述的 ``en_save_replay`` 设置为 ``true``,其他两个设置为 ``false``.

- 兼容OpenNI工具的回放(如NiViewer)
 
  支持OpenNI工具的回放，如NiViewer的播放，这时需要将 ``en_save_replay`` 设置 ``false``, ``en_save_dist_16`` 和 `` en_save_gray_u16``都
  设置为 ``true`` 或者任意一个设置 ``true``,如果都设置为使能，则表示存储深度图和灰度图，其中一个使能则使能 ``en_save_dist_u16`` 为深度图，
  使能 ``en_save_gray_u16`` 则表示保存的为灰度图。

录像文件的读取
+++++++++++++++++

SmartToF 的录像文件"xxx.oni"可以被模拟成标准的DMCAM设备,可以通过 ``dmcam_dev_open_by_uri`` 函数打开，
如文件名为"test.oni",则读取文件名代码如下

.. code-block:: C

	dev = dmcam_dev_open_by_uri("test.oni") 	//or file://test.oni

.. caution::

	模拟dmcam设备和真实dmcam设备的由主要以下区别

	- 模拟设备时，凡是SDK中基于原始DCS数据的处理均可调节和叠加，例如:深度滤波、最小幅值滤波、像素校准、镜头校准等。

	- 模拟设备时，采集DCS原始数据的相关参数再模拟设备中调节是无效的，例如曝光时间，HDR功能等。
