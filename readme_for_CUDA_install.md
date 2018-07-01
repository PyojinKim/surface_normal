## Tested Hardware and Software Setting by pjinkim

*   Environments: Ubuntu 16.04 LTS (64-bit) + GeForce GTX 970M in MSI Laptop (GS60 Ghost pro)


## 1. Install NVIDIA Graphics Driver
Please go to https://hiseon.me/2018/02/17/install_nvidia_driver/ and the following the instructions.

Check
```
$ cat /proc/driver/nvidia/version
cat: /proc/driver/nvidia/version: No such file or directory

$ lspci -k
02:00.0 VGA compatible controller: NVIDIA Corporation GM107 [GeForce GTX 750 Ti] (rev a2)
        Subsystem: NVIDIA Corporation GM107 [GeForce GTX 750 Ti]
        Kernel driver in use: nouveau
        Kernel modules: nvidiafb, nouveau
```

Run
```
$ sudo apt-get update && sudo apt-get install -y dialog language-pack-en
$ export LANGUAGE=en_US
$ export LANG=en_US.UTF-8
$ export LC_ALL=en_US.UTF-8
$ update-locale

$ sudo gedit /etc/default/locale
LANG="en_US.UTF-8"
LANGUAGE="en_US"
LC_ALL="en_US.UTF-8"

$ sudo apt-key adv --fetch-keys http://developer.download.nvidia.com/compute/cuda/repos/ubuntu1604/x86_64/7fa2af80.pub
$ sudo sh -c 'echo "deb http://developer.download.nvidia.com/compute/cuda/repos/ubuntu1604/x86_64 /" >> /etc/apt/sources.list.d/cuda.list'
$ sudo sh -c 'echo "deb http://developer.download.nvidia.com/compute/machine-learning/repos/ubuntu1604/x86_64 /" >> /etc/apt/sources.list.d/cuda.list'
$ sudo apt-get update

$ apt-cache search nvidia
$ sudo apt-get install nvidia-390
$ sudo apt-get install dkms nvidia-modprobe
$ sudo reboot
```

Confirm
```
$ sudo lspci -k
01:00.0 3D controller: NVIDIA Corporation GM204M [GeForce GTX 970M] (rev a1)
	Subsystem: Micro-Star International Co., Ltd. [MSI] GM204M [GeForce GTX 970M]
	Kernel driver in use: nvidia
	Kernel modules: nvidiafb, nouveau, nvidia_396, nvidia_396_drm

$ sudo cat /proc/driver/nvidia/version
NVRM version: NVIDIA UNIX x86_64 Kernel Module  396.26  Mon Apr 30 18:01:39 PDT 2018
GCC version:  gcc version 5.4.0 20160609 (Ubuntu 5.4.0-6ubuntu1~16.04.10)

$ nvidia-smi
Sun Jul  1 17:07:50 2018       
+-----------------------------------------------------------------------------+
| NVIDIA-SMI 396.26                 Driver Version: 396.26                    |
|-------------------------------+----------------------+----------------------+
| GPU  Name        Persistence-M| Bus-Id        Disp.A | Volatile Uncorr. ECC |
| Fan  Temp  Perf  Pwr:Usage/Cap|         Memory-Usage | GPU-Util  Compute M. |
|===============================+======================+======================|
|   0  GeForce GTX 970M    Off  | 00000000:01:00.0 Off |                  N/A |
| N/A   55C    P0    21W /  N/A |    743MiB /  3024MiB |      9%      Default |
+-------------------------------+----------------------+----------------------+

+-----------------------------------------------------------------------------+
| Processes:                                                       GPU Memory |
|  GPU       PID   Type   Process name                             Usage      |
|=============================================================================|
|    0      1072      G   /usr/lib/xorg/Xorg                           427MiB |
|    0      1607      G   compiz                                       244MiB |
|    0     18501      G   ...-token=7304AB02E32DD2ADCBD61CAE1B79FAB1    70MiB |
+-----------------------------------------------------------------------------+
```


## 2. Install CUDA Toolkit (CUDA 8.0)
You need to specify the `-test_file` in [`config.lua`](./config.lua) with a list of file names pointing to the images you are testing. [`./image/`](./image/) provides an example.

We provide several pretrained models for testing. You can download them in [`./model/`](./model/).

Run
```
$ apt-cache search nvidia
$ sudo apt-get install cuda-8-0
```


## 3. Install cuDNN v5.1 (Jan 20, 2017), for CUDA 8.0

sudo apt-get install libcudnn5-dev




## 4. Install Torch
