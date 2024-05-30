# dp自动化实战案例p2~p19所有视频相关代码

```python
"""
b站up ： 时一十一姐呀
公众号： 逆向OneByOne
日期  ： 2024-03-23
b站视频地址： https://space.bilibili.com/308704191/channel/collectiondetail?sid=1947582
官方使用文档：https://drissionpage.cn/
drissionpage是什么：似乎可取代selenium和requests的，可以操作浏览器自动化爬取数据
操作系统：Windows、Linux 或 Mac 支持浏览器
支持浏览器：Chromium 内核（如 Chrome 和 Edge）
如何看chrome/edge路径，在浏览器打开： chrome://version/  edge://version/  taskkill /f /im msedge.exe
如何安装启动 pip install DrissionPage
    https://g1879.gitee.io/drissionpagedocs/get_start/installation
    https://g1879.gitee.io/drissionpagedocs/get_start/before_start
    https://g1879.gitee.io/drissionpagedocs/ChromiumPage/create_page_obj

'connecting'： 网页连接中
'loading'：表示文档还在加载中
'interactive'：DOM 已加载，但资源未加载完成
'complete'：所有内容已完成加载
"""
```

### p2：drissionpage的安装与首次打开网页测试使用 

视频地址：[https://www.bilibili.com/video/BV1Xj421R7dk/](https://www.bilibili.com/video/BV1Xj421R7dk)

```python
from DrissionPage import ChromiumPage, ChromiumOptions

co = ChromiumOptions().set_paths(browser_path=r"C:\Program Files (x86)\Microsoft\Edge\Application\msedge.exe") # 默认情况下，程序使用 9222 端口 浏览器可执行文件路径为'chrome' , 这里的ChromiumOptions即修改一些配置，比如改成edge浏览器执行
page = ChromiumPage(co)  # 创建对象
page.get('http://g1879.gitee.io/DrissionPageDocs', retry=3, interval=2, timeout=15)
```

### p3：drissionpage获取html/text/attr属性的使用 

视频地址：[https://www.bilibili.com/video/BV1Z1421Q7Co/](https://www.bilibili.com/video/BV1Z1421Q7Co)

```python
# 案例1 熟悉.ele .html / .text  / .attr('href')
from DrissionPage import ChromiumPage, ChromiumOptions
co = ChromiumOptions().set_paths(browser_path=r"C:\Program Files (x86)\Microsoft\Edge\Application\msedge.exe") # 默认情况下，程序使用 9222 端口 浏览器可执行文件路径为'chrome'
page = ChromiumPage(co)  # 创建对象
page.get('http://g1879.gitee.io/DrissionPageDocs', retry=3, interval=2, timeout=15)  # 访问网页
print(f">>>>>>>>>>>>>>>>>>>>>>>>\n当前对象控制的页面地址和端口: {page.address}\n浏览器请求头: {page.user_agent}\n是否正在加载状态: {page.states.is_loading} {page.states.ready_state}")
print(">>>>>>>>>>>>>>>>>>>>>>>>\n当前概述html", page.ele('x://*[@id="️-概述"]').html)
print(">>>>>>>>>>>>>>>>>>>>>>>>\n当前版本信息text", page.ele('x://p[contains(text(),"最新版本")]').text)
print(">>>>>>>>>>>>>>>>>>>>>>>>\ngit链接属性值", page.ele('x://p[contains(text(),"项目地址")]/a').attr('href'))
page.quit()  # 关闭浏览器
```

### p4：drissionpage的方法输入文本input/点击click搜索/获取多个元素eles爬取标题与链接 

视频地址：[https://www.bilibili.com/video/BV1pJ4m177us/](https://www.bilibili.com/video/BV1pJ4m177us)

```python
# 案例2  熟悉 .input .click  .eles .attr
from DrissionPage import ChromiumPage, ChromiumOptions
co = ChromiumOptions().set_paths(browser_path=r"C:\Program Files (x86)\Microsoft\Edge\Application\msedge.exe") # 默认情况下，程序使用 9222 端口 浏览器可执行文件路径为'chrome'
page = ChromiumPage(co)  # 创建对象
page.get('https://www.baidu.com', retry=3, interval=2,timeout=15)
page.ele('x://input[@id="kw"]').input('DrissionPage')  # 输入文本
page.ele('x://input[@id="su"]').click()  # 点击按钮
page.wait.load_start()  # 等待页面跳转
links = page.eles('x://h3')  # 获取所有结果
for link in links:  # 遍历并打印结果
    print("标题", link.text, "链接",link.ele("x:/a").attr('href'))
```

### p5：drissionpage获取登陆后的cookie/page.cookies(as_dict=True)

视频地址：[https://www.bilibili.com/video/BV1pm411k7MW/](https://www.bilibili.com/video/BV1pm411k7MW)

```python
# 案例3 熟悉 登陆 .input .cookies(as_dict=True)
from DrissionPage import ChromiumPage, ChromiumOptions
co = ChromiumOptions().set_paths(browser_path=r"C:\Program Files (x86)\Microsoft\Edge\Application\msedge.exe") # 默认情况下，程序使用 9222 端口 浏览器可执行文件路径为'chrome'
page = ChromiumPage(co)  # 创建对象
page.get('https://gitee.com/login', retry=3, interval=2, timeout=15)  # 跳转到登录页面
if page.ele('x://input[@id="user_login"]'):  # 定位到账号文本框，获取文本框元素
    ele = page.ele('x://input[@id="user_login"]')
    ele.input(input("请输入您的账号"))   # 输入对文本框输入账号
    page.ele('x://input[@id="user_password"]').input(input('请输入您的密码'))  # 定位到密码文本框并输入密码
    page.ele('x://input[@value="登 录"]').click()  # 点击登录按钮
print('获取到cookies', page.cookies(as_dict=True))
```

### p6：drissionpage实现翻页爬取并下载图片img.save()/img.src()

视频地址：[https://www.bilibili.com/video/BV14F4m1F759/](https://www.bilibili.com/video/BV14F4m1F759)

```python
# 案例4 熟悉 翻页 下载图片
from DrissionPage import ChromiumPage, ChromiumOptions
co = ChromiumOptions().set_paths(browser_path=r"C:\Program Files (x86)\Microsoft\Edge\Application\msedge.exe") # 默认情况下，程序使用 9222 端口 浏览器可执行文件路径为'chrome'
page = ChromiumPage(co)  # 创建对象
page.get('https://book.douban.com/tag/小说?start=0&type=T', retry=3, interval=2, timeout=15)
for _ in range(2):  # 爬取2页
    for book in page.eles('x://li[@class="subject-item"]'):  # 遍历一页中所有图书
        book_name = book.ele('x://h2/a').attr('title')   # 获取书名
        img = book('x://img')  # 获取封面图片对象
        img.save(path='./img/', name=f"{book_name}.png")  # 保存图片
        print("图片字节获取  img.src()", book_name, )  # 图片字节获取 img.src()
    # 点击下一页
    page('后页>').click()
    page.wait.load_start()
```

### p7：drissionpage过字符类验证码反爬

视频地址：[https://www.bilibili.com/video/BV1Ur42187Sv/](https://www.bilibili.com/video/BV1Ur42187Sv)

```python
# 案例5  字符类验证码反爬  https://www.bilibili.com/video/BV1F8411q71h/
import ddddocr
from DrissionPage import ChromiumPage, ChromiumOptions
co = ChromiumOptions().set_paths(browser_path=r"C:\Program Files (x86)\Microsoft\Edge\Application\msedge.exe") # 默认情况下，程序使用 9222 端口 浏览器可执行文件路径为'chrome'
page = ChromiumPage(co)  # 创建对象
page.get("https://spxksq.amr.guizhou.gov.cn:9081/TopFDOAS/searchDoc.action", retry=3, interval=2, timeout=15)
page.ele('x://input[@id="nameLicNo"]').input("多彩贵州文化艺术股份有限公司")  # 输入搜索词
for i in range(3):
    # 获取验证码图片字节，ddddocr识别验证码图片字母
    img_bytes = page.ele('x://img[@id="captchaImg"]').src()  # 图片字节获取
    ocr = ddddocr.DdddOcr(show_ad=False)
    yzm = ocr.classification(img_bytes)
    print("识别验证码的结果", yzm)
    # 验证码结果输入进去框验证
    page.ele('x://input[@value="请输入验证码"]').input(yzm)  # 输入验证码
    # 点击查询
    page.ele('x://input[@value="查询"]').click()  # 点击查询
    time.sleep(2)
    if page.ele('x://div[@class="x-nameofcenter"]'):
        print("查询名称", page.ele('x://div[@class="x-table"]/a').text)
        print("查询结果", page.ele('x://div[@class="x-nameofcenter"]').html)
        break
    else:
        print("识别错误")
```

### p8：drissionpage过滑块类验证码反爬actions.hold/move/release

视频地址：[https://www.bilibili.com/video/BV1j1421Q7EM/](https://www.bilibili.com/video/BV1j1421Q7EM)

```python
# 案例6  滑块类验证码反爬 https://www.bilibili.com/video/BV15V411P7Wb/
import random
import time
import ddddocr
from DrissionPage import ChromiumPage, ChromiumOptions
co = ChromiumOptions().set_paths(browser_path=r"C:\Program Files (x86)\Microsoft\Edge\Application\msedge.exe") # 默认情况下，程序使用 9222 端口 浏览器可执行文件路径为'chrome'
page = ChromiumPage(co)  # 创建对象
def get_tracks(distance):
    """滑块的运动轨迹"""
    value = round(random.uniform(0.55, 0.75), 2)
    v, t, sum1 = 0, 0.3, 0
    plus = []
    mid = distance * value
    while sum1 < distance:
        if sum1 < mid:
            a = round(random.uniform(2.5, 3.5), 1)
        else:
            a = -round(random.uniform(2.0, 3.0), 1)
        s = v * t + 0.5 * a * (t ** 2)
        v = v + a * t
        sum1 += s
        plus.append(round(s))
    return plus

page.get("https://cszg.mca.gov.cn/biz/ma/csmh/g/cszzsearch.html?value=社会", retry=3, interval=2, timeout=15)

for i in range(5):
    # 1、获取滑块图片
    background_bytes = page.ele('x://img[@id="oriImg"]').src()  # .save(path="./img/", name='background.png')
    cut_bytes = page.ele('x://img[@id="cutImg"]').src()  # .save(path="./img/", name='target.png')
    # 2、识别滑块缺口并获得滑动轨迹
    det = ddddocr.DdddOcr(det=False, ocr=False, show_ad=False)  # import ddddocr
    result = det.slide_match(cut_bytes, background_bytes, simple_target=True)
    print("滑块距离", result)
    offset = result['target'][0]
    tracks = get_tracks(offset)
    print("滑动轨迹", tracks)
    # 3、滑动滑块
    """模拟滑块滑动 https://g1879.gitee.io/drissionpagedocs/ChromiumPage/actions/#-%E4%BD%BF%E7%94%A8%E5%86%85%E7%BD%AEactions%E5%B1%9E%E6%80%A7"""
    page.actions.hold('x://div[@id="slider"]')  # 此方法用于按住鼠标左键不放，按住前可先移动到元素上
    for track in tracks:  # 使鼠标相对当前位置移动若干距离
        page.actions.move(offset_x=track, offset_y=round(random.uniform(1.0, 3.0), 0), duration=.1)
    time.sleep(0.1)
    page.actions.release('x://div[@id="slider"]')  # 此方法用于释放鼠标左键，释放前可先移动到元素上。
    page.ele('x://div[@id="captchadiv"]').get_screenshot(path='./captcha1.jpg')
    time.sleep(3)
    if "验证" in page.ele('x://div[@class="path_content"]').text:
        print("滑动失败, 刷新滑块")
        page.ele('x://img[@onclick="getSlideCaptcha()"]').click()
        time.sleep(3)
    else:
        print("滑动成功")
        break
for tr in page.eles("x://tr")[1:]:
    tds = [td.text.strip() for td in tr.eles('x://td')]
    print(tds)
```

### p9：drissionpage过点选类验证码反爬

视频地址：[https://www.bilibili.com/video/BV1XC411b7cp/](https://www.bilibili.com/video/BV1XC411b7cp)

```python
# 案例7  点选类验证码反爬 https://www.bilibili.com/video/BV1dN411H7vj/
from DrissionPage import ChromiumPage, ChromiumOptions
import cv2

def click_img(yzm_xy):
    # 鼠标点击图片输出该点像素坐标  pip install opencv-python --upgrade  pip install opencv-contrib-python
    

    # 鼠标点击事件的回调函数
    def mouse_callback(event, x, y, flags, param):
        if event == cv2.EVENT_LBUTTONDOWN:
            cv2.circle(img, (x, y), 3, (0, 0, 255), -1)  # 在图片上画一个圆标记鼠标点击的点
            print(f"鼠标点击处的像素坐标：({x}, {y})")  # 输出鼠标点击处的像素坐标
            yzm_xy.append({"x": x, "y": y})

    # 点击图片并获得坐标
    img = cv2.imread('captcha.jpg')
    cv2.namedWindow('image')  # 创建图片显示窗口
    cv2.setMouseCallback('image', mouse_callback)  # 设置鼠标回调函数
    cv2.imshow('image', img)  # 在窗口中显示图片
    while True:
        cv2.imshow('image', img)  # 在窗口中显示图片
        if cv2.waitKey(1) == 13:  # 按下Enter键退出循环
            break
    cv2.destroyAllWindows()  # 关闭窗口


co = ChromiumOptions().set_paths(browser_path=r"C:\Program Files (x86)\Microsoft\Edge\Application\msedge.exe") # 默认情况下，程序使用 9222 端口 浏览器可执行文件路径为'chrome'
page = ChromiumPage(co)  # 创建对象
# 1、打开网页刷新下
page.get("http://www.ccgp-yunnan.gov.cn/page/procurement/procurementList.html", retry=3, interval=2, timeout=15)
print(f">>>>是否正在加载状态: {page.states.is_loading} {page.states.ready_state}")
page.refresh()
# 2、点击翻页触发点选验证码 # page.ele('x://div[@class="verify-refresh"]').click()
page.wait.ele_displayed('x://a[@data-page="next"]', timeout=15)
page.ele('x://a[@data-page="next"]').click()
page.wait(1, 3)
print("要点击的文字", page.ele('x://span[@class="verify-msg"]').text)
# 3、验证码识别点击
img_obj = page.ele('x://div[@class="verify-img-panel"]/img')
if os.path.exists('./captcha.jpg'):
    os.remove('./captcha.jpg')
img_obj.save('./', name='captcha.jpg')
yzm_xy = list()
click_img(yzm_xy)  # ai训练验证码识别模型，接入打码平台api
print("要点击的坐标是", yzm_xy)
time.sleep(3)
for xy in yzm_xy:
    page.actions.move_to(img_obj, offset_x=int(xy['x']/310*350), offset_y=int(xy['y']/155*175), duration=.1).click()
    time.sleep(2)
# 4、获取网页的数据文本
for tr in page.eles("x://tr")[1:]:
    tds = [td.text.strip() for td in tr.eles('x://td')]
    print(tds)
```

### p10：drissionpage过极验4代语序点选和九宫格反爬 

视频地址：[https://www.bilibili.com/video/BV1cp421m7JR/](https://www.bilibili.com/video/BV1cp421m7JR)

```python
# 案例8 点选与九宫格

from DrissionPage import ChromiumPage, ChromiumOptions

def click_img(yzm_xy):
    # 鼠标点击图片输出该点像素坐标  pip install opencv-python --upgrade  pip install opencv-contrib-python
    import cv2

    # 鼠标点击事件的回调函数
    def mouse_callback(event, x, y, flags, param):
        if event == cv2.EVENT_LBUTTONDOWN:
            cv2.circle(img, (x, y), 3, (0, 0, 255), -1)  # 在图片上画一个圆标记鼠标点击的点
            print(f"鼠标点击处的像素坐标：({x}, {y})")  # 输出鼠标点击处的像素坐标
            yzm_xy.append({"x": x, "y": y})

    # 点击图片并获得坐标
    img = cv2.imread('captcha.jpg')
    cv2.namedWindow('image')  # 创建图片显示窗口
    cv2.setMouseCallback('image', mouse_callback)  # 设置鼠标回调函数
    cv2.imshow('image', img)  # 在窗口中显示图片
    while True:
        cv2.imshow('image', img)  # 在窗口中显示图片
        if cv2.waitKey(1) == 13:  # 按下Enter键退出循环
            break
    cv2.destroyAllWindows()  # 关闭窗口

co = ChromiumOptions().set_paths(browser_path=r"C:\Program Files (x86)\Microsoft\Edge\Application\msedge.exe") # 默认情况下，程序使用 9222 端口 浏览器可执行文件路径为'chrome'
page = ChromiumPage(co)  # 创建对象
# 1、打开网页刷新下
page.get("http://cx.cnca.cn/CertECloud/result/skipResultList", retry=3, interval=2, timeout=15)
print(f">>>>是否正在加载状态: {page.states.is_loading} {page.states.ready_state}")
# page.refresh()
# 2、搜索关键词
page.ele('x://input[@id="orgName"]').input("苏州市")
page.wait(1, 3)
page.ele('x://button[@class="btn btn-primary"]').click()
page.wait(1, 3)
text = page.ele('x://div[contains(@class,"geetest_text_tips")]').text
print("提示", text)
# 3、验证码识别点击
if "请按语序依次点击" in text:
    img_obj = page.ele('x://div[contains(@class,"geetest_bg")]')  # 验证码模型识别坐标/打码平台识别坐标
    img_url = img_obj.attr('style').replace('background-image: url("', '').replace('");', '')
    if os.path.exists('./captcha.jpg'):
        os.remove('./captcha.jpg')
    page.download(img_url, r'./', rename='captcha.jpg')
    yzm_xy = list()
    click_img(yzm_xy)  # 验证码模型识别坐标/打码平台识别坐标
    print("要点击的坐标是", yzm_xy)
    for xy in yzm_xy:
        page.actions.move_to(img_obj, offset_x=int(xy['x']), offset_y=int(xy['y']), duration=.1).click()
        page.wait(1, 3)
    page.ele('x://div[contains(@class,"geetest_submit_tips")]').click()
else:  # "请选择3个符合的图片"
    img_target_url = page.ele('x://div[contains(@class, "geetest_ques_tips")]/img').attr('src')
    print("目标点击的图片是", img_target_url)  # 保存图片/字节流，调用训练验证码模型或者打码平台，传9个图片，去识别目标点击的这个图片
    #  x://div[contains(@class,"geetest_window")]/div[contains(@class,"geetest_item_img")]
    for other_img in page.eles('css:.geetest_window .geetest_item_img'):
        img_url = other_img.attr('style').replace('background-image: url("', '').replace('");', '')
        img_num = other_img.attr('class').split(" ")[0]
        print("要点击的图片是", img_num, img_url)
    # 此处接入打码平台，或者识别模型api
    img_num = input("请输入你要点击的图片序号")
    page.ele(f"css:{img_num}").click()
    img_num = input("请输入你要点击的图片序号")
    page.ele(f"css:{img_num}").click()
    img_num = input("请输入你要点击的图片序号")
    page.ele(f"css:.{img_num}").click()
    # page.ele('x://div[contains(@class,"geetest_submit_tips")]').click()
```

### p11：drissionpage巧妙绕过反爬像fiddler和network一样监听数据包 

视频地址：[https://www.bilibili.com/video/BV1N2421N74c/](https://www.bilibili.com/video/BV1N2421N74c)

```python
# # 案例9 监听与抓包  https://g1879.gitee.io/drissionpagedocs/ChromiumPage/listener/#%EF%B8%8F-datapacket%E5%AF%B9%E8%B1%A1
from DrissionPage import ChromiumPage, ChromiumOptions

co = ChromiumOptions().set_paths(browser_path=r"C:\Program Files (x86)\Microsoft\Edge\Application\msedge.exe")  # 默认情况下，程序使用 9222 端口 浏览器可执行文件路径为'chrome'
page = ChromiumPage(co)  # 创建对象
page.listen.start('detail?nodeId=')  # 默认不启动正则匹配，这里代表url包含该字符串，启动正则匹配需要配置 is_regex=True
page.get('https://ygp.gdzwfw.gov.cn/#/44/new/jygg/v3/A?noticeId=dc240acc-d8a3-48ab-b16a-bad2e64a1ff7&projectCode=E4401000002400710001&bizCode=3C51&siteCode=440100&publishDate=20240302000028&source=%E5%B9%BF%E4%BA%A4%E6%98%93%E6%95%B0%E5%AD%97%E4%BA%A4%E6%98%93%E5%B9%B3%E5%8F%B0&titleDetails=%E5%B7%A5%E7%A8%8B%E5%BB%BA%E8%AE%BE&classify=A02&nodeId=1762040444150657029')  # 访问网址
data_packet = page.listen.wait()
print("-----本标签页id与框架id-----", data_packet.tab_id, data_packet.frameId)
print(">>>>数据包请求网址    ", data_packet.method, data_packet.url)
print(">>>>响应文本    ", data_packet.response.body, data_packet.response.raw_body)
print(">>>>响应头    ", data_packet.response.status, data_packet.response.headers)
print(">>>>请求头信息    ", data_packet.request.headers)
# for key, value in data_packet.request.headers.items():
#     print(f"\t【name】 {key} 【value】 {value}")
print(">>>>请求头表单信息    ", data_packet.request.postData)
print(">>>>连接失败信息    ", data_packet.fail_info.errorText)
```

```python
from DrissionPage import ChromiumPage, ChromiumOptions

co = ChromiumOptions().set_paths(browser_path=r"C:\Program Files (x86)\Microsoft\Edge\Application\msedge.exe")  # 默认情况下，程序使用 9222 端口 浏览器可执行文件路径为'chrome'
page = ChromiumPage(co)  # 创建对象
page.get('https://ygp.gdzwfw.gov.cn/#/44/new/jygg/v3/A?noticeId=dc240acc-d8a3-48ab-b16a-bad2e64a1ff7&projectCode=E4401000002400710001&bizCode=3C51&siteCode=440100&publishDate=20240302000028&source=%E5%B9%BF%E4%BA%A4%E6%98%93%E6%95%B0%E5%AD%97%E4%BA%A4%E6%98%93%E5%B9%B3%E5%8F%B0&titleDetails=%E5%B7%A5%E7%A8%8B%E5%BB%BA%E8%AE%BE&classify=A02&nodeId=1762040444150657029')  # 访问网址
html_shadow_root = page.ele('xpath://div[@class="richtext"]/div').shadow_root
for tr in html_shadow_root.eles("x://tr")[-10:-13]:
    print("这个 ", tr.html)
page.listen.start()
page.get('https://ygp.gdzwfw.gov.cn/#/44/new/jygg/v3/A?noticeId=dc240acc-d8a3-48ab-b16a-bad2e64a1ff7&projectCode=E4401000002400710001&bizCode=3C51&siteCode=440100&publishDate=20240302000028&source=%E5%B9%BF%E4%BA%A4%E6%98%93%E6%95%B0%E5%AD%97%E4%BA%A4%E6%98%93%E5%B9%B3%E5%8F%B0&titleDetails=%E5%B7%A5%E7%A8%8B%E5%BB%BA%E8%AE%BE&classify=A02&nodeId=1762040444150657029')  # 访问网址
for data_packet in page.listen.steps():
    print(">>>>监听的数据包url", data_packet.method, data_packet.url)
    print(">>>>响应头    ", data_packet.response.status, data_packet.response.headers)
```

```python
from DrissionPage import ChromiumPage, ChromiumOptions
co = ChromiumOptions().set_paths(browser_path=r"C:\Program Files (x86)\Microsoft\Edge\Application\msedge.exe") # 默认情况下，程序使用 9222 端口 浏览器可执行文件路径为'chrome'
page = ChromiumPage(co)  # 创建对象
page.set.cookies.clear()  # 清掉缓存
page.listen.start('office/jsp/zdsswfaj/wwquery.jsp')  # 默认不启动正则匹配，这里代表url包含该字符串，启动正则匹配需要配置 is_regex=True
page.get('http://beijing.chinatax.gov.cn/bjsat/office/jsp/zdsswfaj/wwquery.jsp')  # 访问网址
for data_packet in page.listen.steps(count=2):
    print(">>>>数据包请求网址    ", data_packet.method, data_packet.url)
    print(">>>>响应头状态码", data_packet.response.status)
    print(">>>>响应头    ", data_packet.response.headers)
    print(">>>>响应头cookie", data_packet.response.extra_info.all_info['headers'].get('Set-Cookie'))
```

```python
# 导入库
from DrissionPage import ChromiumPage,ChromiumOptions
# 创建配置对象
co = ChromiumOptions().set_paths(browser_path=r"C:\Program Files (x86)\Microsoft\Edge\Application\msedge.exe")
# 启动配置
co.set_local_port(7878)
co.ignore_certificate_errors(True)
# 创建浏览器
page = ChromiumPage(co)
# 创建标签页
tab = page.new_tab()
tab.listen.start('.mp3')
# 打开网址
tab.get('https://www.kugou.com/mixsong/a87op8d9.html')
# 开始监听
for data_packet in tab.listen.steps(count=1):
    song_url = data_packet.url
    print(song_url)
# 下载音乐 , 这里要稍等个几秒
tab.download(song_url, rename=tab.title)
```

```python
from DrissionPage import ChromiumPage,ChromiumOptions
co = ChromiumOptions().set_paths(browser_path=r"C:\Program Files (x86)\Microsoft\Edge\Application\msedge.exe")
page = ChromiumPage(co)
page.listen.start(targets=['https://e.oppomobile.com/captcha/api/a?w=', 'https://e.oppomobile.com/captcha/api/p1?sid=', 'https://e.oppomobile.com/captcha/api/p2?sid='])
page.get('https://e.oppomobile.com/market/login/index.html?captcha/api/p1?sid=99c9ca33aa03c4d39694a66ff0b1b7b5&aid=dx-1712718013015-49102898-1&ak=43768f2ab87180b2cbe718f62d4bc5fa&type=0&c=6614b7e7rBgh0bGEucs0RziIqoSfxrjVB1B8Fdv1&_r=0.7676811371377876')
responses = page.listen.wait(3)
for response in responses:
    print(response.url,response.target,response.response.body)
```

### p12：瑞数-通过监听数据包的方式过瑞数vmp反爬

视频地址：[https://www.bilibili.com/video/BV1KD421j7ss/](https://www.bilibili.com/video/BV1KD421j7ss)



### p13：drissionpage刷新cookie绕过瑞数vmp反爬走接口获取 

视频地址：[https://www.bilibili.com/video/BV1Gq421A7sa/](https://www.bilibili.com/video/BV1Gq421A7sa)



### p14：drissionpage过瑞数反爬6代/5/4/3代

视频地址：[https://www.bilibili.com/video/BV1Pm411r7n7/](https://www.bilibili.com/video/BV1Pm411r7n7)



### p15：drissionpage多线程并发操作标签页/浏览器并发提高速度 

视频地址：[https://www.bilibili.com/video/BV1QZ421v7Mw/](https://www.bilibili.com/video/BV1QZ421v7Mw)

```python
# 第一步学会DataRecorder写入excel  https://g1879.gitee.io/datarecorderdocs/installation_and_import/
from DataRecorder import Recorder
r = Recorder(path=r"D:/Sy/company.xlsx", cache_size=500)

# list格式
r.add_data(['康居人', 'https://www.itjuzi.com/company/43017067', '医疗健康'])
r.add_data([['灿芯股份', 'https://www.itjuzi.com/company/32160445', '先进制造'], ['张三的公司', 'https://www.company/43017067', '医康']])

# dict格式
r.add_data([{'公司名': '康居人', '详情链接': 'https://www.itjuzi.com/company/43017067', '行业': '医疗健康'}])
r.add_data([{'公司名': '张三的公司', '详情链接': 2, '行业': 3}, {'公司名': '王二的公司', '详情链接': 5, '行业': 6}])

r.record()
```

```python
# 多线程操作标签页
from threading import Thread

from DrissionPage import ChromiumPage
from DataRecorder import Recorder


def collect(tab, recorder, title):
    """用于采集的方法
    :param tab: ChromiumTab 对象
    :param recorder: Recorder 记录器对象
    :param title: 类别标题
    :return: None
    """
    num = 1  # 当前采集页数
    for i in range(4):
        # 遍历所有标题元素
        for i in tab.eles('.title project-namespace-path'):
            # 获取某页所有库名称，记录到记录器
            print(title, i.text, num)
            recorder.add_data((title, i.text, num))

        # 如果有下一页，点击翻页
        btn = tab('@rel=next', timeout=2)
        if btn:
            btn.click(by_js=True)
            tab.wait.load_start()
            num += 1

        # 否则，采集完毕
        else:
            break


def main():
    # 新建页面对象
    page = ChromiumPage()
    # 第一个标签页访问网址
    page.get('https://gitee.com/explore/ai')
    # 获取第一个标签页对象
    tab1 = page.get_tab()
    # 新建一个标签页并访问另一个网址
    tab2 = page.new_tab('https://gitee.com/explore/machine-learning')
    # 获取第二个标签页对象
    tab2 = page.get_tab(tab2)

    # 新建记录器对象
    recorder = Recorder(r'D:\Sy\company.xlsx')

    # 多线程同时处理多个页面
    Thread(target=collect, args=(tab1, recorder, 'ai')).start()
    Thread(target=collect, args=(tab2, recorder, '机器学习')).start()


if __name__ == '__main__':
    main()
```

```python
from threading import Thread

from DrissionPage import ChromiumPage, ChromiumOptions
from DataRecorder import Recorder


def collect(page, recorder, title):
    """用于采集的方法
    :param page: ChromiumTab 对象
    :param recorder: Recorder 记录器对象
    :param title: 类别标题
    :return: None
    """
    num = 1  # 当前采集页数
    while True:
        # 遍历所有标题元素
        for i in page.eles('.title project-namespace-path'):
            # 获取某页所有库名称，记录到记录器
            recorder.add_data((title, i.text, num))

        # 如果有下一页，点击翻页
        btn = page('@rel=next', timeout=2)
        if btn:
            btn.click(by_js=True)
            page.wait.load_start()
            num += 1

        # 否则，采集完毕
        else:
            break

    recorder.record()  # 把数据记录到文件


def main():
    # 创建配置对象，并设置自动分配端口
    co = ChromiumOptions().auto_port()
    # 新建2个页面对象，自动分配端口的配置对象能共用，但指定端口的不可以
    page1 = ChromiumPage(co)
    page2 = ChromiumPage(co)
    # 第一个浏览器访问第一个网址
    page1.get('https://gitee.com/explore/ai')
    # 第二个浏览器访问另一个网址
    page2.get('https://gitee.com/explore/machine-learning')

    # 新建记录器对象
    recorder = Recorder('data.csv')

    # 多线程同时处理多个页面
    Thread(target=collect, args=(page1, recorder, 'ai')).start()
    Thread(target=collect, args=(page2, recorder, '机器学习')).start()


if __name__ == '__main__':
    main()
```

### p16：drissionpage并发10倍速度爬取详情页

视频地址：[https://www.bilibili.com/video/BV1fA4m1F71a/](https://www.bilibili.com/video/BV1fA4m1F71a)

```python
from DrissionPage import ChromiumPage, ChromiumOptions
from loguru import logger
from concurrent.futures import ThreadPoolExecutor


def detail_tab(d_url):
    tab = page.new_tab(d_url)
    compa = tab.ele("css:.company-header-title").text
    tags = [tag.text for tag in tab.eles("css:.company-tags-box a")]
    logger.success(f">>>>>detail_latest_tab : {compa} , tags: {tags}, tab_url : {tab.url}")
    tab.close()


co = ChromiumOptions().set_paths(browser_path=r"C:\Program Files (x86)\Microsoft\Edge\Application\msedge.exe")
co.set_user_agent(user_agent='Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/123.0.0.0 Safari/537.36')
page = ChromiumPage(co)  # 创建对象
page.get("https://www.itjuzi.com/ipo", retry=3, interval=2, timeout=15)   # 访问网
# 一次性拿到所有详情链接
detail_links_all = []
for tr in page.eles("css:.el-table__row"):
    tds = [td.text.strip() for td in tr.eles("x:.//td")[1:]]
    company = tr.ele("tag:a").text
    a_href = tr.ele("tag:a").attr("href")
    detail_links_all.append(a_href)
    logger.info(f"list_page_company is {company} , a_href is {a_href}")
    # detail_tab(a_href)
logger.success(f">>>>>total_detail_urls is : {len(detail_links_all)}")
# # 单线程标签页操作
# for a_href in detail_links_all:
#     tab = page.new_tab(a_href)
#     # tab = page.latest_tab
#     company = tab.ele("css:.company-header-title").text
#     tags = [tag.text for tag in tab.eles("css:.company-tags-box a")]
#     logger.success(f">>>>>detail_latest_tab : {company} , tags: {tags}, tab_url : {tab.url}")
#     tab.close()


# 多线程标签页操作
with ThreadPoolExecutor(max_workers=10) as tp:
    tp.map(detail_tab, detail_links_all)
```

```python
from DrissionPage import ChromiumPage, ChromiumOptions
# 新建excel表格存储内容
from DataRecorder import Recorder
r = Recorder(path=r"./company.xlsx", cache_size=500)
r.add_data(['公司名', '详情链接', '序号', '地址','行业', '成立时间', '交易所', '上市时间', '募资资金', 'IPO首日市值'])
# 新建page对象打开网页
co = ChromiumOptions().set_paths(browser_path=r"C:\Program Files (x86)\Microsoft\Edge\Application\msedge.exe")
# co.headless(False)
# co.set_user_agent(user_agent='Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/123.0.0.0 Safari/537.36')
page = ChromiumPage(co)  # 创建对象
page.get("https://www.itjuzi.com/ipo", retry=3, interval=2, timeout=15)   # 访问网页
print(page.user_agent)
print("康居人" in page.html)
# 列表页信息存储excel表格
detail_links_all = []
for tr in page.eles("css:.el-table__row"):
    tds = [td.text.strip() for td in tr.eles("x:.//td")[1:]]
    company = tr.ele("tag:a").text
    a_href = tr.ele("tag:a").attr("href")
    tds.insert(0, a_href)
    tds.insert(0, company)
    print(company, a_href, tds)
    detail_links_all.append(a_href)
    r.add_data(tds)
r.record()
```

### p17：drissionpage实现无头浏览器/无痕隐身模式/访客模式/设置ua/设置指定端口 

视频地址：[https://www.bilibili.com/video/BV1oM4m1D7nd/](https://www.bilibili.com/video/BV1oM4m1D7nd)

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

### p18：drissionpage在linux无头模式下过五秒盾Cloudflare

视频地址：[https://www.bilibili.com/video/BV1Dm421x73t/](https://www.bilibili.com/video/BV1Dm421x73t)

```python
# 过五秒盾反爬
from DrissionPage import WebPage, ChromiumOptions
import platform
from loguru import logger

# 1、浏览器配置相关参数
if platform.system().lower() == 'windows':
    co = ChromiumOptions().set_paths(browser_path=r"C:\Program Files (x86)\Microsoft\Edge\Application\msedge.exe")
    value = '确认您是真人'
else:
    co = ChromiumOptions().set_paths(browser_path=r"/opt/google/chrome/google-chrome")
    value = 'Verify you are human'
    co.headless(True)   # 设置无头加载  无头模式是一种在浏览器没有界面的情况下运行的模式，它可以提高浏览器的性能和加载速度
    co.incognito(True)  # 无痕隐身模式打开的话，不会记住你的网站账号密码的
    co.set_argument('--no-sandbox')  # 禁用沙箱 禁用沙箱可以避免浏览器在加载页面时进行安全检查,从而提高加载速度 默认情况下，所有Chrome 用户都启用了隐私沙盒选项  https://zhuanlan.zhihu.com/p/475639754
    co.set_argument("--disable-gpu")  # 禁用GPU加速可以避免浏览器在加载页面时使用过多的计算资源，从而提高加载速度
    co.set_user_agent(user_agent='Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/124.0.0.0 Safari/537.36')  # 设置ua

# 2、打开网页
browser = WebPage('d', chromium_options=co)  # 创建对象
browser.set.window.max()
browser.get("https://cn.airbusan.com/content/common/customercenter/noticeList", retry=3, interval=2, timeout=15)   # 访问网
logger.info(f"user_agent is {browser.user_agent}")
browser.wait(2)

# 3、获取网页页面内容
for i in range(20):
    if browser.ele(f'x://input[@value="{value}"]', timeout=3):
        logger.warning(f"retry {i+1} times, Verify you are human click now")
        browser.ele(f'x://input[@value="{value}"]').click()
        browser.wait(2)
    if not browser.cookies(as_dict=True).get('cf_clearance'):
        logger.error(f"retry {i+1} times, browser_cookie is {browser.cookies(as_dict=True)}")
        continue
    else:
        logger.success(f"retry {i+1} times, browser_cookie is {browser.cookies(as_dict=True)}")
        break
# with open(r"./ccc.html", "w") as f:
#     f.write(browser.html)
browser.wait(2)
browser.wait.ele_displayed('x://td[@class="subject"]/a', timeout=3)
for tr in browser.eles('x://div[@class="boardList mgt60"]//tr', timeout=3)[1:]:
    tds = [td.text for td in tr.eles("x://td", timeout=3)]
    detail_url = tr.ele('x://td[@class="subject"]/a').attr('href')
    logger.info(f"list_page_company is {tds} , a_href is {detail_url}")
# 4、对当前整页截图并保存
browser.get_screenshot(path=r'./headless.png', full_page=True)
browser.quit()
```

```python
# 过五秒盾下载图片
from DrissionPage import WebPage

dp = WebPage()
dp.listen.start('/202312121434/224ecapcarmine-1.jp', method='GET')
dp.get('https://static.galerieslafayette.com/media/images/hp_mod_569/hp_mod_56989832/hp_modvar_104710498/202312121434/224ecapcarmine-1.jpg')
print(f'>>> title: {dp.title}')
# dp.download('https://static.galerieslafayette.com/media/images/hp_mod_569/hp_mod_56989832/hp_modvar_104710498/202312121434/224ecapcarmine-1.jpg', r'D:\aa', 'fx1_lrg2.jpg')
res = dp.listen.wait()  # 等待并获取一个数据包
print(f'>>> url: {res.response.url}, {res.response.headers["content-type"]}')
with open('D:/fx1_lrg.jpg', 'wb') as f:
    f.write(res.response.body)
```

### p19：drissionpage实现随时切换代理ip

视频地址：[https://www.bilibili.com/video/BV1PT421C77U/](https://www.bilibili.com/video/BV1PT421C77U)

[https://www.bilibili.com/video/BV1ph4y127Zv/](https://www.bilibili.com/video/BV1ph4y127Zv)

https://t.zsxq.com/hYDO5

```python
from DrissionPage import ChromiumPage, ChromiumOptions
from loguru import logger

co = ChromiumOptions().set_paths(browser_path=r"C:\Program Files (x86)\Microsoft\Edge\Application\msedge.exe")
# co.add_extension(r'F:\package\Proxy_SwitchyOmega_2.5.21')
co.set_timeouts(5, 5, 5)
# 设置代理 https://www.zdaye.com/free/?ip=&adr=&checktime=&sleep=&cunhuo=&dengji=1&nadr=&https=&yys=&post=&px= https://free.py.cn/
co.set_proxy('http://113.229.7.181:64256')
browser = ChromiumPage(co)
browser.set.window.max()
browser.get("https://www.ip138.com/", retry=1, interval=1, timeout=10)
html_text = browser.get_frame('x://div[@class="hd"]//iframe').ele('text:您的iP地址是').text
logger.success(f">>>>当前的ip {html_text}")
```

```python
from DrissionPage import ChromiumPage, ChromiumOptions
from loguru import logger
import platform


def get_free_ip():
    url = "https://www.zdaye.com/free/?ip=&adr=&checktime=&sleep=&cunhuo=&dengji=1&nadr=&https=&yys=&post=&px="
    browser.get(url, retry=3, interval=1, timeout=15)
    ip_ports = []
    for tr in browser.eles('x://table[@id="ipc"]//tr')[1:]:
        tds = [td.text for td in tr.eles("x://td")]
        ip_ports.append((f"{tds[0]}:{tds[1]}", tds[3]))
    print(len(ip_ports), ip_ports)
    return ip_ports


def switch_ip(ip_port=None):
    global set_proxy
    if ip_port:
        # 设置proxy
        ip, port = ip_port.split(":")
        tab = browser.new_tab()
        tab.get("chrome-extension://padekgcemlokbadohgkifijomclgjgif/options.html#!/profile/proxy")
        tab.ele('x://input[@ng-model="proxyEditors[scheme].host"]').input(ip, clear=True)
        tab.ele('x://input[@ng-model="proxyEditors[scheme].port"]').input(port, clear=True)
        tab.ele('x://a[@ng-click="applyOptions()"]').click()
        tab.wait(1)
        # 提示框
        txt = tab.handle_alert()
        print("提示框", txt)
        tab.handle_alert(accept=False)
        if not omega_proxy:
            # 切换proxy
            tab.get("chrome-extension://padekgcemlokbadohgkifijomclgjgif/popup/index.html#")
            tab.wait(1)
            tab.ele('x://span[text()="proxy"]').click()
            set_proxy = True
    else:
        tab = browser.new_tab()
        tab.get("chrome-extension://padekgcemlokbadohgkifijomclgjgif/popup/index.html#")
        tab.ele('x://span[text()="[直接连接]"]').click()
    if len(browser.tab_ids) > 1:
        print("当前tab个数", len(browser.tab_ids))
        tab.close()


if platform.system().lower() == 'windows':
    co = ChromiumOptions()  # .set_paths(browser_path=r"C:\Program Files (x86)\Microsoft\Edge\Application\msedge.exe")
else:
    co = ChromiumOptions().set_paths(browser_path=r"/opt/google/chrome/google-chrome")
    co.headless(True)  # 设置无头加载  无头模式是一种在浏览器没有界面的情况下运行的模式，它可以提高浏览器的性能和加载速
    # co.incognito(True)  # 无痕隐身模式打开的话，不会记住你的网站账号密码的
    co.set_argument('--no-sandbox')  # 禁用沙箱 禁用沙箱可以避免浏览器在加载页面时进行安全检查,从而提高加载速度 默认情况下，所有Chrome 用户都启用了隐私沙盒选项  https://zhuanlan.zhihu.com/p/475639754
    co.set_argument("--disable-gpu")  # 禁用GPU加速可以避免浏览器在加载页面时使用过多的计算资源，从而提高加载速度
    co.set_user_agent(user_agent='Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/124.0.0.0 Safari/537.36')  # 设置ua

co.set_timeouts(6, 6, 6)
co.set_local_port(9211)
# 1、设置switchyOmega插件
co.add_extension(r'F:\package\Proxy_SwitchyOmega_2.5.21')
browser = ChromiumPage(co)

# 2、重置switchyOmega插件
omega_proxy = False
switch_ip()
browser.get("https://www.ip138.com/", retry=0)
html_text = browser.get_frame('x://div[@class="hd"]//iframe').ele('text:您的iP地址是').text
logger.success(f">>>>当前的ip {html_text}")

# 3、随机切换代理ip
# ip_all = get_free_ip()
ip_all = [{"ip":"113.229.7.181","port":64256,"expire_time":"2024-04-27 22:24:00"},{"ip":"183.148.9.36","port":64256,"expire_time":"2024-04-27 22:24:00"}, {"ip":"222.90.3.113","port":64256,"expire_time":"2024-04-27 21:41:19"},{"ip":"113.218.244.146","port":64256,"expire_time":"2024-04-27 21:51:52"},{"ip":"60.174.0.124","port":64256,"expire_time":"2024-04-27 21:40:55"},{"ip":"175.174.186.230","port":64256,"expire_time":"2024-04-27 21:51:53"},{"ip":"182.136.53.219","port":64256,"expire_time":"2024-04-27 21:51:52"}]
for ips in ip_all:
    logger.info(f"~~~切换ip，now {ips['ip']}")
    # 重置switchyOmega插件
    switch_ip(f"{ips['ip']}:{ips['port']}")
    browser.wait(1)
    try:
        browser.get("https://www.baidu.com/", retry=0)
        browser.get("https://www.ip138.com/", retry=0)
        html_text = browser.get_frame('x://div[@class="hd"]//iframe').ele('text:您的iP地址是').text
        logger.success(f">>>>>>>>切换代理成功 {html_text}")
    except Exception as err:
        logger.error(f"----------切换代理失败 dp {err}")
browser.quit()
```

