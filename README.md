# nano
Learning Jetson Nano, notes, tutorials, etc.


####### This will turn the FAN on...
sudo sh -c 'echo 255 > /sys/devices/pwm-fan/target_pwm'
####### This will turn the FAN off...
sudo sh -c 'echo 0 > /sys/devices/pwm-fan/target_pwm'


####### This is some mambo Jambo for setting performance levels
sudo vim /etc/rc.local

  echo 1 > /sys/devices/system/cpu/cpu0/online
  echo 1 > /sys/devices/system/cpu/cpu1/online
  echo 1 > /sys/devices/system/cpu/cpu2/online
  echo 1 > /sys/devices/system/cpu/cpu3/online
  echo performance > /sys/devices/system/cpu/cpu0/cpufreq/scaling_governor
  nvpmodel -m 0
  ( sleep 60 && jetson_clocks )&

sudo chmod a+rx /etc/rc.local
update-rc.d -f ondemand remove

####### Here is some useful auto-fan control stuff.  Install this...
unzip jetson-fan-ctl-master.zip
cd jetson-fan-ctl-master
./install.sh

####### Get all the documentation on the drive
sudo unminimize

####### This is from the Jetson Zoo -- for setting up TensorFlow
# install prerequisites
sudo apt-get install libhdf5-serial-dev hdf5-tools libhdf5-dev zlib1g-dev zip libjpeg8-dev
# install and upgrade pip3
sudo apt-get install python3-pip
sudo pip3 install -U pip testresources setuptools
# install the following python packages
sudo pip3 install -U numpy==1.16.1 future==0.17.1 mock==3.0.5 h5py==2.9.0 keras_preprocessing==1.0.5 keras_applications==1.0.8 gast==0.2.2 enum34 futures protobuf
# to install TensorFlow 1.15 for JetPack 4.4:
sudo pip3 install --pre --extra-index-url https://developer.download.nvidia.com/compute/redist/jp/v44 ‘tensorflow<2’
# or install the latest version of TensorFlow (2.1) for JetPack 4.4:
sudo pip3 install --pre --extra-index-url https://developer.download.nvidia.com/compute/redist/jp/v44 tensorflow
