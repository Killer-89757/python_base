# 禁止chrome更新与chrome同时多开高低版本分身

## 背景目的

- 本地有一个最新版本的chrome浏览器，想安装一个低版本的浏览器，**同时希望两个版本的浏览器都存在，不自动更新**；可以用来调试不同网站js想看行号的情况，就用低版本浏览器，有强迫症的时候用最新版本的浏览器

- 如图，最新版本浏览器 https://www.google.cn/chrome/next-steps.html?statcb=1&installdataindex=empty&defaultbrowser=0

  ![img](https://cdn.jsdelivr.net/gh/Killer-89757/PicBed/images/2024%2F05%2FFl9_mChkFf02rffqmidxirSzo4Yv-c9133e.png)

- 我当前的版本是**最新版本124的浏览器**

  ![img](https://cdn.jsdelivr.net/gh/Killer-89757/PicBed/images/2024%2F05%2FFr-sXj06ZJCKUtm75fyc5-dx0Qv3-7bb858.png)

## 禁止更新限制

- 打开C:\Program Files (x86)\Google\Update， 如果有[GoogleUpdate.exe](http://googleupdate.exe/)，删除该目录下[GoogleUpdate.exe](http://googleupdate.exe/)，目的是使google的自动更新程序失效

  ![img](https://cdn.jsdelivr.net/gh/Killer-89757/PicBed/images/2024%2F05%2FFgwaeEVENIDI042wUGVMGgr_jCqV-79cf50.png)

- 然后新建[GoogleUpdate.txt](http://googleupdate.txt/)文件，里面随便写什么内容，复制到该目录C:\Program Files (x86)\Google\Update下面

  ![img](https://cdn.jsdelivr.net/gh/Killer-89757/PicBed/images/2024%2F05%2FFmeKfB_S4pYWxke6vcWkAitZusK1-dd71ca.png)

- 然关掉chrome在打开chrome，到如下地址页面chrome://settings/help ，即可发现已经**禁止更新**

  ![img](https://cdn.jsdelivr.net/gh/Killer-89757/PicBed/images/2024%2F05%2FFubMlA8dNpUVqmC4o0kgoXL7sAvf-7f053d.png)

## 下载个旧版的浏览器与同时多开高低版本分身

- 下载107版本的谷歌浏览器，https://www.chromedownloads.net/chrome64win/

  ![img](https://cdn.jsdelivr.net/gh/Killer-89757/PicBed/images/2024%2F05%2FFkBOiy5Xd5vGoFOQuFlQc9-23eju-c19530.png)

- 然后进行**两次**解压，其中7-zip软件到这里下载 https://t.zsxq.com/Txtwj

  ![img](https://cdn.jsdelivr.net/gh/Killer-89757/PicBed/images/2024%2F05%2FFpW0OnXc_zPgbfh3izeWfn4NI8RL-894577.png)

  ![img](https://cdn.jsdelivr.net/gh/Killer-89757/PicBed/images/2024%2F05%2FFtiKhPiswsL00DCminwZOSLj1vbp-830b13.png)

- 紧接着我们到这个目录下面来 107.0.5304.122_chrome64_stable_windows_installer\chrome\Chrome-bin  

  ![img](https://cdn.jsdelivr.net/gh/Killer-89757/PicBed/images/2024%2F05%2FFnDKrUgJ_DkJnz5_HcWCeqwtqEYx-de78ff.png)

- 并对桌面进行快捷方式的命名

  ![img](https://cdn.jsdelivr.net/gh/Killer-89757/PicBed/images/2024%2F05%2FFgSG3KV_cb2Jp3bmm-poU9a9APBb-c7cb9b.png)

- 然后新建一个空白的文件夹chrome107，并记住它的文件夹路径地址，比如我的 "F:\othersoft\107.0.5304.122_chrome64_stable_windows_installer\chrome\Chrome-bin\chrome107"

  ![img](https://cdn.jsdelivr.net/gh/Killer-89757/PicBed/images/2024%2F05%2FFhfMPCs5FInFrVKDhN2rpE0SsyxE-0c943b.png)

- 修改桌面快捷方式图标chrome107，右键属性进行修改为F:\othersoft\107.0.5304.122_chrome64_stable_windows_installer\chrome\Chrome-bin\chrome.exe --user-data-dir="F:\othersoft\107.0.5304.122_chrome64_stable_windows_installer\chrome\Chrome-bin\chrome107"

  ![image.png](https://cdn.jsdelivr.net/gh/Killer-89757/PicBed/images/2024%2F05%2FFnsPgdjf5afoqiCe15Mz4m2_qtMk-3aa88c.png)

- 最后分别打开chrome124的快捷方式，chrome107的快捷方式，可以发现两个浏览器各用各的版本了，及实现了Chrome多开高低版本分身

  ![img](https://cdn.jsdelivr.net/gh/Killer-89757/PicBed/images/2024%2F05%2FFgSG3KV_cb2Jp3bmm-poU9a9APBb-54e009.png)

  ![img](https://cdn.jsdelivr.net/gh/Killer-89757/PicBed/images/2024%2F05%2FFi8dPfPKXMFQGbsk0MdOeaudwHFy-7259c2.png)

参考文档：

- https://blog.csdn.net/qq_41336022/article/details/130577357

- https://www.slimjet.com/chrome/google-chrome-old-version.php