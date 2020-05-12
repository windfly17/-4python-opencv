

# 树莓派4b安装opencv3.0与opencv4.1

1. ## 安装官方系统

	下载地址：http://downloads.raspberrypi.org/raspbian_latest

	其他工具略

2. ## 系统设置：略(记得在设置中打开摄像头)

4. ## 更换镜像源

	1. ### 先备份源文件
	```shell
	sudo cp /etc/apt/sources.list /etc/apt/sources.list.bak
	sudo cp /etc/apt/sources.list.d/raspi.list /etc/apt/sources.list.d/raspi.list.bak'
	```
	2. ### 编辑系统源文件
	```shell
	sudo nano /etc/apt/sources.list
	```
	3. ### 将初始的源使用#注释掉，添加如下两行清华的镜像源。
	   
	```shell
	deb http://mirrors.tuna.tsinghua.edu.cn/raspbian/raspbian/ buster main contrib non-free rpi
	deb-src http://mirrors.tuna.tsinghua.edu.cn/raspbian/raspbian/ buster main contrib non-free rpi
	```
	
	4. ### 保存执行如下命令 sudo apt-get update，完成源的更新软件包索引。
	   
	```shell
	sudo apt-get update&&upgrade
	```
	
	5. ### 还需要更改系统源
	   
	```shell
	sudo nano /etc/apt/sources.list.d/raspi.list
	```
	用#注释掉原文件内容，用以下内容取代：用#注释掉原文件内容，用以下内容取代：
	```shell
	deb http://mirrors.tuna.tsinghua.edu.cn/raspberrypi/ buster main ui
	deb-src http://mirrors.tuna.tsinghua.edu.cn/raspberrypi/ buster main ui
	```

5. ## 安装必要的库

	1. ### 安装numpy
	
		```shell
		sudo pip3 install numpy
		```
		
	2. ### 安装opencv依赖库
	
		```shell
		sudo apt-get install libhdf5-dev -y
		sudo apt-get install libatlas-base-dev -y
		sudo apt-get install libjasper-dev -y
		sudo apt-get install libqt4-test -y
		sudo apt-get install libqtgui4 -y
		```
		
	4. ### 查询opencv库与opencv-contrib库可用版本
		作者没有更换pip源，查询到了多个版本，国内源不知到有没有。
		
		```shell
		sudo pip3 install python-opencv==
		sudo pip3 install python-contrib-opencv==
		```
		
		根据需求，自行安装所需版本
		
		```shell
		sudo pip3 install python-opencv==3.4.6.27
		sudo pip3 install python-contrib-opencv==3.4.6.27
		```
		
		官方源可能过慢，可以使用手机热点或科学上网方法下载后拷贝到树莓派进行安装，仅提供我安装的3.4.6.27的下载链。
	
		```shell
		https://www.piwheels.org/simple/opencv-contrib-python/opencv_contrib_python-3.4.6.27-cp37-cp37m-linux_armv7l.whl
		https://www.piwheels.org/simple/opencv-python/opencv_python-3.4.6.27-cp37-cp37m-linux_armv7l.whl
		```
		安装本地库的方法：
		
		```shell
		sudo pip3 insatll 文件位置
		```
		
5. ## 测试安装情况
	正常情况下应该已经成功安装，但不排除可能缺少库文件而导致安装失败。
	
	```shell
	sudo pip3 list | grep python-opencv
	```
	
	测试代码：
	
	```python
	import numpy as np
	import cv2
	
	cam = cv2.VideoCapture(0)
	while True:
		ret, img = cam.read()
		cv2.imshow('cam', img)
		ch = cv2.waitKey(5)
		if ch == 27:
			break
	cv2.destroyAllWindows()
	```
