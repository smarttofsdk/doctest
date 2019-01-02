sample_capture_frames样例
====================================

SDK中提供了基本采集、参数设置、滤波使能、保存录像文件等四个基本样例，
基本覆盖了在模组二次开发中常用的一些API使用，可以作为用户进行开发时
的基本参考。

运行sample_capture_frames采集样例程序如图.

.. image:: imageC/win_C4.jpg

样例中为先对模组进行采集前基本设置，然后开启采集，每次获取10帧,然后进行深度和
灰度等计算，设置的采集总帧数为100帧，采集完成后停止采集。采集样例中包括了dmcam_cap_config_set用
于采集前的配置，dmcam_cap_start开始采集，dmcam_cap_get_frames获取
采集数据,dmcam_frame_get_distance等主要采集接口。




















