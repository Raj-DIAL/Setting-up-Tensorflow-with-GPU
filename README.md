# Setting-up-Tensorflow 1.6-with-GPU (NVidia Tesla p100)
User guide to setting up Tensorflow with GPU support on Ubuntu 16.04


1. Clean install ubuntu 16.04 server using a bootable USB device.
Link: https://www.ubuntu.com/download/server

2. Server edition only has command line. Install desktop
sudo apt-get install ubuntu-desktop

3. Restart and login to the desktop

4. Check for Tensorflow CUDA library requirements. At the time of writing, Tensorflow pre-built binaries support CUDA versio 9.0
