HUION和GAOMON无驱Linux内核模块的安装
=======================

安装方法
----------

**注意:** 需要Kernel v3.5或者更高的内核版本.

### 一.克隆代码到本地，在终端输入以下命令：

    git clone https://github.com/Tiger-D-Chen/digimend-kernel-drivers

### 二.安装内核驱动编译环境
#### 1.安装Linux内核头文件
##### 1.1 Debian系发行版(如Ubuntu,Mint,Deepin等)，在终端输入以下命令：

    sudo apt-get install -y "linux-headers-$(uname -r)"

##### 1.2 Fedora系发行版(如Fedora,CentOS等)，在终端输入以下命令：

    sudo dnf install -y "kernel-devel-uname-r == $(uname -r)"

#### 2.安装DKMS
##### 2.1 Debian系发行版(如Ubuntu,Mint,Deepin等)，在终端输入以下命令：

    sudo apt-get install -y dkms

##### 2.2 Fedora系发行版(如Fedora,CentOS等)，在终端输入以下命令：

    sudo dnf install -y dkms

### 三.安装内核驱动模块
##### 3.1 终端中进入clone代码的路径下digimend-kernel-drivers文件夹，进入该文件夹：

    cd */digimend-kernel-drivers/

**注意:** ` /digimend-kernel-drivers/为你电脑中实际的路径, 比如：/home/tiger/Documents/digimend-kernel-drivers/ `

##### 3.2 然后执行：

    sudo make dkms_install

##### 3.3 如果你之前已经装过digimend-kernel-drivers驱动，则需要首先执行:

    sudo make dkms_uninstall
    sudo dkms remove digimend/12 --all
    sudo rm -r /usr/src/digimend-12

然后再次执行：

    sudo make dkms_install

##### 3.4 操作完成后，重启系统。
### 四.可能遇到的问题及解决方法
##### 4.1 报错信息包含：`ERROR: Kernel configuration is invalid. include/generated/autoconf.h or include/config/auto.conf are missing. Run 'make oldconfig && make prepare' on kernel src to fix it.`
###### 解决办法:

    sudo apt install --reinstall linux-headers-$(uname -r)
    sudo reboot

##### 4.2 报错信息包含：`/bin/sh: flex：未找到命令 `
###### 解决办法: 

    sudo apt-get install bison
    sudo apt-get install flex

 卸载内核模块方法
----------   
终端里cd到digimend-kernel-drivers/文件夹，在此路径下执行如下命令

    sudo make dkms_uninstall
    sudo dkms remove digimend/12 --all
    sudo rm -r /usr/src/digimend-12
