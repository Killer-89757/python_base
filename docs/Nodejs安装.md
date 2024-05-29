# Nodejs安装

**功能**：可以运行js代码

**下载**：https://nodejs.org/en/download

----

1. 下载[node-v18.17.1-x64.msi](http://node-v18.16.1-x64.msi/)，除安装路径可以修改，其它一路next即可

![img](https://cdn.jsdelivr.net/gh/Killer-89757/PicBed/images/2024%2F05%2FFo6AY66NC8DN52PCdkbj7fLEXQ59-e7e8b4.png)

2. 如下为下载好的msi

![img](https://cdn.jsdelivr.net/gh/Killer-89757/PicBed/images/2024%2F05%2FFlVXVMLBZLYfSHfLF2I3kJ8oJNKK-b1f298.png)

3. 双击运行msi然后一路next，直到这里自定义安装路径修改下，比如我这里是`E:Software\nodejs\`

![img](https://cdn.jsdelivr.net/gh/Killer-89757/PicBed/images/2024%2F05%2FFk_93p9PclQg7aDRe4M88cEWU_Ke-1102c2.png)

4. 然后install就安装好了，最后finish即可

![img](https://cdn.jsdelivr.net/gh/Killer-89757/PicBed/images/2024%2F05%2FFsSHxRS_J2-G52kizz_C5Io5Ht-e-c99474.png)

5. 然后打开win+R输入cmd打开cmd窗口，输入node -v 如下输出版本号，就代表安装成功了

![img](https://cdn.jsdelivr.net/gh/Killer-89757/PicBed/images/2024%2F05%2FFhsEcoBOW-pV-V1Ibk26vSwV9a5C-e53e11.png)

6. 在刚刚安装nodejs的文件夹路径下`E:Software\nodejs\`新建一个node_cache文件夹

![img](https://cdn.jsdelivr.net/gh/Killer-89757/PicBed/images/2024%2F05%2FFsopMQ9PF77gtw6BsTPWVh23zsTT-30c76d.png)

7. 然后继续win+R输入cmd打开cmd窗口，输入如下4条命令，注意`E:Software\nodejs\`文件夹路径换成你自己的

```
npm config set registry https://registry.npm.taobao.org  ：设置淘宝镜像源

npm config set prefix E:\Software\nodejs\  ：修改npm全局（-g）模块安装所在路径

npm config set cache E:\Software\nodejs\node_cache  ：修改缓存cache的路径（ps：如果不修改，则默认到C盘位置C:\Users\Administrator\AppData\Roaming\npm）

npm root -g  ：查看node_modules的目录
```

![img](https://cdn.jsdelivr.net/gh/Killer-89757/PicBed/images/2024%2F05%2FFopaaZQ6k7KbhYrxEQ_jn8OTNoJg-1a6695.png)

8. 打开环境变量窗口，设置系统环境变量，新增NODE_PATH变量，`NODE_PATH = E:\Software\nodejs\node_modules`

![img](https://cdn.jsdelivr.net/gh/Killer-89757/PicBed/images/2024%2F05%2FFmDvKuVF1VNCj2cnIqq7jDmcMtkM-873b86.png)

9. 打开用户环境变量窗口，修改用户变量里的Path， 将`C:\Users\Administrator\AppData\Roaming\npm改成E:\Software\nodejs`，即确定完成

![img](https://cdn.jsdelivr.net/gh/Killer-89757/PicBed/images/2024%2F05%2FFov4whrB5x_4CxnVOGSDHsusrT3W-268ceb.png)

10. 测试安装js依赖模块，以管理员身份打开cmd窗口，如果没有以管理员身份打开cmd窗口，则会安装模块报错

![img](https://cdn.jsdelivr.net/gh/Killer-89757/PicBed/images/2024%2F05%2FFsiRnXREL9hAAzJ85IwBY3R3Xyvy-b19431.png)

![img](https://cdn.jsdelivr.net/gh/Killer-89757/PicBed/images/2024%2F05%2FFlD9or4zukkFwl1rQP329Ad3MzZ5-8071ae.png)

11. 然后输入`npm install express -g`，如下就代表安装成功了

![img](https://cdn.jsdelivr.net/gh/Killer-89757/PicBed/images/2024%2F05%2FFvkmc2X8KEJ3Fz-QXWj_qufyfBoO-354c4c.png)

12. 新建一个hello.js，然后node hello.js测试运行看看， 如下没有报错，nodejs已经安装成功

![img](https://cdn.jsdelivr.net/gh/Killer-89757/PicBed/images/2024%2F05%2FFgpi25_NknUq1DtVctjFJ1ZZEcM6-75b6bb.png)

13. npm install 是nodejs安装各种依赖包的方法，如果安装慢，可以尝试如下方法解决

```cmd
npm install gl -g --registry=http://registry.npm.taobao.org
npm install canvas -g --canvas_binary_host_mirror=https://registry.npmmirror.com/-/binary/canvas

或者如下
npm config set registry https://registry.npm.taobao.org
npm install gl -g 
npm install canvas

或者如下
npm install -g cnpm
cnpm install gl -g 
cnpm install canvas -g

或者如下
npm install -g nrm
nrm use taobao
nrm ls    查看可以用切换的源
npm install gl -g 
```

