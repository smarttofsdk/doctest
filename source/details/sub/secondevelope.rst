二次开发流程
===============

基本采集数据
---------------

一般的数据采集采集流程包括设备初始化，日志配置，创建设备列表，打开
设备，采集原始数据，获取深度和灰度数据，获取点云数据关闭设备等操作。

接口调用采集说明
+++++++++++++++++

SmartToF SDK在采集时的API接口调用流程如下图所示：

.. image:: ../../../images/采集接口流程.jpg

参数设置和读取示例
---------------------

模组的参数设置和读取分别通过调用dmcam_param_batch_set和dmcam_param_batch_get实现，可以设置积分时间、帧率等参数，也可读取模组信息、温度等参数，具体参数说明参考下面的的主要参数说明。

主要参数说明
+++++++++++++++++

模组的参数类型在dmcam_dev_param_e的枚举类型中，如下::

	typedef enum {
		PARAM_DEV_MODE = 0,
		PARAM_MOD_FREQ,

		PARAM_INFO_VENDOR,
		PARAM_INFO_PRODUCT,
		PARAM_INFO_CAPABILITY,
		PARAM_INFO_SERIAL,
		PARAM_INFO_VERSION,   //HW&SW info
		PARAM_INFO_SENSOR,    //part version, chip id, wafer id

		PARAM_INFO_CALIB,     //get calibration info
		PARAM_ROI,            //ROI set/get
		PARAM_FRAME_FORMAT,   //frame information,eg.dcs1for gray,4 dcs for distance
		PARAM_ILLUM_POWER,    //illumination power set/get
		PARAM_FRAME_RATE,     //frame rate set/get
		PARAM_INTG_TIME,      //integration time set/get
		PARAM_PHASE_CORR,     //phase offset correction
							  //PARAM_SWITCH_MODE, /*>swith mode use[gray,3d]*/
		PARAM_TEMP,           //<Get camera temperature--------------
		PARAM_HDR_INTG_TIME,  //<Setting HDR integration time param
		PARAM_SYNC_DELAY,     //<delay ms for sync use
		PARAM_ENUM_COUNT,
	}dmcam_dev_param_e;
	
参数代码示例
++++++++++++++++++

* 进行参数设置::

	dmcam_param_item_t wparam;			
	uint16_t intg_time = 700;			//表示设置积分的大小 范围为0-1500 
	memset(&wparam,0,sizeof(wparam));
	wparam.param_id = PARAM_INTG_TIME;	//表示设置的参数为积分时间
	wparam.param_val_len = sizeof(intg_time);
	assert(dmcam_param_batch_set(dev,&wparam,1));	//调用API进行单个参数设置
	
* 进行参数读取::

	dmcam_param_item_t rparam;
	memset(&rparam,0,sizeof(rparam));
	rparam.param_id = PARAM_INTG_TIME;	//表示要读取的参数项为积分时间
	assert(dmcam_param_batch_get(dev,&rparam,1));	//调用API获取单个参数
	
滤波功能使用
-------------------

SDK中支持对模组进行像素校准使能、最小幅值滤波、自动曝光等fliter功能的使用，filter类型参考dmcam_filter_id_e的说明。

主要滤波功能说明
+++++++++++++++++++

模组的滤波类型在如下的枚举类型中::

	typedef enum {
		DMCAM_FILTER_ID_LEN_CALIB,    /**>lens calibration*/
		DMCAM_FILTER_ID_PIXEL_CALIB,  /**>pixel calibration*/
		DMCAM_FILTER_ID_MEDIAN,       /**>Median filter for distance data*/
		DMCAM_FILTER_ID_RESERVED,        /**>Gauss filter for distance data*/
		DMCAM_FILTER_ID_AMP,          /**>Amplitude filter control*/
		DMCAM_FILTER_ID_AUTO_INTG,    /**>auto integration filter enable : use sat_ratio to adjust */
		DMCAM_FILTER_ID_SYNC_DELAY,   /**> sync delay */
		DMCAM_FILTER_ID_TEMP_MONITOR, /**>temperature monitor */
		DMCAM_FILTER_ID_HDR,          /**>HDR mode */
		DMCAM_FILTER_ID_OFFSET,       /**> set offset for calc distance */
		DMCAM_FILTER_ID_SPORT_MODE,   /**> set sport mode */
		//-------------------
		DMCAM_FILTER_CNT,
	}dmcam_filter_id_e;
	
滤波代码示例
++++++++++++++++++

* 像素校准，开启后用于深度数据的矫正::

	dmcam_filter_args_u witem;
	dmcam_filter_id_e filter_id = DMCAM_FILTER_ID_PIXEL_CALIB; //像素校准
	dmcam_filter_enable(dev,filter_id,&witem,sizeof(dmcam_filter_args_u));//开启像素校准
	dmcam_filter_disable(dev,DMCAM_FILTER_ID_PIXEL_CALIB); //关闭像素校准
	
* 深度滤波，开启后用于对深度数据滤波::

	dmcam_filter_args_u witem;
	dmcam_filter_id_e filter_id = DMCAM_FILTER_ID_MEDIAN;	//深度滤波
	witem.median_ksize = 3;	//深度滤波通常设置值
	dmcam_filter_enable(dev,filter_id,&witem,sizeof(dmcam_filter_args_u));//开启深度滤波
	dmcam_filter_disable(dev,DMCAM_FILTER_ID_MEDIAN);	//关闭深度滤波
	
* 幅值滤波，开启后过滤质量差的点::

	dmcam_filter_args_u witem;
	dmcam_filter_id_e filter_id = DMCAM_FILTER_ID_AMP;	//最小幅值滤波
	witem.min_amp = 30;	//设置的最小幅值滤波的阈值
	dmcam_filter_enable(dev,filter_id,&witem,sizeof(dmcam_filter_args_u));//开启最小幅值滤波
	dmcam_filter_disable(dev,DMCAM_FILTER_ID_AMP);	//关闭最小幅值滤波
	
* 自动积分时间，开启后根据被测物体的距离自动调整曝光时间大小::

	dmcam_filter_args_u witem;
	dmcam_filter_id_e filter_id = DMCAM_FILTER_ID_AUTO_INTG;	//自动曝光
	witem.sat_ratio = 5;//自动曝光时设置的值
	dmcam_filter_enable(dev,filter_id,&witem,sizeof(dmcam_filter_args_u));//开启自动曝光
	dmcam_filter_disable(dev,DMCAM_FILTER_ID_AUTO_INTG);	//关闭自动曝光
	
* 多模组串扰消除，开启消除或者减小多模组同时开启时的串扰::

	dmcam_filter_args_u witem;
	dmcam_filter_id_e filter_id = DMCAM_FILTER_ID_SYNC_DELAY;	 //串扰延时
	witem.sync_delay = 0;	//延时时间设为0时为随机时间
	dmcam_filter_enable(dev,filter_id,&witem,sizeof(dmcam_filter_args_u));//开启串扰延时
	dmcam_filter_disable(dev,DMCAM_FILTER_ID_SYNC_DELAY);	//关闭串扰延时

* 运动模式0，帧格式要设置为2::

	dmcam_filter_args_u witem;
	dmcam_filter_id_e filter_id = DMCAM_FILTER_ID_SPORT_MODE;	 //运动模式0
	dmcam_param_item_t wparam;	
	uint32_t set_format = 2;	//表示要设置的帧格式为2		
	memset(&wparam,0,sizeof(wparam));
	wparam.param_id = PARAM_FRAME_FORMAT;	//表示设置的参数为帧格式
	wparam.frame_format.format = set_format;	//设置的帧格式为2
	wparam.param_val_len = sizeof(set_format);
	assert(dmcam_param_batch_set(dev,&wparam,1));	//调用API进行帧格式参数设置
	witem.sport_mode = 0;	//设置运动模式为0
	dmcam_filter_enable(dev,filter_id,&witem,sizeof(dmcam_filter_args_u));//开启运动模式0
	dmcam_filter_disable(dev,DMCAM_FILTER_ID_SPORT_MODE);//关闭运动模式0
	
* 运动模式1，帧格式要设置为4::

	dmcam_filter_args_u witem;
	dmcam_filter_id_e filter_id = DMCAM_FILTER_ID_SPORT_MODE;	 //运动模式1
	dmcam_param_item_t wparam;	
	uint32_t set_format = 4;	//表示要设置的帧格式为4		
	memset(&wparam,0,sizeof(wparam));
	wparam.param_id = PARAM_FRAME_FORMAT;	//表示设置的参数为帧格式
	wparam.frame_format.format = set_format;	//设置的帧格式为4
	wparam.param_val_len = sizeof(set_format);
	assert(dmcam_param_batch_set(dev,&wparam,1));	//调用API进行帧格式参数设置
	witem.sport_mode = 1;	//设置运动模式为1
	dmcam_filter_enable(dev,filter_id,&witem,sizeof(dmcam_filter_args_u));//开启运动模式1
	//关闭运动模式1时，帧格式要先恢复到2
	set_format = 2;		//帧格式要恢复设置为2
	wparam.frame_format.format = set_format;	//设置的帧格式的值为2
	wparam.param_id = PARAM_FRAME_FORMAT;	//表示设置的参数为帧格式
	wparam.param_val_len = sizeof(set_format);
	assert(dmcam_param_batch_set(dev,&wparam,1));	//调用API进行帧格式参数设置2
	dmcam_filter_disable(dev,DMCAM_FILTER_ID_SPORT_MODE);//关闭运动模式1







	
	
