# HHU-RobLab
<font size=11 >实验室学习资料共享交流平台</font>

# 好用的开发工具
通过 https://education.github.com/pack/offers 我们可以利用我们的教育邮箱（@hhu.edu.cn）申请到很多很有用的开发工具，如Jetbrains全家桶（其中就包括著名的IntelliJ IDEA,PyCharm等），Github Pro订阅，Termius Premium订阅等等。这些都是对学生免费使用的！
# C/C++
# Python学习
  Python编程无师自通 电子书及代码
  
  链接：https://pan.baidu.com/s/1Z0vQT4BPuhZ2_yA6BzcYGw 
  提取码：1111
  祝师兄强烈推荐：
  https://docs.python.org/3/howto/logging.html
  
  https://docs.python.org/3/library/unittest.html
  
  https://www.python.org/dev/peps/pep-0008/
# JAVA学习
# Web开发
# php学习
# Linux学习
# 机器学习
# 深度学习
# 强化学习
# F1TENTH: AUTONOMOUS RACING
https://www.youtube.com/playlist?list=PL7rtKJAz_mPdQ6fdpDkis9WrARUINneLp
# 各种踩过的坑/实用技巧
## 保证外网的顺畅访问
在linux环境中，安装clash等系列代理工具显然没有在Windows中那样方便。
当然，动手能力强的话可以直接装clash的命令行版本，但过程比较复杂，也有一些隐藏的坑。
这里介绍一种借助局域网中已经安装并配置好clash的Windows进行代理的方法：
首先，打开clash里的“允许局域网LAN”选项（我使用的是Clash .Net，显示上可能会略有不同）
然后查看本机IP（Clash里应该能看得到）如：192.168.1.108
Clash for Windows 的默认混合端口是7890，其他版本的Clash也许会有不同，可自行寻找。这里用Clash for Windows的7890端口做示范：
在需要访问外网的linux机器的终端中输入 
```
export https_proxy=192.168.1.108:7890
export http_proxy=192.168.1.108:7890
```
即可使用当前终端访问外网，进行相关操作。

## pip的安装
有的时候下载的镜像中python并没有自带pip，需要手动安装
```
curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py
sudo python2 get-pip.py  #为python2安装pip
sudo python3 get-pip.py  #为python3安装pip
```
## ROS的安装
1.手动安装ROS时，需要确保安装过程的互联网连接正常且可以[访问外网](./README.md#保证外网的顺畅访问)
2.在编译catkin Workspace的时候，可能需要卸载当前的libboost
```
sudo apt remove libboost1.67-dev
sudo apt autoremove
```
然后安装libboost 1.58版本
```
sudo apt install -y libboost1.58-dev libboost1.58-all-dev
```
如果无法通过apt安装libboost1.58，则需要手动编译安装
```
wget -O boost_1_58_0.tar.bz2 http://sourceforge.net/projects/boost/files/boost/1.58.0/boost_1_58_0.tar.bz2/download
tar --bzip2 -xvf boost_1_58_0.tar.bz2
cd boost_1_58_0
./bootstrap.sh --with-libraries=all --with-toolset=gcc
./b2 toolset=gcc
sudo ./b2 install --prefix=/usr
sudo ldconfig
```
如果使用arm64版本的linux，则需要把第五行
```
./b2 toolset=gcc
```
改成
```
./b2 -d2 -q toolset=gcc architecture=arm abi=aapcs address-model=64
```
