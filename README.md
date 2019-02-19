# Ubuntu-18.04-System-Setup

Instructions given for Configurations:
Nvidia driver : 390.77
Cuda : 9.0
cuDNN : 7.2.1
Python : 3.6.7
PyTorch 1.0.1
Pip3, Virtual env(venv),Numpy,Scipy,Matplotlib,OpenCV,PIllow

#  NVIDIA DRIVER 390.77

Installing Drivers on ubuntu 18.04

1. First, detect the model of your nvidia graphic card and the recommended driver. To do so execute:
ubuntu-drivers devices

2. If you agree with the recommendation feel free to use ubuntu-drivers command again to install all recommended drivers:
sudo ubuntu-drivers autoinstall

3. Once the installation is concluded, reboot your system and you are done.





# Installing CUDA 9.0 and cuDNN 7.2.1 

-->to verify your gpu is cuda enable check
lspci | grep -i nvidia

-->install other import packages
sudo apt-get install g++ freeglut3-dev build-essential libx11-dev libxmu-dev libxi-dev libglu1-mesa libglu1-mesa-dev

-->CUDA 9 requires gcc 6
sudo apt install gcc-6
sudo apt install g++-6

-->downoad one of the "runfile (local)" installation packages from cuda toolkit archive
wget https://developer.nvidia.com/compute/cuda/9.0/Prod/local_installers/cuda_9.0.176_384.81_linux-run

-->make the download file executable
chmod +x cuda_9.0.176_384.81_linux.run
sudo ./cuda_9.0.176_384.81_linux.run --override

--> answer following questions while installation begin
--> You are attempting to install on an unsupported configuration. Do you wish to continue? y
--> Install NVIDIA Accelerated Graphics Driver for Linux-x86_64 384.81? n
--> Install the CUDA 9.0 Toolkit? y

--> set up symlinks for gcc/g++
sudo ln -s /usr/bin/gcc-6 /usr/local/cuda/bin/gcc
sudo ln -s /usr/bin/g++-6 /usr/local/cuda/bin/g++

--> setup your paths
echo 'export PATH=/usr/local/cuda-9.0/bin:$PATH' >> ~/.bashrc
echo 'export LD_LIBRARY_PATH=/usr/local/cuda-9.0/lib64:$LD_LIBRARY_PATH' >> ~/.bashrc
source ~/.bashrc

--> To download cudnn7.2.1 for cuda9.0

https://developer.nvidia.com/compute/machine-learning/cudnn/secure/v7.2.1/prod/9.0_20180806/cudnn-9.0-linux-x64-v7.2.1.38

tar -xzvf cudnn-9.0-linux-x64-v7.2.1.38.tgz
--> copy the following files into the cuda toolkit directory.
sudo cp -P cuda/include/cudnn.h /usr/local/cuda-9.0/include
sudo cp -P cuda/lib64/libcudnn* /usr/local/cuda-9.0/lib64/
sudo chmod a+r /usr/local/cuda-9.0/lib64/libcudnn*


--> Finally, to verify the installation, check
nvidia-smi
nvcc -V


#  Python 3.6.7 
sudo apt update
sudo apt -y upgrade
Check which version of Python 3 is installed by typing:
python3 -V --> 3.6.7
--> To manage software packages for Python, install pip, a tool that will install and manage libraries or modules to use in your projects.
sudo apt install -y python3-pip

--> There are a few more packages and development tools to install to ensure that we have a robust set-up for our programming environment:
sudo apt install build-essential libssl-dev libffi-dev python3-dev


# Packages - VirtualEnv 

sudo apt install -y python3-venv

--> To create virtualenv:
python3.6 -m venv ~/.virtualenv/test_env

--> To activate this:
source ~/.virtualenv/test_env/bin/activate

--> To deactivate this:
deactivate

#  Packages - PyTorch (for cuda 9.0 & python3.6 & pip) 
pip3 install torch torchvision

# Packages - Numpy,Scipy,Matplotlib,OpenCV,PIllow, (for python3.6 Ubuntu 18) 
sudo apt update
sudo apt upgrade
sudo apt install python3-numpy python3-scipy python3-matplotlib
sudo apt install python3-opencv
pip3 install Pillow



Reference links :
https://linuxconfig.org/how-to-install-the-nvidia-drivers-on-ubuntu-18-04-bionic-beaver-linux

https://docs.nvidia.com/deploy/cuda-compatibility/index.html

https://devtalk.nvidia.com/default/topic/1031351/linux/cannot-purge-and-install-nvidia-driver/

https://devtalk.nvidia.com/default/topic/1042312/linux/cudnn7-2-for-cuda9-0/

https://gist.github.com/Mahedi-61/2a2f1579d4271717d421065168ce6a73


