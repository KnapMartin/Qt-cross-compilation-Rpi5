# Qt-cross-compilation-Rpi5
Guide for setting up cross-compilation for Qt projects on Raspberry pi 5

# get the source
sudo wget https://download.qt.io/archive/qt/5.15/5.15.7/single/qt-everywhere-opensource-src-5.15.7.tar.xz

# extract
sudo tar xfv qt-everywhere-src-5.15.7.tar.xz 

# change mkspec file
omitted

# copy aarch64 toolchain to /rpi/tools/

# synch
sudo rsync -avz --rsync-path="rsync" --delete root@192.168.2.2:/lib sysroot
sudo rsync -avz --rsync-path="rsync" --delete root@192.168.2.2:/usr/include sysroot/usr
sudo rsync -avz --rsync-path="rsync" --delete root@192.168.2.2:/usr/lib sysroot/usr
sudo rsync -avz --rsync-path="rsync" --delete root@192.168.2.2:/opt/vc sysroot/opt

# add rasp-pi5 configuration to mkspec

# reconfigure (wip)

../qt-everywhere-src-5.15.7/configure -release -opengl es2 -eglfs -device linux-rasp-pi5-aarch64 -device-option CROSS_COMPILE=~/rpi/tools/gcc-linaro-14.0.0-2023.06-x86_64_aarch64-linux-gnu/bin/aarch64-linux-gnu- -sysroot ~/rpi-sysroot -prefix /usr/local/qt5.15 -extprefix ~/rpi/qt5.15 -opensource -confirm-license -skip qtscript -skip qtwayland -skip qtwebengine -nomake tests -make libs -pkg-config -no-use-gold-linker -v -recheck



