# Windows自救笔记
- tags: windows, python, setuptools, mingw

----

由于种种原因，这两天不能用OS X了，只能在一台悲剧的Windows上生存..
Windows的生存环境真的非常差，所以有了这篇自救笔记。

切换到Windows之后的第一件事就是与真实世界联系上，我用的GoAgent，下载运行之后在IE里面这么设置一下就可以了：
http://ww3.sinaimg.cn/large/a74eed94jw1dwh2wwyf1oj.jpg

##基本软件选用
浏览器：Chrome （其实我更喜欢Safari，不过坑爹的...Safari 6没有Windows版本）
聊天：[QQ国际板](http://download.imqq.com/download.shtml) （没有广告）
密码管理：[1Password](https://agilebits.com/onepassword/win) 
SSH：PuTTY
Git：王八git..实在是不喜欢"Windows 8 风格"
网盘：Dropbox
压缩：7-Zip
编辑器：Notepad++

##Python的设置
我装的是Python 2.7..**我的Python装在C盘，不在C盘的自己手动改盘符..**
直接从官网下载安装包，然后在http://pypi.python.org/pypi/setuptools/0.6c11 拉到最下面，找到`setuptools-0.6c11.win32-py2.7.exe`，下载，安装。
然后把`C:\Python27;C:\Python27\Scripts;`加到PATH里.打开CMD，输入Python应该就能看到Python提示符了.
退出Python，在CMD里输入`easy_install pip`就把pip拉下来了...
后面就很简单了.
需要注意的是，如果想要在Windows下编译Python的C库的话默认需要VC2008..
不过可以设置MingW为默认编译器（***记得把MingW的bin目录`C:\MinGW\bin`加到PATH里***）：在`C:\Python27\Lib\distutils`目录下新建个`distutils.cfg`文件，内容写：
```
[build]
compiler = mingw32
```
或者可以在每次安装库的时候手动指定`-compiler=mingw32`。

----

我在使用中遇到了这样的提示：
```
gcc: 错误：unrecognized command line option ‘-mno-cygwin’

error: command 'gcc' failed with exit status 1
```
搜索之后[知道这是一个bug](http://stackoverflow.com/questions/9645004/python-mno-cygwin)，打开`C:\Python27\Lib\distutils\cygwinccompiler.py`并删去文件内所有的` -mno-cyg`和` -mno-cygwin`即可。

***在Windows上搞Python开发真的很反人类***

##SSH密钥
PuTTY和王八git都不可以直接使用OpenSSH的密钥（果然Windows上面的软件都不是一般的奇葩），需要使用[PuTTYgen](http://the.earth.li/~sgtatham/putty/latest/x86/puttygen.exe)转换一下（打开PuTTYgen->Conversions->Import Key->选中密钥，打开->Save private key）

##系统美化
看久了OS X之后看Windows的字体非常不舒服。。
在字体美化上，推荐使用[MacType](https://code.google.com/p/mactype/downloads/list),下载安装之后按用户向导照设置一下就可以了..效果很好

##生活习惯
OS X和Windows的Ctrl(Command)/Alt的键位基本是反的..
在http://www.piaodown.com/soft/43226.htm 这里可以下到一个改键工具，（需要.Net 2.0支持，可以在http://www.onlinedown.net/soft/38669.htm 下载到）
然后把Ctrl和Alt互换一下位置就可以了..

不得不吐槽一句，1Password的Windows版本界面实在是太恶心了...
http://ww3.sinaimg.cn/large/a74ecc4cjw1dwh2u5dh2oj.jpg