# Ubuntu16.04
Ubuntu下环境的配置，tensorflow，docker等

# apt-get update 报错
出现类似如下提示
```
E: Could not get lock /var/lib/dpkg/lock – open (11: Resource temporarily unavailable)
E: Unable to lock the administration directory (/var/lib/dpkg/), is another process using it?
```
查看进程
```
ps aux | grep -i apt
```
kill进程
```
sudo kill -9 <process id>
```


# 修改conda镜像源
在终端中运行以下命令修改镜像源,可以明显加速安装.
```
# 优先使用清华conda镜像
conda config --prepend channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/

# 也可选用科大conda镜像
conda config --prepend channels http://mirrors.ustc.edu.cn/anaconda/pkgs/free/
```
要查看镜像源是否安装成功的话,建议终端中运行以下命令:
```
conda config --set show_channel_urls yes
```
会生成一个~/.condarc文件,运行cat命令查看文件内容
```
cat ~/.condarc
```
显示内容为
```
channels:
  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/
  - http://mirrors.ustc.edu.cn/anaconda/pkgs/free/
  - defaults
show_channel_urls: true
```
这样每次用conda安装时,在package右边都会显示安装源的地址,那么我们对于安装的时间能有一个大致的估计. 
修改后,用conda安装镜像源中任何库都能明显加速,在我的电脑上安装速度级可以达到MB/s 
原文：https://blog.csdn.net/yucicheung/article/details/79094657 

# anaconda

## Ubuntu安装anaconda之后打开终端出现（base）
![(base) yin@yin-System-Product-Name](https://github.com/xfyin1994/Ubuntu16.04/blob/master/wdP8C.png)

这也可以因为auto_activate_base设置为True。您可以使用以下命令进行检查
```
conda config --show | grep auto_activate_base
```
将其设置为false
```
conda config --set auto_activate_base False
```
## conda清理瘦身

anaconda就像一个相对独立的生态，所有被安装的包都在anaconda的安装目录下客观存在者，客观占用着我们的硬盘空间，随着使用到的包越来越多，一次次伴随安装的依赖包也越来越多，还有Python每个版本都对应了自身的一整套包，例如Python3.5和3.6就分别对应了各自的一整套包，anaconda文件夹的体积也越来越大，突发奇想查看一下呗，7.8G，瞬间被吓倒，怎么解决呢，很简单！

conda clean就可以轻松搞定！
第一步：通过```conda clean -p```来删除一血没用的包，这个命令会检查哪些包没有在包缓存中被硬依赖到其他地方，并删除它们。
第二步：通过```conda clean -t```可以将conda保存下来的tar包。经过上面两步，我的anaconda便变成了4.3G，几乎瘦身一半。
有一点要注意的是，```conda clean```命令是对所有anaconda下的包进行搜索，当然也包括构建的其他Python环境中的包，这一点还是很高效的，不用再进入其他环境重复操作。
原文：https://blog.csdn.net/marsjhao/article/details/62884246 

# CUDA
## 卸载CUDA
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

## 安装cuda9.0

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
# 安装cudnn
https://developer.nvidia.com/rdp/cudnn-archive 下载cudnn(需要注册账号登录)：
 
 ××cuDNN v7.0.5 Library for Linux××
```
下载好cudnn-9.0-linux-x64-v7.tgz之后：

cd ~/下载
tar zxvf cudnn-9.0-linux-x64-v7.tgz
cd cuda/include/
sudo cp cudnn.h /usr/local/cuda/include/    #复制头文件

再将cd进入lib64目录下的动态文件进行复制和链接：
cd cuda/lib64/

sudo cp lib* /usr/local/cuda/lib64/    #复制动态链接库
cd /usr/local/cuda/lib64/
sudo rm -rf libcudnn.so libcudnn.so.7    #删除原有动态文件
sudo ln -s libcudnn.so.7.0.5 libcudnn.so.7  #生成软衔接（注意这里要和自己下载的cudnn版本对应，可以在/usr/local/cuda/lib64下查看自己libcudnn的版本）
sudo ln -s libcudnn.so.7 libcudnn.so      #生成软链接

安装完成。

```
# Tensorflow配置环境报错
## 关于python安装tensorflow出现No matching distribution found for tensorflow的一种解决
```
pip install -i https://pypi.tuna.tsinghua.edu.cn/simple/ --upgrade tensorflow
复制安装完美解决，前提是python是64位
```

### tensorflow清华源下载安装
pip，pip3注意对应不同的python版本
```
sudo pip3 install tensorflow-gpu==1.8 -i https://pypi.tuna.tsinghua.edu.cn/simple
```
# ubuntu16.04安装python2.7
```
sudo apt-get update
sudo apt-get install python-minimal python-dev
```
# ubuntu16.04同时使用 pyhton2.7和3.5，并随意切换
```
cd /usr/bin
sudo mv python python.bak
sudo ln -s python2.7 python
sudo ln -s python3.5 python3
```
# 关于解决Ubuntu16.04中pip和pip3同时指向Python3.5的问题
##分别用以下命令安装pip、pip3
```
sudo apt install python-pip

sudo apt install python3-pip
```
```
which pip 
#我的显示如下：
#/usr/local/bin/pip
vim /usr/local/bin/pip
```

可能遇到的问题：
我无法编辑里面的内容，需要先更改文件的权限，方法如下：
进入到/usr/local/bin 路径下，输入：
```
sudo chmod 777 xxx #(xxx是指文件名，777是指将所有对此文件的操作权限赋予用户)
```
然后接着上一步：
编辑 pip文件：
将第一行 #!/usr/bin/python3 修改为
```
#!/usr/bin/python2
```
保存之后，在查看一下pip的指向，就发现已经指向了Python2.7，大功告成

## 如果报如下错误的话
```
Traceback (most recent call last):
  File "/usr/local/bin/pip", line 7, in <module>
    from pip._internal import main
ImportError: No module named _internal
```
执行如下代码
```
python -m pip install --upgrade pip
```
