配置pip镜像源
由于pytorch的安装包有500M左右的大小，不设置镜像源可能因为网速问题而失败。

国内镜像源列表
豆瓣(douban) http://pypi.douban.com/simple/ 
清华大学 https://pypi.tuna.tsinghua.edu.cn/simple/ 
阿里云 http://mirrors.aliyun.com/pypi/simple/ 
中国科技大学 https://pypi.mirrors.ustc.edu.cn/simple/ 
中国科学技术大学 http://pypi.mirrors.ustc.edu.cn/simple/ 
这里博主采用ailiyun镜像，原因是博主给Ubuntu也切换了源，在尝试各种镜像时ailyun最快

更新源
运行一下命令：

cd ~/.pip
如果不存在该文件夹则：
mkdir ~/.pip
cd ~/.pip
touch pip.conf
gedit pip.conf
在pip.conf中添加一下内容：

[global]
index-url = http://mirrors.aliyun.com/pypi/simple/
[install]
trusted-host=mirrors.aliyun.com

保存即可
原文：https://blog.csdn.net/u013832707/article/details/80076917 
