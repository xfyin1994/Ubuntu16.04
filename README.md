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

# 安装cuda9.0

cuda9.0下载地址：https://developer.nvidia.com/cuda-90-download-archive
```
按以上五个选项选择，然后将此文件下载下来。
终端输入：
sudo sh cuda_9.0.176_384.81_linux.run

安装过程中会执行一些确认信息，其中有一个更新驱动的选项，这个选择否。因为前边驱动我们已经正确安装。
等待安装完成，

配置环境变量：
sudo gedit ~/.bashrc

将以下内容写入到~/.bashrc尾部：
export PATH=/usr/local/cuda-9.0/bin${PATH:+:${PATH}}
export LD_LIBRARY_PATH=/usr/local/cuda-9.0/lib64${LD_LIBRARY_PATH:+:${LD_LIBRARY_PATH}}
 
在终端执行命令
source ~/.bashrc
让配置立即生效

测试CUDA的sammples：
cd /usr/local/cuda-9.0/samples/1_Utilities/deviceQuery #由自己电脑目录决定
sudo make
sudo ./deviceQuery

```
