sample_set_param样例
========================

sample_set_param样例主要展示了对模组参数设置的一般方法，
主要参数包模设置模组的积分时间、采集帧率、调制频率等，运行
的样例程序结果如图。

.. image:: imageC/win_C5.jpg

模组参数相关接口包括模组参数的设置和获取，参数设置在调用dmcam_dev_open接口打开设备后可以
进行设置，参数设置通过调用dmcam_param_batch_set,参数获取通过调用dmcam_param_batch_get。

















