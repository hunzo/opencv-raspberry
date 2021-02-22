# Install OpenCV in Rasbian
## Config swap filesize to 2048 for compile
- editfile
```shell
sudo vi /etc/dphys-swapfile
```
```
CONF_SWAPSIZE=2048
```
- restart services
```
sudo /etc/init.d/dphys-swapfile stop
sudo /etc/init.d/dphys-swapfile start
```
- update and upgrade os 
```shell
sudo apt update -y && sudo  apt upgrade -y
```
- install tools for compile and build
```shell
sudo apt install cmake build-essential pkg-config git
```
- install library for OpenCV
```shell
sudo apt install libjpeg-dev libtiff-dev libjasper-dev libpng-dev libwebp-dev libopenexr-dev
sudo apt install libavcodec-dev libavformat-dev libswscale-dev libv4l-dev libxvidcore-dev libx264-dev libdc1394-22-dev libgstreamer-plugins-base1.0-dev libgstreamer1.0-dev
```
```shell
sudo apt install libgtk-3-dev libqtgui4 libqtwebkit4 libqt4-test python3-pyqt5
```
```shell
sudo apt install libatlas-base-dev liblapacke-dev gfortran
```
```shell
sudo apt install libhdf5-dev libhdf5-103
```
```shell
sudo apt install python3-dev python3-pip python3-numpy
```
## Download OpenCV Package
```bash
#!/bin/bash
cd ~
wget -O opencv.zip https://github.com/opencv/opencv/archive/4.1.1.zip
wget -O opencv_contrib.zip https://github.com/opencv/opencv_contrib/archive/4.1.1.zip
unzip opencv.zip
unzip opencv_contrib.zip
mv opencv-4.1.1 opencv
mv opencv_contrib-4.1.1 opencv_contrib
```
## Start Compile and Build Package
```shell
#!/bin/bash
cd ~/opencv
mkdir build

cd build

cmake -D CMAKE_BUILD_TYPE=RELEASE \
    -D CMAKE_INSTALL_PREFIX=/usr/local \
    -D OPENCV_EXTRA_MODULES_PATH=~/opencv_contrib/modules \
    -D ENABLE_NEON=ON \
    -D ENABLE_VFPV3=ON \
    -D BUILD_TESTS=OFF \
    -D INSTALL_PYTHON_EXAMPLES=OFF \
    -D OPENCV_ENABLE_NONFREE=ON \
    -D CMAKE_SHARED_LINKER_FLAGS=-latomic \
    -D BUILD_EXAMPLES=OFF .. \

# make -j4
make -j$(nproc)
sudo make install
sudo ldconfig
```
## Config swap file to default
- editfile
```shell
sudo vi /etc/dphys-swapfile
```
```
CONF_SWAPSIZE=100
```
- reboot
## Test OpenCV
```shell
python3
```
```python
import cv2
```
```python
cv2.__version__
```





