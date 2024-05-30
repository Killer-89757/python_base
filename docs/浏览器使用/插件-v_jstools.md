# 插件-v_jstools

**功能**：生成临时环境/hook功能/注入代码/解混淆

**下载**：https://github.com/cilame/v_jstools

**文档**： https://www.jsdebug.cn/#/toolsbook 

---

**下载如图：**

![img](https://cdn.jsdelivr.net/gh/Killer-89757/PicBed/images/2024%2F05%2FFubeXtBHLDv4sutHVMe6L6yUiORT-e52958.png)

**安装如图：**chrome://extensions/

![img](https://cdn.jsdelivr.net/gh/Killer-89757/PicBed/images/2024%2F05%2FFqixnP8TjmRbEtvpN1n4YC6qG5QM-f989d9.png)

![img](https://cdn.jsdelivr.net/gh/Killer-89757/PicBed/images/2024%2F05%2FFhKVEckA2d6dmzzpOZ8IdV1dsUjy-9eca2d.png)

------



### 功能用途一：生成临时环境

1. 先点击打开如下两个开关，然后打开配置页面

![img](https://cdn.jsdelivr.net/gh/Killer-89757/PicBed/images/2024%2F05%2FFmZg_aZ2iyS7g7WBI4foY1_7PqSa-ae4457.png)

2. 如下插件配置详情，勾选上总开关，DOM开关，以及常用的挂钩，然后关掉该配置页面

![img](https://cdn.jsdelivr.net/gh/Killer-89757/PicBed/images/2024%2F05%2FFsrSzgzQ-mXaBUnmRTVXYUs3BChF-5e9df4.png)

3. 打开一个网址，刷新网页，然后点击插件的生成临时环境

![img](https://cdn.jsdelivr.net/gh/Killer-89757/PicBed/images/2024%2F05%2FFpUN0ZqSf3Mgku_S6LcsqcObaCad-4c3872.png)

4. 刷新网页后，需要简单的往下滑动翻页下，这时候再点击生成临时环境

![img](https://cdn.jsdelivr.net/gh/Killer-89757/PicBed/images/2024%2F05%2FFhOk59NgoO81_tWfiVxMDPvdOCcM-9a083e.png)

5. 点击确定后，ctrl+v粘贴到本地新建的js文件中

![img](https://cdn.jsdelivr.net/gh/Killer-89757/PicBed/images/2024%2F05%2FFjpQ36U069Z4mKP-a10_ShNUye8I-ca9d02.png)

6. 接下来就是js生成目标参数了，比如你要生成cookie的参数，刚刚复制的环境内容放在最上方，生成加密参数的js放中间，最下方输出你想要研究的目标参加即可，这个在接下来的补环境文章里面会进一步介绍，**注意，插件补的环境可能不太全，不是所有的网站都可以，有的还需要自己细细调整，才能生成最终的结果参数**

![img](https://cdn.jsdelivr.net/gh/Killer-89757/PicBed/images/2024%2F05%2FFnik2NkV-XuqJc97SxEfzAJE6TYN-7611b8.png)

7. 如下置空日志打印函数：var v_console_log = function(){{}}  ， 即可在运行的时候就不会有日志输出，调试的时候仍然需要打开看日志输出

![img](https://cdn.jsdelivr.net/gh/Killer-89757/PicBed/images/2024%2F05%2FFtH194swIJtL7hUl5YRzcyxwgj4F-fd1e7d.png)

------

### 功能用途二：hook-cookie

1. 先点击打开如下两个开关，然后打开配置页面

![img](https://cdn.jsdelivr.net/gh/Killer-89757/PicBed/images/2024%2F05%2FFt5sL73JVtccRCXk3XCsHNZw7VaB-5b2972.png)

2. 在配置页面如下勾选

![img](https://cdn.jsdelivr.net/gh/Killer-89757/PicBed/images/2024%2F05%2FFp3vM7wRVl2OCNFmExlszyuuO_kM-5489c0.png)

3. 然后网页清掉缓存，刷新网页

![img](https://cdn.jsdelivr.net/gh/Killer-89757/PicBed/images/2024%2F05%2FFp1VxSBH7rTbMXm5NaTixbmUp25--09cb8a.png)

4. 如下刷新网页后，点击调试js，在生成cookie的位置就会被插件hook拦截到，在conosle界面就会有如下cookie输出了，在Call Stack界面可以通过堆栈回溯反推cookie怎么生成的，以上就是插件hook-cookie的用法

![img](https://cdn.jsdelivr.net/gh/Killer-89757/PicBed/images/2024%2F05%2FFgsGXbubsHVlqeYAqds_4BjVCrlL-772b2c.png)