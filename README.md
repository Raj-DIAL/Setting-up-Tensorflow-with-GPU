# Setting-up-Tensorflow 1.6-with-GPU (NVidia Tesla p100)
User guide to setting up Tensorflow with GPU support on Ubuntu 16.04


1. Clean install ubuntu 16.04 server using a bootable USB device.
Link: https://www.ubuntu.com/download/server

2. Server edition only has command line. Install desktop
sudo apt-get install ubuntu-desktop

3. Restart and login to the desktop

4. Check for Tensorflow CUDA library requirements. At the time of writing, Tensorflow pre-built binaries support CUDA versio 9.0

5. Download the relevant run file for the cuda toolkit: https://developer.nvidia.com/cuda-90-download-archive?target_os=Linux&target_arch=x86_64&target_distro=Ubuntu&target_version=1604&target_type=runfilelocal

- Choose OS (linux)
- Choose taget archiectecture (X86-64 bit)
- Choose linux distribution (Ubuntu)
- Choose version (16.04)
- Choose run type (run file local)

  Download the file "cuda_9.0.176_384.81_linux.run" (Note: This file name depends on the version you want to install)
  
 6. Open a terminal and run $sudo apt-get install build-essential. This will install gcc compilers. (Note: $ is bash command line)
 
 7. Check $ gcc --version
 
 8. The CUDA Driver requires that the kernel headers and development packages for the running version of the kernel be installed at the time of the driver installation, as well whenever the driver is rebuilt.

  Read more at: http://docs.nvidia.com/cuda/cuda-installation-guide-linux/index.html#ixzz5Af7WupiO 
  
  Run command: $sudo apt-get install linux-headers-$(uname -r)
 
