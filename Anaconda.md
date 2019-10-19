# 使用conda安装requirement.txt指定的依赖包
2019-04-24 20:39:19 Jonah_Mao 阅读数 2276更多
分类专栏： Python
版权声明：本文为博主原创文章，遵循 CC 4.0 BY-SA 版权协议，转载请附上原文出处链接和本声明。
本文链接：https://blog.csdn.net/Mao_Jonah/article/details/89502380
许多Python项目中都包含了requirements.txt文件，该文件记录了当前程序的所有依赖包及其精确版本号。

## 生成requirement.txt文件
```
pip freeze > requirements.txt
```
### 安装requirement.txt文件依赖
```
pip install -r requirements.txt
```
## 除了使用pip命令来生成及安装requirement.txt文件以外，也可以使用conda命令来安装。
```
conda install --yes --file requirements.txt
```
但是这里存在一个问题，如果requirements.txt中的包不可用，则会抛出“无包错误”。
使用下面这个命令可以解决这个问题
```
$ while read requirement; do conda install --yes $requirement; done < requirements.txt
```
如果想要在conda命令无效时使用pip命令来代替，那么使用如下命令：
```
$ while read requirement; do conda install --yes $requirement || pip install $requirement; done < requirements.txt
```
也可以这样子操作
## 导出到.yml文件
```
conda env export > freeze.yml
```
## 直接创建conda环境
```
conda env create -f freeze.yml
```

Reference：
Install only available packages using “conda install --yes --file requirements.txt” without error
