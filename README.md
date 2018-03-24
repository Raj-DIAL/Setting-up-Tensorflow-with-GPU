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

  Download the file "cuda_9.0.176_384.81_linux.run" (Note: This file name depends on the version you want to install)[About 1.6GB in size]
  
 6. Open a terminal and run $sudo apt-get install build-essential. This will install gcc compilers. (Note: $ is bash command line)
 
 7. Check $ gcc --version
 
 8. The CUDA Driver requires that the kernel headers and development packages for the running version of the kernel be installed at the time of the driver installation, as well whenever the driver is rebuilt.

    Read more at: http://docs.nvidia.com/cuda/cuda-installation-guide-linux/index.html#ixzz5Af7WupiO 
    Run command: $sudo apt-get install linux-headers-$(uname -r)
 
9. Installing CUDA drivers some times creates issues with X-server (desktop) causing infinite login loop. In this installation, we are interested in only using the NVidia GPU for computing only. Therefore, no need to create an xorg.conf file. If you have one, remove it (assuming you have a fresh OS install). $ sudo rm /etc/X11/xorg.conf

10. To install the Display Driver, the Nouveau drivers must first be disabled. The Nouveau drivers are loaded if the following command prints anything:
$ lsmod | grep nouveau

    To disable nouveau driver:
    Create a file at sudo nano /usr/lib/modprobe.d/blacklist-nouveau.conf with the following contents:
    blacklist nouveau
    
    options nouveau modeset=0
    
    save and exit (ctrl+O+enter, ctrl+x+enter)
    
11. Run $sudo update-initramfs -u

12. Reboot the computer and make sure X-server (desktop) works fine.

13. Press ctrl+alt+f1 to enter to command-line mode, login with username and password.

14. To install the NVidia Cuda toolkit, the X-server (desktop) should be stopped. Run $ sudo service lightdm stop

15. Check if desktop service is stopped: sudo service lightdm status

16. Move to the directory where the cuda toolkit is downloaded (default will be downloads folder). Execute the command

    $ sudo sh cuda_9.0.176_384.81_linux.run --no-opengl-libs
    
    Make sure to run with no opengl support, otherwise the desktop will not work. 
    
    Follow the instructions on the screen:
    - EULA acceptance
    - Yes to install nvidia driver
    - Yes to install nvidia toolkit (default directory)
    - Yes to create symbolic link to /usr/local/cuda
    - Yes to install nvidia samples (default directory)
    - No  to rebuilding any Xserver configurations with Nvidia. If the GPU used for display is an NVIDIA GPU, the X server configuration file, /etc/X11/xorg.conf, may need to be modified. In some cases, nvidia-xconfig can be used to automatically generate a xorg.conf file that works for the system. For non-standard systems, such as those with more than one GPU, it is recommended to manually edit the xorg.conf file. Consult the xorg.conf documentation for more information.

Read more at: http://docs.nvidia.com/cuda/cuda-installation-guide-linux/index.html#ixzz5AfDpShg7 
Follow us: @GPUComputing on Twitter | NVIDIA on Facebook
    
 17. Installation should be complete now. Do $sudo modprobe nvidia (no output should be produced)
 
 18. Set Environment path variables:
 
    $ export PATH=/usr/local/cuda-9.0/bin:$PATH
    
    $ export LD_LIBRARY_PATH=/usr/local/cuda-9.0/lib64:$LD_LIBRARY_PATH
    
    Note: This depends on the cuda version
 19. Verify the driver version:
  
    $ cat /proc/driver/nvidia/version

 20. Check CUDA driver version:
  
    $ nvcc -V
    
 21. Goto samples folders (default in /home/usr/$samplesfolder) and do $make
 
 22. Find and run deviceQuery and ./bandwidthTest under ~/NVIDIA_CUDA-9.0_Samples, both should PASS.
 
 23. Reboot and login in to desktop. GPU driver and cuda are all set up now.



Reference:
1. http://docs.nvidia.com/cuda/cuda-installation-guide-linux/index.html#introduction

2. https://devtalk.nvidia.com/default/topic/878117/cuda-setup-and-installation/-solved-titan-x-for-cuda-7-5-login-loop-error-ubuntu-14-04-/1

