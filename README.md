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
(working a bit more)
../qt-everywhere-src-5.15.7/configure -release -opengl es2 -eglfs  -device linux-rasp-pi5-aarch64     -device-option CROSS_COMPILE=/home/knap-linux/rpi/tools/gcc-linaro-14.0.0-2023.06-x86_64_aarch64-linux-gnu/bin/aarch64-linux-gnu-     -device-option QMAKE_LFLAGS+=--sysroot=/home/knap-linux/rpi/sysroot     -device-option QMAKE_CFLAGS+=--sysroot=/home/knap-linux/rpi/sysroot     -device-option QMAKE_CXXFLAGS+=--sysroot=/home/knap-linux/rpi/sysroot     -opensource -confirm-license

(todo)
../qt-everywhere-src-5.15.7/configure -release -opengl es2 -eglfs  -device linux-rasp-pi5-aarch64     -device-option CROSS_COMPILE=/home/knap-linux/rpi/tools/gcc-linaro-14.0.0-2023.06-x86_64_aarch64-linux-gnu/bin/aarch64-linux-gnu-     -device-option QMAKE_LFLAGS+=--sysroot=/home/knap-linux/rpi/sysroot     -device-option QMAKE_CFLAGS+=--sysroot=/home/knap-linux/rpi/sysroot     -device-option QMAKE_CXXFLAGS+=--sysroot=/home/knap-linux/rpi/sysroot     -opensource -confirm-license -prefix /usr/local/qt5.15 -extprefix ~/rpi/qt5.15 -opensource -confirm-license -skip qtscript -skip qtwayland -skip qtwebengine -nomake tests -make libs -pkg-config -no-use-gold-linker -v -recheck

(mogoce boljsa opcija da najprej sourcas env)
export PKG_CONFIG_SYSROOT_DIR=/home/knap-linux/rpi/sysroot
export PKG_CONFIG_LIBDIR=/home/knap-linux/rpi/sysroot/usr/lib/pkgconfig
export PKG_CONFIG_PATH=/home/knap-linux/rpi/sysroot/usr/lib/pkgconfig
export CFLAGS="--sysroot=/home/knap-linux/rpi/sysroot"
export CXXFLAGS="--sysroot=/home/knap-linux/rpi/sysroot"
export LDFLAGS="--sysroot=/home/knap-linux/rpi/sysroot"

export CXXFLAGS="-I/home/knap-linux/rpi/sysroot/usr/include/c++/11.5.0"
export LDFLAGS="-L/home/knap-linux/rpi/sysroot/usr/lib"

in osnovna komanda:
../qt-everywhere-src-5.15.7/configure -release     -device linux-rasp-pi5-aarch64     -device-option CROSS_COMPILE=/home/knap-linux/rpi/tools/gcc-linaro-14.0.0-2023.06-x86_64_aarch64-linux-gnu/bin/aarch64-linux-gnu-     -opensource -confirm-license     -opengl es2     -eglfs -pkg-config -v

ali cela:
../qt-everywhere-src-5.15.7/configure -release     -device linux-rasp-pi5-aarch64     -device-option CROSS_COMPILE=/home/knap-linux/rpi/tools/gcc-linaro-14.0.0-2023.06-x86_64_aarch64-linux-gnu/bin/aarch64-linux-gnu-     -opensource -confirm-license     -opengl es2     -eglfs -skip qtscript -skip qtwayland -skip qtwebengine -nomake tests -make libs -pkg-config -no-use-gold-linker -v -recheck





