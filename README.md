# opencv_cmake_file  
cmake -D CMAKE_INSTALL_PREFIX=/usr/local -D CMAKE_BUILD_TYPE=Release -D WITH_TBB=ON -D WITH_V4L=ON -D WITH_LIBV4L=ON -D WITH_QT=ON -D WITH_OPENGL=ON \ -D OPENCV_EXTRA_MODULES_PATH=../opencv_contrib/modules ..  
or  
cmake -D CMAKE_INSTALL_PREFIX=/usr/local -D CMAKE_BUILD_TYPE=Release -D WITH_TBB=ON -D WITH_V4L=ON -D WITH_LIBV4L=ON -D WITH_OPENGL=ON ..  


# original article  
https://ricky.moe/2017/08/27/ubuntu-opencv-3-2-0-install/  
依赖安装  
sudo apt-get update  
sudo apt-get upgrade  
sudo apt-get install build-essential checkinstall cmake pkg-config yasm gfortran git  
sudo apt-get install libjpeg8-dev libjasper-dev libpng12-dev  
如果你在使用ubuntu 14.04 系统  
sudo apt-get install libtiff4-dev  
如果你在使用ubuntu 16.04 系统  
sudo apt-get install libtiff5-dev  
sudo apt-get install libavcodec-dev libavformat-dev libswscale-dev libdc1394-22-dev  
sudo apt-get install libxine2-dev libv4l-dev  
sudo apt-get install libgstreamer0.10-dev libgstreamer-plugins-base0.10-dev  
sudo apt-get install libqt4-dev libgtk2.0-dev libtbb-dev  
sudo apt-get install libatlas-base-dev  
sudo apt-get install libfaac-dev libmp3lame-dev libtheora-dev  
sudo apt-get install libvorbis-dev libxvidcore-dev  
sudo apt-get install libopencore-amrnb-dev libopencore-amrwb-dev  
sudo apt-get install x264 v4l-utils  

还有一些可选的安装包：  
sudo apt-get install libprotobuf-dev protobuf-compiler  
sudo apt-get install libgoogle-glog-dev libgflags-dev  
sudo apt-get install libgphoto2-dev libeigen3-dev libhdf5-dev doxygen  
检出OpenCV 3.2.0相关代码  
检出OpenCV 3.2.0  
git clone https://github.com/opencv/opencv.git  
cd opencv  
如果你的机器上有安装OpenBlas，OpenCV 3.2.0会无法编译。我们检出一个带有bug patch的版本  
git checkout 2b44c0b6493726c465152e1db82cd8e65944d0db   
cd ..  
检出OpenCV_contrib 3.2.0  
OpenCV_contrib包含了诸多带有专利保护的算法模块，推荐一起编译，免得要用的时候还要来处理。  
git clone https://github.com/opencv/opencv_contrib.git  
cd opencv_contrib  
git checkout abf44fcccfe2f281b7442dac243e37b7f436d961  
cd ..  
编译安装  
创建一个编译目录  
cd opencv  
mkdir build  
cd build  
cmake配置工程  
cmake -D CMAKE_BUILD_TYPE=RELEASE \
      -D CMAKE_INSTALL_PREFIX=/usr/local \
      -D INSTALL_C_EXAMPLES=OFF \
      -D INSTALL_PYTHON_EXAMPLES=OFF \
      -D WITH_TBB=ON \
      -D WITH_V4L=ON \
      -D WITH_QT=ON \
      -D WITH_OPENGL=ON \
      -D OPENCV_EXTRA_MODULES_PATH=../../opencv_contrib/modules \
      -D BUILD_EXAMPLES=OFF ..  
编译与安装  
先检查本机的CPU有几个内核  
nproc  
如果显示的是数字4，证明电脑是4核，全部利用起来编译  
make -j4  
sudo make install  
sudo sh -c 'echo "/usr/local/lib" >> /etc/ld.so.conf.d/opencv.conf'  
sudo ldconfig  
验证安装版本  
pkg-config --modversion opencv  
如果显示的是3.2.0,证明OpenCV 3.2.0 版本编译OK。  
