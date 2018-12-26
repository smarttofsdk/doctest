主要API接口说明
=======================

模组连接相关接口
+++++++++++++++++++++++

dmcam_init
^^^^^^^^^^^^^^^^^^^

.. list-table::
	:widths: 60 60
	:header-rows: 1
	
	* - 头文件
	  - #include “dmcam.h”
	* - 函数原型
	  - ``void dmcam_init(const char *log_fname)``
	* - 功能描述
	  - 模组初始化，dmcam层初始化
	* - 函数参数
	  - log_fname[in]:指定dmcam的日志文件名	  
	* - 函数返回值
	  - 无
	  
dmcam_dev_list
^^^^^^^^^^^^^^^^^^^	  

.. list-table::
	:widths: 60 60
	:header-rows: 1
	
	* - 头文件
	  - #include “dmcam.h”
	* - 函数原型
	  - ``int dmcam_dev_list(dmcam_dev_t *dev_list, int dev_list_num)``
	* - 功能描述
	  - 获取模组设备列表
	* - 函数参数1
	  - dev_list[in]:设备列表	  
	* - 函数参数2
	  - dev_list_num[in]：设备列表容量
	* - 函数返回值
	  - 设备个数

dmcam_dev_open
^^^^^^^^^^^^^^^^^^^	
	  
.. list-table::
	:widths: 60 60
	:header-rows: 1
	
	* - 头文件
	  - #include “dmcam.h”
	* - 函数原型
	  - ``dmcam_dev_t* dmcam_dev_open(dmcam_dev_t *dev)``
	* - 功能描述
	  - 打开指定的dmcam设备，如果未指定，尝试打开设备列表的第一个选项
	* - 函数参数
	  - dev[in]:指定的dmcam设备	  
	* - 函数返回值
	  - 如果NULL:设备打开失败	  

dmcam_dev_open_by_fd
^^^^^^^^^^^^^^^^^^^^^
	  
.. list-table::
	:widths: 60 60
	:header-rows: 1
	
	* - 头文件
	  - #include “dmcam.h”
	* - 函数原型
	  - ``dmcam_dev_t* dmcam_dev_open_by_fd(int fd)``
	* - 功能描述
	  - 用指定的fd打开指定的dmcam设备，在Android的USB设备中使用
	* - 函数参数
	  - fd[in]:指定的fd	  
	* - 函数返回值
	  - 如果NULL:设备打开失败

dmcam_dev_close
^^^^^^^^^^^^^^^^^^^	
	  
.. list-table::
	:widths: 60 60
	:header-rows: 1
	
	* - 头文件
	  - #include “dmcam.h”
	* - 函数原型
	  - ``void* dmcam_dev_close(dmcam_dev_t *dev)``
	* - 功能描述
	  - 关闭指定的dmcam设备
	* - 函数参数
	  - dev[in]:指定的dmcam设备  
	* - 函数返回值
	  - 无

dmcam_uninit
^^^^^^^^^^^^^^^^^^^	
	  
.. list-table::
	:widths: 60 60
	:header-rows: 1
	
	* - 头文件
	  - #include “dmcam.h”
	* - 函数原型
	  - ``void dmcam_uninit(void)``
	* - 功能描述
	  - 模组dmcam层复位
	* - 函数参数
	  - 无  
	* - 函数返回值
	  - 无
	  
模组参数设置相关接口
++++++++++++++++++++++

dmcam_param_batch_set
^^^^^^^^^^^^^^^^^^^^^^^

.. list-table::
	:widths: 60 100
	:header-rows: 1
	
	* - 头文件
	  - #include “dmcam.h”
	* - 函数原型
	  - ``dmcam_param_batch_set(dmcam_dev_t*dev,const dmcam_param_item_t *param_items, int item_cnt)``
	* - 功能描述
	  - 通用批量参数设置
	* - 函数参数1
	  - dev[in]:dmcam设备
	* - 函数参数2
	  - param_items[in]:要写参数条目，支持批量设置	
	* - 函数参数3
	  - item_cnt[in]:参数条目中参数个数
	* - 函数返回值
	  - true:成功 false:失败

dmcam_param_batch_get
^^^^^^^^^^^^^^^^^^^^^^^

.. list-table::
	:widths: 60 100
	:header-rows: 1
	
	* - 头文件
	  - #include “dmcam.h”
	* - 函数原型
	  - ``dmcam_param_batch_get(dmcam_dev_t*dev,const dmcam_param_item_t *param_items, int item_cnt)``
	* - 功能描述
	  - 通用批量参数设置
	* - 函数参数1
	  - dev[in]:dmcam设备
	* - 函数参数2
	  - param_items[out]:读取的参数条目，支持多个
	* - 函数参数3
	  - item_cnt[in]:参数条目中参数个数
	* - 函数返回值
	  - true:成功 false:失败
	  

模组数据采集相关接口
+++++++++++++++++++++	

dmcam_cap_set_frame_buffer
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. list-table::
	:widths: 60 100
	:header-rows: 1
	
	* - 头文件
	  - #include “dmcam.h”
	* - 函数原型
	  - ``bool dmcam_cap_set_frame_buffer(dmcam_dev_t *dev, uint8_t *frame_buf, uint32_t frame_buf_size)``
	* - 功能描述
	  - 设置帧缓冲区
	* - 函数参数1
	  - dev[in]:dmcam设备
	* - 函数参数2
	  - frame_buf[in]:用来存放frame数据的buffer，如果未指定，根据frame_buf_size在内部自动分配	
	* - 函数参数3
	  - frame_buf_size[in]:frame_buffer的大小
	* - 函数返回值
	  - true:成功 false:失败

dmcam_cap_set_callback_on_frame_ready
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. list-table::
	:widths: 60 100
	:header-rows: 1
	
	* - 头文件
	  - #include “dmcam.h”
	* - 函数原型
	  - ``void dmcam_cap_set_callback_on_frame_ready(dmcam_dev_t *dev, dmcam_cap_frdy_f on_cap_frdy)``
	* - 功能描述
	  - 注册一帧接收完成回调函数
	* - 函数参数1
	  - dev[in]:dmcam设备
	* - 函数参数2
	  - cb[in]:帧结束回调函数	
	* - 函数返回值
	  - 无

dmcam_cap_set_callback_on_error
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. list-table::
	:widths: 60 100
	:header-rows: 1
	
	* - 头文件
	  - #include “dmcam.h”
	* - 函数原型
	  - ``void dmcam_cap_set_callback_on_error(dmcam_dev_t *dev, dmcam_cap_err_f on_cap_err)``
	* - 功能描述
	  - 注册帧错误回调函数
	* - 函数参数1
	  - dev[in]:dmcam设备
	* - 函数参数2
	  - cb[in]:帧错误回调函数	
	* - 函数返回值
	  - 无

dmcam_cap_start
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. list-table::
	:widths: 60 100
	:header-rows: 1
	
	* - 头文件
	  - #include “dmcam.h”
	* - 函数原型
	  - ``bool dmcam_cap_start(dmcam_dev_t *dev)``
	* - 功能描述
	  - 启动采集
	* - 函数参数
	  - dev[in]:dmcam设备
	* - 函数返回值
	  - true:成功 false:失败

dmcam_cap_get_frames
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. list-table::
	:widths: 60 100
	:header-rows: 1
	
	* - 头文件
	  - #include “dmcam.h”
	* - 函数原型
	  - ``int dmcam_cap_get_frames(dmcam_dev_t *dev,uint32_t frame_num,uint8_t*frame_data,uint32_tframe_dlen, dmcam_frame_t *first_frame_info)``
	* - 功能描述
	  - 获取指定数目帧数据，并填入用户指定的缓冲
	* - 函数参数1
	  - dev[in]:dmcam设备
	* - 函数参数2
	  - frame_num[in]：采集的帧数
	* - 函数参数3
	  - frame_data[out]:帧数据
	* - 函数参数4
	  - frame_dlen[in]:帧数据缓冲长度
	* - 函数参数5
	  - frame_info[out]:第一帧信息
	* - 函数返回值
	  - 大于0表示采集到的帧数目 小于0表示出错

dmcam_cap_stop
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. list-table::
	:widths: 60 100
	:header-rows: 1
	
	* - 头文件
	  - #include “dmcam.h”
	* - 函数原型
	  - ``bool dmcam_cap_stop(dmcam_dev_t *dev)``
	* - 功能描述
	  - 停止采集
	* - 函数参数
	  - dev[in]:dmcam设备
	* - 函数返回值
	  - true:成功 false:失败  

采集数据处理相关接口
+++++++++++++++++++++

dmcam_frame_get_dist_f32
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. list-table::
	:widths: 60 100
	:header-rows: 1
	
	* - 头文件
	  - #include “dmcam.h”
	* - 函数原型
	  - ``dmcam_frame_get_dist_f32(dmcam_dev_t *dev, float *dst, int dst_len,uint8_t *src, int src_len, const dmcam_frame_info_t *finfo)``
	* - 功能描述
	  - 从帧获得的原始数据转换成距离数据
	* - 函数参数1
	  - dev[in]:dmcam设备
	* - 函数参数2
	  - dst[out]:距离数据，单位 m，如果过曝光则是65.5，曝光不足65.3	
	* - 函数参数3
	  - dst_len[in]：距离长度数据
	* - 函数参数4
	  - src[in]:原始数据	  
	* - 函数参数5
	  - src_len[in]:原始数据长度，字节
	* - 函数参数6
	  - finfo[in]:原始帧信息	  
	* - 函数返回值
	  - 返回距离数据个数
	  
dmcam_frame_get_gray
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. list-table::
	:widths: 60 100
	:header-rows: 1
	
	* - 头文件
	  - #include “dmcam.h”
	* - 函数原型
	  - ``int dmcam_frame_get_gray(dmcam_dev_t *dev, float *dst, int dst_len,uint8_t *src, int src_len, const dmcam_frame_info_t *finfo)``
	* - 功能描述
	  - 从帧获得的原始数据转换成灰度数据
	* - 函数参数1
	  - dev[in]:dmcam设备
	* - 函数参数2
	  - dst[out]:灰度数据 范围是0-65500	
	* - 函数参数3
	  - dst_len[in]：灰度数据长度
	* - 函数参数4
	  - src[in]:原始数据	  
	* - 函数参数5
	  - src_len[in]:原始数据长度，字节
	* - 函数参数6
	  - finfo[in]:原始帧信息	  
	* - 函数返回值
	  - 返回灰度数据个数
	  
dmcam_frame_get_pcl
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. list-table::
	:widths: 60 100
	:header-rows: 1
	
	* - 头文件
	  - #include “dmcam.h”
	* - 函数原型
	  - ``int dmcam_frame_get_pcl(dmcam_dev_t *dev, float *pcl, int pcl_len,const float *dist, int dist_len, int img_w, int img_h, const dmcam_camera_para_t *p_cam_param)``
	* - 功能描述
	  - 从获得的深度数据转换成点云数据
	* - 函数参数1
	  - dev[in]:dmcam设备
	* - 函数参数2
	  - pcl[out]:点云数据缓存, pcl[3i+0],pcl[3i+1],pcl[3i+2]分别作为第i个点在空间X轴Y轴Z轴的坐标	
	* - 函数参数3
	  - pcl_len[in]：点云数据长度
	* - 函数参数4
	  - dist[in]:深度数据缓存，单位是 m(float)	  
	* - 函数参数5
	  - dist_len[in]:深度数据长度
	* - 函数参数6
	  - img_w[in]:深度数据图的宽
	* - 函数参数7
	  - img_h[in]:深度数据图的高  
	* - 函数参数8
	  - p_cam_param[in]:相机参数，如果为空,则使用内部参数	  
	* - 函数返回值
	  - 返回点云数据数
	  
dmcam_frame_get_pcl_xyzd
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. list-table::
	:widths: 60 100
	:header-rows: 1
	
	* - 头文件
	  - #include “dmcam.h”
	* - 函数原型
	  - ``int dmcam_frame_get_pcl_xyzd(dmcam_dev_t *dev, float *pcl, int pcl_len,const float *dist, int dist_len, int img_w, int img_h,bool pseudo_color, const dmcam_camera_para_t *p_cam_param)``
	* - 功能描述
	  - 从获得的深度数据转换成点云数据
	* - 函数参数1
	  - dev[in]:dmcam设备
	* - 函数参数2
	  - pcl[out]:点云数据缓存，pcl[4i+0],pcl[4i+1],pcl[4i+2]分别作为第i个点在空间X轴Y轴Z轴的坐标,pcl[4i+3]是深度或者伪彩色	
	* - 函数参数3
	  - pcl_len[in]：点云数据长度
	* - 函数参数4
	  - dist[in]:深度数据缓存，单位是 m(float)	  
	* - 函数参数5
	  - dist_len[in]:深度数据长度
	* - 函数参数6
	  - img_w[in]:深度数据图的宽
	* - 函数参数7
	  - img_h[in]:深度数据图的高  
	* - 函数参数8
	  - pseudo_color[in]:true则为伪rgb彩色数据，false则为深度数据，单位m
	* - 函数参数9
	  - p_cam_param[in]:相机参数，如果为空,则使用内部参数	  
	* - 函数返回值
	  - 返回点云数据数
	  
dmcam_filter_enable
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. list-table::
	:widths: 60 100
	:header-rows: 1
	
	* - 头文件
	  - #include “dmcam.h”
	* - 函数原型
	  - ``int dmcam_filter_enable(dmcam_dev_t*dev, dmcam_filter_id_e fid, dmcam_filter_args_u *args, uint32_t arg_len)``
	* - 功能描述
	  - 使能对原始数据进行滤波控制
	* - 函数参数1
	  - dev[in]:dmcam设备
	* - 函数参数2
	  - fid:滤波类型，参考模组滤波类型说明
	* - 函数参数3
	  - args[in]：滤波控制参数
	* - 函数参数4
	  - args_len:参数长度  	  
	* - 函数返回值
	  - 返回负值错误