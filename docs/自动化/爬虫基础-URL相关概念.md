# 爬虫基础-URL相关概念

**知识点**：URL（Uniform Resource Locator 统一资源定位符）

**思考**：往浏览器中输入URL到获取网页内容之间都发生了什么

---

1. 日常中，我们在浏览器输入网址敲下回车跳转到某个页面，这个网址叫URL

![img](https://cdn.jsdelivr.net/gh/Killer-89757/PicBed/images/2024%2F05%2FFoF9njSvpn78YMyJJunxzj-tDqWQ-bccd56.png)

2. 一般URL的组成结构包含协议/域名/端口号/资源路径/参数等，http默认端口号80，https默认端口号443，端口号默认隐藏不展示

![img](https://cdn.jsdelivr.net/gh/Killer-89757/PicBed/images/2024%2F05%2FFt392pzSZo4iLOKzd8T9xJmDlOiE-158c2d.png)

3. 一般来说我们输入给浏览器的都是易记的域名比如baidu.com，实际上中间流程会由DNS域名解析成具体的ip地址来定位计算机资源的位置，这里简单了解下即可

![img](https://cdn.jsdelivr.net/gh/Killer-89757/PicBed/images/2024%2F05%2FFkat8KMsyG7JC6NaCddENXvXKwF_-a0aba4.png)

4. 回到URL上，完整的组成结构如下，问号之前是路径，问号之后一般是查询的内容以&号分割

![img](https://cdn.jsdelivr.net/gh/Killer-89757/PicBed/images/2024%2F05%2FFkaTB35DzosiTZCBqqTnPDMB-khn-6c248f.png)

5. 协议：常用的协议有http/https/ftp等，也被称之为protocol，指定url以什么协议发送请求

![img](https://cdn.jsdelivr.net/gh/Killer-89757/PicBed/images/2024%2F05%2FFnShfUjfQmDIegLMYILV-dy8DUpN-0102f5.png)

6. 地址：常以域名（baidu.com）/ip地址（183.60.82.98）/主机名（localhost）来展现，用来确定URL所要访问的服务器地址

![img](https://cdn.jsdelivr.net/gh/Killer-89757/PicBed/images/2024%2F05%2FFnxAMQVwMeMIR9svqZsh4iqhMysN-39365f.png)

7. 域名：域名分一级域名、二级域名、以及顶级域名

![img](https://cdn.jsdelivr.net/gh/Killer-89757/PicBed/images/2024%2F05%2FFuHy7kRcDn2kh5M6H9BpP7I5gQbF-f855cf.png)

8. 问号之前的是路径，问号之后的是查询的参数，常常以&号间隔

![img](https://cdn.jsdelivr.net/gh/Killer-89757/PicBed/images/2024%2F05%2FFgLcLgs3BsltwLSGm5n15AjfqcbS-d5ae1c.png)

9. 回到开始的问题：往浏览器中输入URL到获取网页内容之间都发生了什么，我这里简单的概括下
   - 输入url后
   - dns服务器解析域名出ip地址
   - 浏览器通过ip地址与服务器建立tcp连接，并向服务器发送http请求
   - 服务器接受到请求进行处理，并响应返回html内容
   - 浏览器渲染html内容展示给我们看

10. 推荐文章阅读
    - 一文搞懂URL https://mp.weixin.qq.com/s/YU-2EM6eysYePifaZS4yqA
    - 从输入URL到浏览器显示页面发生了什么 https://mp.weixin.qq.com/s/tzxR1YsWFqVzAc8JMFmgZQ
    - 在浏览器输入URL回车之后发生了什么 https://mp.weixin.qq.com/s/aB6vQ0AmE_bmPZnD_5K59Q
    - 从输入URL到页面展示，这中间发生了什么 https://mp.weixin.qq.com/s/Nf0jp5QqSEFvs2gSPazZ4Q