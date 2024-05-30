# Fiddler安装及配置

## 前言：

Fiddler都是大家常用的抓包软件，网上也有很多安装及配置的文章，然后下面的安装及配置过程是比较详细的，大家可以参考下，这一篇不是重点，重点是下一篇，会提到一些比较好用的插件，这一篇安装及配置的文章主要是方便大家有需要的时候观看。

## 一、安装

官网下载地址（最新版本）**：**https://www.telerik.com/download/fiddler

### 1.下载步骤：

1. 在谷歌浏览器打开下载网址，翻译为中文网页，根据提示下载到电脑常用磁盘
2. 下载地址网页：

Download Fiddler→How do you plan to use Fidder? （此处任选一个答案）

- Your email（填写你的邮箱地址）

- Country（国家，此处选择China）

- 勾选“ I accept the Fiddler End User License Agreement”

- Download For Windows（点击下载Windows系统最新版本fidder）

![img](https://cdn.jsdelivr.net/gh/Killer-89757/PicBed/images/2024%2F05%2FFmSNqFZZgsEbSReappAEq_FOPNQQ-14ca80.png)

### 2.fiddler安装

**安装步骤：**

1. 点击打开[FiddlerSetup.exe](http://fiddlersetup.exe/)程序，自定义安装到电脑常用磁盘下；
2. 安装后，点开安装的fidder目录，点击启动**[Fiddler.exe](http://fiddler.exe/)**程序，打开**fidder**软件，表示安装成功。

![img](https://cdn.jsdelivr.net/gh/Killer-89757/PicBed/images/2024%2F05%2FFrc1hE6z2-VCzc_gAtrTwRE98lVF-6416d3.png)![img](https://cdn.jsdelivr.net/gh/Killer-89757/PicBed/images/2024%2F05%2FFtEIzBjGIz-hAvWqhx0mitsQpdOc-f5e52a.png)![img](https://cdn.jsdelivr.net/gh/Killer-89757/PicBed/images/2024%2F05%2FFnID4tLizwG9hsJtyOmbq50xfwc7-53c03a.png)![img](https://cdn.jsdelivr.net/gh/Killer-89757/PicBed/images/2024%2F05%2FFjaw2eoMBUG2CnWUSByGLsYeaJlm-bcc556.png)![img](https://cdn.jsdelivr.net/gh/Killer-89757/PicBed/images/2024%2F05%2FFsciQuqNqU3wrDMy7WoX5FX9dRuk-ac1d16.png)![img](https://cdn.jsdelivr.net/gh/Killer-89757/PicBed/images/2024%2F05%2FFsbm1ZEzPkbW-t5SYS2a2lSog227-d207ec.png)![img](https://cdn.jsdelivr.net/gh/Killer-89757/PicBed/images/2024%2F05%2FFpUv8yXpp-q-LT8LmFF2541G9h1C-9420fe.png)![img](https://cdn.jsdelivr.net/gh/Killer-89757/PicBed/images/2024%2F05%2FFicKrefSUu40nGcPys5wMWIqN-fc-9ab4e6.png)

## 二、fiddler配置

双击[Fiddler.exe](http://fiddler.exe/)，弹出“**AppContainer Configuration**”对话框，点击“**cancel**”就行。

**Progress Telerik Fiddler Web Debugger**菜单栏中，**Tools——Options**。

![img](https://cdn.jsdelivr.net/gh/Killer-89757/PicBed/images/2024%2F05%2FFu6VeRT4SzpV8-vywIlTtklCMc9n-97cd45.png)

### HTTPS配置

勾选 **Capture HTTPS CONNECTs、Decrypt HTTPS traffic、Ignore server certificate errors(unsafe)**。

如下：

![img](https://cdn.jsdelivr.net/gh/Killer-89757/PicBed/images/2024%2F05%2FFjtr3HT1G4ECX880Nt-ONhJrntn8-9451e6.png)

**Decrypt HTTPS traffic**中的选项说明：

- **from all processes** ：抓取所有的 https 程序, 包括电脑程序和手机APP。

- **from browsers only** ：只抓取浏览器中的https请求。

- **from non-browsers only** ：只抓取除了浏览器之外的所有https请求。

- **from remote clients only** ：只抓取远程的客户端的https请求，就是只抓取手机APP上的https请求。

配置好之后点击**OK**保存。

弹出对话框“**SCARY TEXT AHEAD：Read Carefully！**”，点击**YES**。

弹出对话框“安全警告”，询问是否安装证书，点击是。

弹出对话框“**Add certificate to the Machine Root List？**”，点击**YES**。

弹出对话框“**TrustCert Success**”，点击确定。

再点击一下**options**中的**ok**，以防忘记保存配置。

**注意事项：**

如果HTTPS请求出问题，例如，浏览器提示“**您的链接不是私密链接**”等，一般都是证书安装有问题，重新安装一遍证书，重复一遍HTTPS配置即可。

**Options——HTTPS——Actions——Trust Root Certificate。**

![img](https://cdn.jsdelivr.net/gh/Killer-89757/PicBed/images/2024%2F05%2FFkqXPWQ95l6399GclIcm8G2ry7ap-91f427.png)![img](https://cdn.jsdelivr.net/gh/Killer-89757/PicBed/images/2024%2F05%2FFmbke7SDwL_0ouxoAyfjvG1s_l-K-9acb89.png)

![img](https://cdn.jsdelivr.net/gh/Killer-89757/PicBed/images/2024%2F05%2FFpUuyrlA1ixA7JZRIYinbBa5SUIQ-8ef875.png)

![img](https://cdn.jsdelivr.net/gh/Killer-89757/PicBed/images/2024%2F05%2FFs1OgEh1uwKR-j61LbyKjo40m8G6-cf380a.png)

### Connections配置

**Fiddler listens on port**，确保**fiddler**的端口为**8888**。(这个端口可以写成自己想要的端口，合理即可)

勾选**Allow remote computers to connect**。

弹出对话框“**Enabling Remote Access**”对话框，点击确定。

![img](https://cdn.jsdelivr.net/gh/Killer-89757/PicBed/images/2024%2F05%2FFgPeBaEKT72pk8gG_oFwaWUPNl_N-179725.png)

![img](https://cdn.jsdelivr.net/gh/Killer-89757/PicBed/images/2024%2F05%2FFrquOSeB4gr_xn-XNIVW7faXR1_1-60d0a5.png)

### fiddler 证书需安装至根证书

没有安装 fidder 根证书会出现的情况：

1. 设置好 fidder 的 options 之后，会发现 fidder 安全证书安装在 “个人” 证书下，未验证安全性，证书提示需要安装在根证书下。
2. 打开 fidder ，浏览器访问 [https://www.baidu.com](https://www.baidu.com/) 网址时，提示 “你的连接不是私密连接”，结果无法访问。
3. 可以成功访问百度网址，但是浏览器下载软件发现迟迟连接不上，无法下载。

![img](https://cdn.jsdelivr.net/gh/Killer-89757/PicBed/images/2024%2F05%2FFsGgckywVDZz6W-o9DNM168wwndz-41c38e.png)

![img](https://cdn.jsdelivr.net/gh/Killer-89757/PicBed/images/2024%2F05%2FFnAAHONafBWmQ-eeqHKSfZBumZtb-72048f.png)

**安装 fiddler 根证书步骤：**

1. 打开 fiddler --> tool --> Options --> HTTPS
2. 勾选：Check for certificate revocation
3. 点击右边的按钮：Actions
4. 信任根证书，单击选择：Trust Root Certificate
5. 出现警告弹窗，均选择 yes
6. 回到Https的页面，最后再 OK ，重启一下 fiddler 就可以了。
7. 如果重启 fiddler 后，打开浏览器网址依旧连接失败：那就重置证书，再次信任根证书，保存后，关闭 fiddler 和浏览器，关闭计算机，重启计算机后再操作。
8. PC 端浏览器访问代理服务器成功，可以抓取浏览器的 http 和 https 的请求了。

![img](https://cdn.jsdelivr.net/gh/Killer-89757/PicBed/images/2024%2F05%2FFuaBbmWZTJlGCcBmdDkAYoRewX4V-3e9bd6.png)

![img](https://cdn.jsdelivr.net/gh/Killer-89757/PicBed/images/2024%2F05%2FFsnAGRCdrngFL1kwKE1bAEWaNhur-6afeec.png)

![img](https://cdn.jsdelivr.net/gh/Killer-89757/PicBed/images/2024%2F05%2FFmSxYAx4iIEhx1xs_7uS1IkiscM--60e37e.png)

![img](https://cdn.jsdelivr.net/gh/Killer-89757/PicBed/images/2024%2F05%2FFmSxYAx4iIEhx1xs_7uS1IkiscM--f6ea81.png)

![img](https://cdn.jsdelivr.net/gh/Killer-89757/PicBed/images/2024%2F05%2FFi9bPI6p1qxLwTKbUOWm8pZPelOW-08bc35.png)

![img](https://cdn.jsdelivr.net/gh/Killer-89757/PicBed/images/2024%2F05%2FFrKvYUFJTFyqgcOvt4iZ6dU1vG7I-d4ab64.png)

![img](https://cdn.jsdelivr.net/gh/Killer-89757/PicBed/images/2024%2F05%2FFntbRb2_JkPn2-x8X_uMRpxXkqup-278fb5.png)

## 三、APP抓包时的手机代理设置

### 1. 环境准备

**让手机和 PC 在同一个局域网下面：**

1. 如果 PC 是笔记本，让 iOS 或 Android 手机、iPhone 或笔记本它们连接同一个 wifi 网络即可。
2. 如果 PC 是网线连接的台式电脑，则在这个局域网下找到一个 WiFi ：
3. 让 iOS 或 Android 手机、iPhone ，连接此 WiFi ，开启代理设置，而 IP 则设置本机 IP 地址。

**PC 电脑本机 IP 的确定方法：**

1. 打开 cmd 窗口，输入命令：ipconfig ，IPv4 地址就是本机 IP 地址。
2. 点击 [fidder.exe](http://fidder.exe/) 文件打开 fidder ，根据 fidder 的 Online 菜单，可以找到本机 IP 地址。

![img](https://cdn.jsdelivr.net/gh/Killer-89757/PicBed/images/2024%2F05%2FFtKNt1BXztP3f15Z7HCKJDDiDYUW-2e6d76.png)![img](https://cdn.jsdelivr.net/gh/Killer-89757/PicBed/images/2024%2F05%2FFoqoKYL8Ybr41MVMx8cZx1KX-nuK-c995ad.png)

### 2. 手机代理设置

1. 先点击 [fiddler.exe](http://fiddler.exe/) 文件打开 fiddler ，目前已设置好一打开 fiddler ，就表示已经成功打开PC 电脑的代理服务器。

2.  手机：设置 → WLAN → 找到同一局域网的 WiFi  → 修改网络 

3.  WiFi 代理设置：输入正确的 WiFi 密码 → 勾选 “显示高级选项” → 代理选择 “手动” 

   - 服务器主机名设置为 PC 本机 IP

   - 服务器端口 8888（这个端口设置在：fidder → Options → Connections →  Fiddler listens on port）

   - 点击 “连接” 保存此代理服务器连接设置。

4. 已设置手机代理服务器成功。

![img](https://cdn.jsdelivr.net/gh/Killer-89757/PicBed/images/2024%2F05%2FFlE7Rb7Ead-UPgh_eSbeT9CchGzB-fad472.png)

![img](https://cdn.jsdelivr.net/gh/Killer-89757/PicBed/images/2024%2F05%2FFhGFWDTVjqXweXy8KZ8dfandIWlm-393504.png)

### 3. 手机 fiddler 证书安装

**手机安装 fiddler 证书步骤：**

1. 手机设置代理，同时设置手机锁屏密码。
2. 手机浏览器，地址栏输入 fiddler 右上方的 IP 地址和端口： [http://IP:8888](http://ip:8888/) 
3. 点击页面里面的：FiddlerRoot certificate 
4. 下载 fidder 证书，记住证书的下载路径
5. 手机：设置 → 高级设置 → 安全 → 从SD卡安装 → 内部存储空间 → 下载路径 → 点击下载的证书
6. 点击证书安装 → 自定义证书名字（例如：fidder_该证书的IP：端口） → 点击 “确定” ，安装证书。
7. 已设置成功，可以开始抓取手机 http 和 https 请求了。

![img](https://cdn.jsdelivr.net/gh/Killer-89757/PicBed/images/2024%2F05%2FFguv0N8KQOYCIxPi2580RE9W46BL-beeb56.png)

![img](https://cdn.jsdelivr.net/gh/Killer-89757/PicBed/images/2024%2F05%2FFvNV5qb42EVno3daCuW8bkrXckUA-8b407f.png)

![img](https://cdn.jsdelivr.net/gh/Killer-89757/PicBed/images/2024%2F05%2FFrBvxVuV0R4UrPuecnES_IYGm1lO-4bae0c.png)



## 四、解决fiddler自动关闭

人行征信密码控件会导致fiddler经常自动停止，并提示：

![img](https://cdn.jsdelivr.net/gh/Killer-89757/PicBed/images/2024%2F05%2FFs0UsiH5OT_lfszMEfxJD-2qG840-b68571.png)

在控制面板，卸载人行征信安全控件。删除C:\Windows\Prefetch路径下PBCCR开头的.pf文件。


![img](https://cdn.jsdelivr.net/gh/Killer-89757/PicBed/images/2024%2F05%2FFgkKg-0Y53ve2zZNYYVgzPx_A1Nu-38b6e2.png)

删除C:\Windows\SysWOW64下面的PBCCRCNew文件夹。重新启动[Fiddler.exe](http://fiddler.exe/)。