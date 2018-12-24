Windows平台Python样例
=======================

Windows下运行Python样例需要安装对应Python版本的dmcam包、
numpy、matplotlib、pygame、Pyqtgraph等包。

运行python样例相关包的安装
------------------------------

#. dmcam库的安装

	dmcam包从1.60后开始，已经上传python各版本对应的whl包到Pypi网站，
	如要更新安装最新的dmcam包，安装命令如下::
	   
	   pip install -U dmcam

	如果要安装指定版本的dmcam,则需加上版本号，如安装版本号为1.57.7::

	   pip install dmcam==1.57.7

	安装dmcam包的结果如下图：

	.. image:: imageP/win_P1.jpg 

#. 样例其他库的安装
   
	安装numpy、matplotlib、pygame、PyQt5、pyqtgraph,可以通过以下命令安装::

	 pip install -r requirement.txt

	.. note::
		在python2.7或者python3.4环境下安装PyQt5可能回导致失败，可以换成安装PyQt4   

运行Python基本采集样例
------------------------

运行在windows/samples/python目录中的sample_basic.py采集程序::

   python sampe_basic.py

基本采集程序运行的结果如下图

.. image:: imageP/win_P2.jpg 

运行Python参数设置样例
-------------------------

运行在windows/samples/python目录中的sample_param.py程序::

   python sample_param.py

参数设置程序运行结果如下图

.. image:: imageP/win_P3.jpg 

运行Python UI样例
------------------------

运行在windows/samples/python目录中的sample_gui_pygame.py程序::

   python sample_gui_pygame.py

程序运行结果如下图

.. image:: imageP/win_P4.jpg 