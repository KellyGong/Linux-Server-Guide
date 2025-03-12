# 服务器系统盘清理

服务器系统盘主要是由于大家在 （1）使用 ``pip install`` 和 ``conda install`` 时程序默认将下载的包缓存在系统盘上，导致经常需要清理，（2）以及在 ``conda create -n`` 时将环境直接安装在系统盘。


**大家记得先使用全局替换，将 gongzheng 替换为自己的名字**

**数据盘路径，3090 为 /home/data/用户名/，A6000为 /data/用户名/ （这里以3090为例）**


## 服务器缓存清理和一劳永逸设置

### pip 和 conda 缓存清理
```
pip cache purge
conda clean --all
```

### 指定 pip 包缓存位置

在用户目录下，执行命令 ``vi ~/.pip/pip.conf`` （参考3090服务器系统盘在 /home/data下，用户名是 gongzheng，自行替换对应信息）

```
[global]
index-url = https://pypi.tuna.tsinghua.edu.cn/simple
cache-dir = /home/data/gongzheng/pip
[install]
trusted-host = https://pypi.tuna.tsinghua.edu.cn
```

### 指定 conda 包缓存位置

在用户目录下，执行命令 ``vi ~/.condarc`` （参考3090服务器系统盘在 /home/data下，用户名是 gongzheng，自行替换对应信息）

```
channels:
  - defaults
show_channel_urls: true
default_channels:
  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main
  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/r
  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/msys2
custom_channels:
  conda-forge: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
  msys2: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
  bioconda: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
  menpo: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
  pytorch: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
  pytorch-lts: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
  simpleitk: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
  deepmodeling: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/
pkgs_dirs:
  - /home/data/gongzheng/pkgs
```


## 服务器环境路径设置

### 迁移系统盘环境到数据盘 (举例有个环境名称为 torch，通过 conda create -n 创建)

首先拷贝环境
```
conda create -p=/home/data/gongzheng/envs/torch --clone torch
```
`-p` 为 指定安装路径为数据盘，比方说所有环境存在``envs`` 下，环境名称不变，仍为 torch

删除对应的环境
```
conda remove -n torch --all
```

**以上步骤重复执行，将所有个人环境迁移至数据盘**

### 修改 conda 配置文件，即可如之前一样使用 conda create -n torch，conda install 一样使用

在 ``~/.condarc`` 文件最后添加

```
envs_dirs:
  - /home/data/gongzheng/envs
```
