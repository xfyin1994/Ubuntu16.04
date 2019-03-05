# 配置pip镜像源
由于pytorch的安装包有500M左右的大小，不设置镜像源可能因为网速问题而失败。

## 国内镜像源列表
豆瓣(douban) http://pypi.douban.com/simple/ 
清华大学 https://pypi.tuna.tsinghua.edu.cn/simple/ 
阿里云 http://mirrors.aliyun.com/pypi/simple/ 
中国科技大学 https://pypi.mirrors.ustc.edu.cn/simple/ 
中国科学技术大学 http://pypi.mirrors.ustc.edu.cn/simple/ 
这里博主采用ailiyun镜像，原因是博主给Ubuntu也切换了源，在尝试各种镜像时ailyun最快

更新源
运行一下命令：
```
cd ~/.pip
```
如果不存在该文件夹则：
```
mkdir ~/.pip
cd ~/.pip
touch pip.conf
gedit pip.conf
```
在pip.conf中添加一下内容：
```
[global]
index-url = http://mirrors.aliyun.com/pypi/simple/
[install]
trusted-host=mirrors.aliyun.com
```
保存即可

安装pytorch
执行命令```pip install torch torchvision```根据自身情况可能需要在命令前加上```sudo``` 
结果如下
```
Looking in indexes: http://mirrors.aliyun.com/pypi/simple/
Collecting torch
  Downloading http://mirrors.aliyun.com/pypi/packages/e0/d2/e069611c5e05b4c0d77f841969aa0e6136c43b7a81c0a6cde4910e49a0ce/torch-0.3.1-cp27-cp27mu-manylinux1_x86_64.whl (496.9MB)
    100% |████████████████████████████████| 496.9MB 1.6MB/s 
```
测试是否安装成功
```
gph@gph-P452:~$ python
Python 2.7.12 (default, Dec  4 2017, 14:50:18) 
[GCC 5.4.0 20160609] on linux2
Type "help", "copyright", "credits" or "license" for more information.
>>> import torch
>>> 
```
原文：https://blog.csdn.net/u013832707/article/details/80076917 
