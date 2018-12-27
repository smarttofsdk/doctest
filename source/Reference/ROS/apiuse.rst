ROS API 使用
=======================

API使用
+++++++++++++++++++

#. 开启一个滤波功能，如DMCAM_FILTER_ID_AUTO_INTG::

	rosservice call /smarttof/change_filter "filter_id:
	'DMCAM_FILTER_ID_AUTO_INTG'
	filter_value: 0"
	
#. 关闭一个滤波功能，如DMCAM_FILTER_ID_AUTO_INTG::

	rosservice call /smarttof/disable_filter "filter_id:
	'DMCAM_FILTER_ID_AUTO_INTG'"




