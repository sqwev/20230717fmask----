# Fmask4.6在Windows和Linux上的安装与配置说明

Fmask是一款针对Landsat和Sentinel-2的去云软件。但是由于其本身的安装对于不大熟悉Linux的用户来说比较困难，所以本文将介绍如何在Windows和Linux上安装Fmask4.6，并且配置好Fmask4.6的环境变量。

软件项目地址：https://github.com/GERSL/Fmask

软件下载：https://drive.google.com/drive/folders/1yFXIlxWU7NeaQ4EK3Uj-VR2uggrPWjgo
## 1. Windows上安装Fmask4.6

1. 按照默认安装

2. 将Fmask安装路径(C:\Program Files\GERS\Fmask_4_6\application)加入环境变量

运行方式
```
PS G:\My_phd\phd1_shang\20220907TryCloudDetection\new\S2B_MSIL1C_20220830T021529_N0400_R003_T52TFS_20220830T040747.SAFE\GRANULE\L1C_T52TFS_A028629_20220830T022209> Fmask_4_6

```

## 2. Linux上安装Fmask4.6


1. 安装准备文件

（1）.MATLAB Runtime R2021a (9.12)在以下页面下载
https://www.mathworks.com/products/compiler/mcr/index.html

（2）.Fmask4.6 Linux版

2. 安装

（1）使用`unzip [***.zip] -d [dir]`解压两个zip压缩包

（2）输入`sudo ./install -mode silent -agreeToLicense yes`安装MATLAB Runtime R2021a，如果这个不行，就使用root权限进行安装

安装后，需要在目标计算机上，将以下内容追加到环境变量 LD_LIBRARY_PATH 的末尾:
```
/usr/local/MATLAB/MATLAB_Runtime/v910/runtime/glnxa64/usr/local/MATLAB/MATLAB_Runtime/v910/bin/glnxa64:/usr/local/MATLAB/MATLAB_Runtime/v910/sys/os/glnxa64:/usr/local/MATLAB/MATLAB_Runtime/v910/extern/bin/glnxa64
```
如果 MATLAB Runtime 要与 MATLAB Production Server 或 MATLAB Web App Server 配合使用，则不需要修改上面的环境变量。

（3）执行`chmod +x Fmask_4_6_Linux_mcr.install`，改变文件权限

（4）执行`./Fmask_4_6_Linux_mcr.install -mode silent -agreeToLicense yes`安装Fmask4.6，如果这个不行，就使用root权限进行安装

3. 修改环境变量

在`.bashrc`文件的末尾加上
```bash
export XAPPLRESDIR=$XAPPLRESDIR:/usr/local/MATLAB/MATLAB_Runtime/v910/X11/app-defaults
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/MATLAB/MATLAB_Runtime/v910/runtime/glnxa64:/usr/local/MATLAB/MATLAB_Runtime/v910/bin/glnxa64:/usr/local/MATLAB/MATLAB_Runtime/v910/sys/os/glnxa64:/usr/local/MATLAB/MATLAB_Runtime/v910/sys/opengl/lib/glnxa64```
```
4.运行方式

```
(base) shenzhouaZengLabGpu:/media/data_repo/s2A MSI20210817T020701_N0301_R10T52TGR_20210817T040839.SAFE/GRANULE/L1C_T52TGR_A032132_20210817T020655S /usr/GERS/Fmask_4_6/application/Fmask_4_6
Fmask 4.6 start ...
Cloud/cloud shadow/snow dilated by 3/3/0 pixels.
cloud probability threshold of 20.00%.
Load or calculate TOA reflectances .Narning: Fail to locate the auxiliary data. please input the directory path of+he auxiliary data.
Detect potential clouds, cloud shadows, snow, and water .
Match cloud shadows with clouds.
Fmask 4.6 finished (2.37 minutes)
for L1C T52TGR A032132 20210817T020655 with 87.76% clear pixels
```