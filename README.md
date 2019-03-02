# Ubuntu16.04
Ubuntu下环境的配置，tensorflow，docker等


# 卸载CUDA
注意以下的命令都是在root用户下操作的。

卸载CUDA很简单，一条命令就可以了，主要执行的是CUDA自带的卸载脚本，读者要根据自己的cuda版本找到卸载脚本：
```
sudo /usr/local/cuda-8.0/bin/uninstall_cuda_8.0.pl
```
卸载之后，还有一些残留的文件夹，之前安装的是CUDA 8.0。可以一并删除：
```
sudo rm -rf /usr/local/cuda-8.0/
```
这样就算卸载完了CUDA。


