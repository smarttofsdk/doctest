运行
=======================

运行Python样例需要安装对应Python版本的dmcam包、
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

python相关包安装好后，就可以运行指定的样例。