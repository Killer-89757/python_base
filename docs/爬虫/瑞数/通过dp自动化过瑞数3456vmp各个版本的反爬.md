# 通过dp自动化过瑞数3/4/5/6/vmp各个版本的反爬【视频+代码】

**视频讲解：**

1、瑞数-如何区分是不是瑞数反爬，以及如何区分是瑞数反爬的哪个版本 https://t.zsxq.com/19yl2diwe  

2、瑞数-通过监听数据包的方式过瑞数vmp反爬 https://t.zsxq.com/19uZYXyWH

3、瑞数-通过刷新cookie+走反爬接口的方式过瑞数反爬 https://t.zsxq.com/19hWYyUox 

4、瑞数-dp过瑞数6代/5代/4代/3代反爬视频演示  https://t.zsxq.com/19ZxwSIvt 、

5、瑞数-在**linux**服务器下**无头**浏览器模式相关代码见文章末尾

**相关代码1-监听抓包，仅学习交流使用**

```python
# 案例10-1 瑞数vmp版本 渲染的方式（既翻页又拿元素标签），监听抓包的方式（只翻页）， 接口的方式（只获取cookie）

from DrissionPage import WebPage, ChromiumOptions
from lxml import etree
co = ChromiumOptions().set_paths(browser_path=r"C:\Program Files (x86)\Microsoft\Edge\Application\msedge.exe")
page = WebPage('d', chromium_options=co)
print("当前页面对象模式11", page.mode)
page.listen.start('fice/jsp/zdsswfaj/wwquery')  # 默认不启动正则匹配，这里代表url包含该字符串，启动正则匹配需要配置 is_regex=True
page.get('http://beijing.chinatax.gov.cn/bjsat/office/jsp/zdsswfaj/wwquery.jsp', retry=3, interval=2, timeout=15)   # 访问网页
page.ele('text=东城').click()
print(page.ele('text:项查询结果').text.strip().rstrip('页').strip())
for packet in page.listen.steps():
    # 解析文本数据
    if packet.method == 'POST':
        res_text = packet.response.body
        al_res = etree.HTML(res_text)
        print(packet.method, packet.request.postData, packet.url)
        for tr in al_res.xpath("//tr"):
            tds = [td.strip() for td in tr.xpath(".//td/text()")]
            print(tds)
        cur_page = page.ele('text:项查询结果').text.strip().split("/")[0][-1]
        print(f"当前是第 {page.ele('text:项查询结果').text.strip().rstrip('页').strip()}")
        page('text=下一页').click()  # 点击下一页
        if cur_page == '3':
            break
```

**相关代码2-刷新cookie+走接口，仅学习交流使用**

```python
# 案例10-2 瑞数vmp版本 接口的方式（只获取cookie）
from DrissionPage import WebPage, ChromiumPage, ChromiumOptions
import requests
from lxml import etree
co = ChromiumOptions().set_paths(browser_path=r"C:\Program Files (x86)\Microsoft\Edge\Application\msedge.exe")
co.set_load_mode('none')
page = WebPage('d', chromium_options=co)
page.get('http://beijing.chinatax.gov.cn/bjsat/office/jsp/zdsswfaj/wwquery.jsp', retry=3, interval=2, timeout=15)   # 访问网页
print('>>>当前cookie', page.cookies(as_dict=True))
browser_cookies = page.cookies(as_dict=True)
print('>>>VIP9lLgDcAL2T', browser_cookies['VIP9lLgDcAL2T'])
# # page.refresh()
# # browser_cookies = page.cookies(as_dict=True)
# # print('>>>VIP9lLgDcAL2T', browser_cookies['VIP9lLgDcAL2T'])

# 不切换模式，直接page.post 配合page.refresh()

sss = time.time()
for c_page in range(1, 6):
    _post_data = {"orgCode": "11100000000", "bz": "dq", "dq": "东城", 'dqy': str(c_page)}
    for i in range(3):
        page.post("http://beijing.chinatax.gov.cn/bjsat/office/jsp/zdsswfaj/wwquery", data=_post_data, retry=0)
        r = page.response
        print(f"当前页面{c_page} res响应状态码", r.status_code)
        if r.status_code != 200:
            # print(f"切换到{page.mode}模式，刷新网页获取cookie")
            page.refresh()
            # page.cookies_to_session()
            # print(f"切换到{page.mode}模式，继续接口请求")
        else:
            al_res = etree.HTML(r.text)
            for tr in al_res.xpath("//tr"):
                tds = [td.strip() for td in tr.xpath(".//td/text()")]
                print(tds)
            break
print(time.time() -sss)


# # 通过requests的方式
# sss = time.time()
# url = "http://beijing.chinatax.gov.cn/bjsat/office/jsp/zdsswfaj/wwquery"
# for c_page in range(1, 6):
#     _post_data = {"orgCode": "11100000000", "bz": "dq", "dq": "东城", 'dqy': str(c_page)}
#     headers = {
#         'user-agent': page.user_agent,
#         'cookie': f"VIP9lLgDcAL2S={browser_cookies['VIP9lLgDcAL2S']}; VIP9lLgDcAL2T={browser_cookies['VIP9lLgDcAL2T']}",
#         'Content-Type': 'application/x-www-form-urlencoded'
#     }
#     # res = requests.post(url, headers=headers, data=_post_data, timeout=10)
#     # print(f"当前页面{c_page} res响应状态码", res.status_code)
#     for i in range(3):
#         res = requests.post(url, headers=headers, data=_post_data, timeout=10)
#         print(f"当前页面{c_page} res响应状态码", res.status_code)
#         if res.status_code != 200:
#             page.refresh()
#             browser_cookies = page.cookies(as_dict=True)
#             print('VIP9lLgDcAL2T', browser_cookies['VIP9lLgDcAL2T'])
#             headers.update({'cookie': f"VIP9lLgDcAL2S={browser_cookies['VIP9lLgDcAL2S']}; VIP9lLgDcAL2T={browser_cookies['VIP9lLgDcAL2T']}"})
#             continue
#         else:
#             break
#     al_res = etree.HTML(res.text)
#     for tr in al_res.xpath("//tr"):
#         tds = [td.strip() for td in tr.xpath(".//td/text()")]
#         print(tds)
# print(time.time() -sss)

# for i in range(3):
#     res = requests.post(url, headers=headers, data=_post_data, timeout=10)
#     print(f"当前页面{c_page} res响应状态码", res.status_code)
#     if res.status_code != 200:
#         page.refresh()
#         browser_cookies = page.cookies(as_dict=True)
#         print('VIP9lLgDcAL2T', browser_cookies['VIP9lLgDcAL2T'])
#         headers.update({'cookie': f"VIP9lLgDcAL2S={browser_cookies['VIP9lLgDcAL2S']}; VIP9lLgDcAL2T={browser_cookies['VIP9lLgDcAL2T']}"})
#         continue
#     else:
#         break


# # 通过webpage（s）模式替代
# sss = time.time()
# page.change_mode()
# for c_page in range(1, 6):
#     _post_data = {"orgCode": "11100000000", "bz": "dq", "dq": "东城", 'dqy': str(c_page)}
#     for i in range(3):
#         page.post("http://beijing.chinatax.gov.cn/bjsat/office/jsp/zdsswfaj/wwquery", data=_post_data)
#         r = page.response
#         print(f"当前页面{c_page} res响应状态码", r.status_code)
#         if r.status_code != 200:
#             page.change_mode()
#             print(f"切换到{page.mode}模式，刷新网页获取cookie")
#             page.refresh()
#             page.change_mode()
#             print(f"切换到{page.mode}模式，继续接口请求")
#         else:
#             break
#     for tr in page.eles('x://tr'):
#         tds = [td.text for td in tr.eles('x://td')]
#         print(tds)
# print(time.time() -sss)
```

**相关代码3-浏览器渲染页面的方式，瑞数vmp反爬-仅学习交流使用**

```python
from DrissionPage import ChromiumPage, ChromiumOptions
from lxml import etree
co = ChromiumOptions().set_paths(browser_path=r"C:\Program Files (x86)\Microsoft\Edge\Application\msedge.exe")
page = ChromiumPage(co)
page.get('http://beijing.chinatax.gov.cn/bjsat/office/jsp/zdsswfaj/wwquery.jsp', retry=3, interval=2, timeout=15)   # 访问网页
page.ele('text=东城').click()
page.wait(2, 3)
print("北京洪瑞厚通贸易有限公司" in page.html)  # False
print("iframe", "北京洪瑞厚通贸易有限公司" in page.get_frame('x://table//table//iframe').html)  # True
print("iframe", ["北京洪瑞厚通贸易有限公司" in iframe.html for iframe in page.get_frames('t:iframe')])  # True
iframe = page.get_frame('x://table//table//iframe')
for tr in iframe.eles("x://tr"):
    tds = [td.text for td in tr.eles('x://td')]
    print(tds)
```

**相关代码4-监听数据包的方式，瑞数6代反爬-仅学习交流使用**

```python
# 案例11 瑞数6代版本  渲染的方式（既翻页又拿元素标签），监听抓包的方式（只翻页）， 接口的方式（只获取cookie）
from DrissionPage import WebPage, ChromiumOptions
co = ChromiumOptions().set_paths(browser_path=r"C:\Program Files (x86)\Microsoft\Edge\Application\msedge.exe")
page = WebPage('d', chromium_options=co)
page.listen.start('pi/internet/event/homePage/list?AfbF5f')
page.get('https://www.urbtix.hk/', retry=3, interval=2, timeout=15)   # 访问网页
for packet in page.listen.steps():
    res_json = packet.response.body
    print(packet.method, packet.request.postData, packet.url)
    for row in res_json['data']:
        print("文本数据", row)
    break
```

**相关代码5-渲染页面的方式，瑞数5代反爬-仅学习交流使用**

```python
# 案例12 瑞数5代 渲染页面的方式
from DrissionPage import WebPage, ChromiumOptions
co = ChromiumOptions().set_paths(browser_path=r"C:\Program Files (x86)\Microsoft\Edge\Application\msedge.exe")
page = WebPage('d', chromium_options=co)
page.get('http://www.bankofdl.com/home/pc/gywm/cggg/list.shtml', retry=3, interval=2, timeout=15)   # 访问网页
for tag_li in page.eles('x: //div[@class="sell_list_rgt"]//li'):
    title = tag_li.ele('x:./a').attr('title')
    href = tag_li.ele('x:./a').attr('href')
    date = tag_li.ele('x:./i').text
    print(f"date:{date} ，title: {title} ,  href {href}")
```

**相关代码6-渲染页面的方式，瑞数4代反爬-仅学习交流使用**

```python
from DrissionPage import WebPage, ChromiumOptions
co = ChromiumOptions().set_paths(browser_path=r"C:\Program Files (x86)\Microsoft\Edge\Application\msedge.exe")
page = WebPage('d', chromium_options=co)
page.get('http://www.fangdi.com.cn/new_house/new_house_list.html', retry=3, interval=2, timeout=15)   # 访问网页
max_page = page.ele('x://span[@class="page_total"]').text.lstrip('共').rstrip('页')
for p in range(int(max_page)):
    cur_page = page.ele('x://span[@class="page_current"]').text
    print(f"当前是多少页 {cur_page}/{max_page}")
    for tr in page.eles('x://div[@class="rent_table"]//tr')[1:]:
        tds = [td.text.strip() for td in tr.eles('x://td')]
        print(tds)
    page.ele('下一页').click()
```

**相关代码7-监听抓包的方式，瑞数3代反爬-仅学习交流使用**

```python
from DrissionPage import ChromiumPage, ChromiumOptions

co = ChromiumOptions().set_paths(browser_path=r"C:\Program Files (x86)\Microsoft\Edge\Application\msedge.exe") # 默认情况下，程序使用 9222 端口 浏览器可执行文件路径为'chrome'
page = ChromiumPage(co)  # 创建对象
page.listen.start('/xxgk/getPostMarketList')  # 默认不启动正则匹配，这里代表url包含该字符串，启动正则匹配需要配置 is_regex=True
page.get('https://www.cde.org.cn/main/xxgk/listpage/b40868b5e21c038a6aa8b4319d21b07d', retry=3, interval=2, timeout=15)   # 访问网页
total_counts = int(page.ele('x://span[@class="layui-laypage-count"]').text.lstrip("共").rstrip("条").strip())
max_page = math.ceil(total_counts/10)
print(f"最大页{max_page} , 共{total_counts}条数据")
for packet in page.listen.steps():
    res_json = packet.response.body
    cur_page = page.ele('x://span[@class="layui-laypage-curr"]').text
    print(f"当前是第 {cur_page}/{max_page} 页", res_json['data']['records'])
    for row in res_json['data']['records']:
        print("文本数据", row)
    page('text=下一页').click()  # 点击下一页
    if cur_page == '3':
        break
```

**相关代码8-linux服务器下，采用无头浏览器模式过瑞数反爬**

**① 先安装浏览器**

- cd /opt

- yum install https://dl.google.com/linux/direct/google-chrome-stable_current_x86_64.rpm

- google-chrome --version

**② 然后运行如下代码**

```python
from DrissionPage import ChromiumPage, ChromiumOptions
from loguru import logger
import platform

if platform.system().lower() == 'windows':
    co = ChromiumOptions().set_paths(browser_path=r"C:\Program Files (x86)\Microsoft\Edge\Application\msedge.exe")
else:
    co = ChromiumOptions().set_paths(browser_path=r"/opt/google/chrome/google-chrome")
    co.set_local_port(9211)
    co.set_user_agent(user_agent='Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/123.0.0.0 Safari/537.36')  # 设置ua
    co.headless(True)   # 设置无头加载  无头模式是一种在浏览器没有界面的情况下运行的模式，它可以提高浏览器的性能和加载速度
    co.incognito(True)  # 无痕隐身模式打开的话，不会记住你的网站账号密码的
    # co.set_argument('--guest')  # 设置访客模式，不会记住你的网站账号密码的等cookie
    co.set_argument('--no-sandbox')  # 禁用沙箱 禁用沙箱可以避免浏览器在加载页面时进行安全检查,从而提高加载速度 默认情况下，所有Chrome 用户都启用了隐私沙盒选项  https://zhuanlan.zhihu.com/p/475639754
    co.set_argument("--disable-gpu")  # 禁用GPU加速可以避免浏览器在加载页面时使用过多的计算资源，从而提高加载速度

# 创建浏览器对象
browser = ChromiumPage(co)  # 创建对象
browser.get("https://www.itjuzi.com/ipo", retry=3, interval=2, timeout=15)   # 访问网
detail_links_all = []
for tr in browser.eles("css:.el-table__row"):
    tds = [td.text.strip() for td in tr.eles("x:.//td")[1:]]
    company = tr.ele("tag:a").text
    a_href = tr.ele("tag:a").attr("href")
    detail_links_all.append(a_href)
    logger.info(f"list_page_company is {company} , a_href is {a_href}")
logger.success(f">>>>>total_detail_urls is : {len(detail_links_all)}")
browser.quit()
```

新发现

chrome浏览器启动是400，edge是200，实则是谷歌浏览器是104版本的问题，更新成最新的就没问题了

![img](https://cdn.jsdelivr.net/gh/Killer-89757/PicBed/images/2024%2F05%2FFoQpn9t2tRs8WCWRu-DZp95WHy0r-1bb293.png)

![img](https://cdn.jsdelivr.net/gh/Killer-89757/PicBed/images/2024%2F05%2FFk4mtKPs4H49unRWYkPllMCi0tZh-1a62af.png)



```python
from DrissionPage import ChromiumPage, ChromiumOptions


# co = ChromiumOptions().set_paths(browser_path=r"C:\Program Files (x86)\Microsoft\Edge\Application\msedge.exe")
co = ChromiumOptions()
co.auto_port()
co.headless(True)   # 设置无头加载  无头模式是一种在浏览器没有界面的情况下运行的模式，它可以提高浏览器的性能和加载速度
co.incognito(True)  # 无痕隐身模式打开的话，不会记住你的网站账号密码的
# co.set_argument('--guest')  # 设置访客模式，不会记住你的网站账号密码的等cookie
co.set_argument('--no-sandbox')  # 禁用沙箱 禁用沙箱可以避免浏览器在加载页面时进行安全检查,从而提高加载速度 默认情况下，所有Chrome 用户都启用了隐私沙盒选项  https://zhuanlan.zhihu.com/p/475639754
co.set_argument("--disable-gpu")  # 禁用GPU加速可以避免浏览器在加载页面时使用过多的计算资源，从而提高加载速度

# 创建浏览器对象
page = ChromiumPage(co)  # 创建对象
print("当前_user_agent", page.user_agent)
page.set.user_agent(page.user_agent.replace('Headless', ''))
print("之后_user_agent", page.user_agent)

page.listen.start('zwgk_cxgh_jzfatzgg.shtml')  # 默认不启动正则匹配，这里代表url包含该字符串，启动正则匹配需要配置 is_regex=True
page.get("http://mpnr.chengdu.gov.cn/ghhzrzyj/jzfatzgg/zwgk_cxgh_jzfatzgg.shtml", retry=3, interval=2, timeout=15)   # 访问网

for data_packet in page.listen.steps(2):
    print("\n=======================================================\n")
    print(">>>>数据包请求网址    ", data_packet.method, data_packet.url)
    print(">>>>响应头状态码", data_packet.response.status)
    print(">>>>响应头    ", data_packet.response.extra_info.all_info['headers'])
    print(">>>>响应头response-cookie", data_packet.response.extra_info.all_info['headers'].get('Set-Cookie'))
    print(">>>>请求头headers", data_packet.request.extra_info.all_info['headers'])
    print(">>>>请求头request-cookie", data_packet.request.extra_info.all_info['headers'].get('Cookie'))
page.quit()
```

