# Charles安装及配置

## 一、安装激活

下载地址：https://www.charlesproxy.com/download/

下载完成之后安装即可。

激活码获取地址：https://www.zzzmode.com/mytools/charles/

![img](https://cdn.jsdelivr.net/gh/Killer-89757/PicBed/images/2024%2F05%2FFjHXWirtdbJJwqiNmacKZkPF3B6a-5ab57b.png)

上图输出框内随便输入一个名称，然后点击生成，之后就会生成一个激活码了，之后打开**Charles**，点击**Help，**然后点击下图圈出来的：

![img](https://cdn.jsdelivr.net/gh/Killer-89757/PicBed/images/2024%2F05%2FFsTsfmexjDgW_U8-oSQ-Nyov3lg7-efd067.png)

之后跳出如下：

![img](https://cdn.jsdelivr.net/gh/Killer-89757/PicBed/images/2024%2F05%2FFk6NUdRtxmq53ZkOugAh9fWSPBYX-0f3c1d.png)

后这里填上刚才在获取激活码页面输入框中输入的名称和获取的激活码即可，跳出如下代表激活完成：

![img](https://cdn.jsdelivr.net/gh/Killer-89757/PicBed/images/2024%2F05%2FFrkTjoYQSdIGDDJfxBOzzMGJZ6Z_-6b372b.png)

## 二、代理配置

### 2.1 代理设置

打开**Charles**，点击Proxy ==> Proxy Settings，之后按照下图配置：

![img](https://cdn.jsdelivr.net/gh/Killer-89757/PicBed/images/2024%2F05%2FFrwNRdxFzhxCFawgSzw-XdnxwtN5-9c62d9.png)

上图中的端口可以自行配置

### 2.2 抓取端口设置

点击Proxy --> SSL Proxy Settings

1. 勾选Enable SSL Proxying
2. 点击Add，添加抓取端口 * : *

![img](https://cdn.jsdelivr.net/gh/Killer-89757/PicBed/images/2024%2F05%2FFuwS0IBYwWS3Ziw3VycayM_wOkji-4c0b81.png)![img](https://cdn.jsdelivr.net/gh/Killer-89757/PicBed/images/2024%2F05%2FFuABVWMVIUy3DyaRDNWZnzJWfkly-cedd9b.png)

## 三、证书配置

### 3.1 电脑证书信任

依次点击**Help** ==> **SSL Proxying** ==> **Install Charles Root Certificate** ==> **安装证书** ==> **本地计算机** ==> **将所有的证书都放入下列存储** ==> **点击浏览,选择”受信任的根证书颁发机构”** ==> **完成**



**验证:**

**Help** ==> **SSL Proxying** ==> **Install Charles Root Certificate** ==> **证书路径** ==> **证书状态显示”该证书没有问题”**即可

![img](https://cdn.jsdelivr.net/gh/Killer-89757/PicBed/images/2024%2F05%2FFj1hzTZrpdJq64BEuq7TxHjrCGvx-335fc0.png)



### 3.2 手机信任

1. 依次点击**Help** ==> **SSL Proxying** ==> **Install Charles Root Certificate on a Mobile Device or Remote Browser**

![img](https://cdn.jsdelivr.net/gh/Killer-89757/PicBed/images/2024%2F05%2FFmHBpQAHvjL3fgsRQlaPNTIbNQrC-fbde1a.png)

2. **手机设置** --> **无限区域网** --> **选择WIFI** --> **配置代理** --> **输入电脑ip,端口8888 (IP可在Help -> Local IP Addresser查看)**

3. 打开浏览器 --> 输入 **[chls.pro/ssl](http://chls.pro/ssl)**下载证书

4. 安装下载好的证书

5. 信任证书