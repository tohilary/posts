# 果粉Pythoner的Windows自救笔记
- tags: python, windows

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