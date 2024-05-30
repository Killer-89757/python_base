# 实现自由切换代理和ua

**前言**

上一篇我们自己实现了一个代理插件，这一篇文章我们直接实现一个能够**自由切换代理和UA**的插件来满足我们在自动化过程中对代理和UA的切换。

## 案例

我们先打开上一篇文章中开发的代理插件，如下：

![img](https://cdn.jsdelivr.net/gh/Killer-89757/PicBed/images/2024%2F05%2FFoi_FjZPO83i3-NrugAWPv--UV4O-7e931d.png)

这一篇我们需要用到的就是这两个方法，然后我们回顾一下第一篇认识插件中是不是有一个叫做后台脚本文件的，然后manifest.json配置文件中也有一个background（后台脚本）的配置，有了这个后台脚本，我们就只需要能够实时跟这个background（后台脚本）进行交互就可以实现我们自由切换代理或者UA的功能了，那么我们怎样跟这个background（后台脚本）进行实时交互呢？这个时候就会想起jsrpc，是的，由于已经有渣总开发的jsrpc工具-sekiro，所以这里我们直接在这个的基础上进行修改就好了，首先把sekrio脚本拿过来，之后将下面的代码放进sekrio脚本，代码如下：

```js
function resetProxy() {
    chrome.proxy.settings.clear(
        {scope: 'regular'},
        function () {
            var success = !chrome.runtime.lastError;
            console.log(success);
        }
    );
}

function setProxy(host, port) {

    var config = {
        mode: "fixed_servers", rules: {
            singleProxy: {
                scheme: "http", host: host, port: port ? parseInt(port) : ""
            }, bypassList: []
        }
    };
    chrome.proxy.settings.set({value: config, scope: 'regular'}, function () {
        var success = !chrome.runtime.lastError;
        if (success) {
            console.log("set proxy success");
        } else {
            console.log("set proxy failed:" + chrome.runtime.lastError.message);
        }
    });
}
```

之后就是修改请求中的逻辑了，这个逻辑大家自己按照自己的思路写就行了，我是这样写的，如下：

![img](https://cdn.jsdelivr.net/gh/Killer-89757/PicBed/images/2024%2F05%2FFp6VcrFqHwbHoo1OdMnBmCCTwEeu-8c5f5b.png)

到这里切换代理的逻辑就已经好了，接下来我们来看看如何修改UA，这里要修改的UA是发包的UA，修改之后是如下的样子：

![img](https://cdn.jsdelivr.net/gh/Killer-89757/PicBed/images/2024%2F05%2FFl0OnpqXEst4Fy68Pxuzwo2TEm3c-d19daf.png)

![img](https://cdn.jsdelivr.net/gh/Killer-89757/PicBed/images/2024%2F05%2FFpHDUwZxZjslKgLLPo_vqLzR6g1_-dcc694.png)

修改发包UA的代码我就直接贴出来了，如下：

```js
//ua切换部分
chrome.webRequest.onBeforeSendHeaders.addListener(
    function (details) {
        for (let i = 0; i < details.requestHeaders.length; ++i) {
            if (details.requestHeaders[i].name === 'User-Agent') {
                let ua = localStorage.getItem('ua');
                if (!ua) break;
                if (ua === "default") break;
                else {
                    ua_valuve = localStorage.getItem('customua') || navigator.userAgent
                    details.requestHeaders[i].value = ua_valuve
                }
                break;
            }
        }
        return {requestHeaders: details.requestHeaders};
    },
    {urls: ["*://*/*"]},
    ["blocking", "requestHeaders"]
);
```

还是把这段代码直接放到刚才的脚本文件中，这里由于这个脚本文件是在后台运行的，我们按照插件里的方式命令，直接命名为[background.js](http://background.js/)，之后还是按照使用jsrpc的方式来实现判断逻辑就好了，我的代码如下：![img](https://cdn.jsdelivr.net/gh/Killer-89757/PicBed/images/2024%2F05%2FFshZqJ_3BMHMWunAlfGWi0bnQ3U5-2f6545.png)

到这里整个后台脚本的逻辑就完成了，接下来我们创建配置文件，配置如下：

```js
{
  "background": {
    "scripts": [
      "js/background.js"
    ]
  },
  "manifest_version": 2,
  "name": "Change Proxy or Ua Extension",
  "version": "1.0",
  "description": "自由切换代理IP或UA",
  "permissions": [
    "proxy",
    "tabs",
    "storage",
    "webRequest",
    "webRequestBlocking",
    "*://*/*"
  ],
  "icons": {
    "128": "icon.png"
  },
  "browser_action": {
    "default_title": "Change Proxt Or Ua Setting"
  }
}
```

整个完成之后就是下面这样了

![img](https://cdn.jsdelivr.net/gh/Killer-89757/PicBed/images/2024%2F05%2FFnSoocTPLpdys4Iw1tc8AWFYflPY-ef07a4.png)

可以发现这个插件没啥文件，主要的逻辑都是在后台脚本文件中，接下来我们来试试，还是安装插件，安装完成之后我们先发起一个请求看看，如下：

![img](https://cdn.jsdelivr.net/gh/Killer-89757/PicBed/images/2024%2F05%2FFgj4skodHjoXvcb3_DKCKZokFnds-165139.png)

之后我们先启动[sekiro.bat](http://sekiro.bat/)，启动之后我们直接在本地发起请求来切换UA看看，如下

![img](https://cdn.jsdelivr.net/gh/Killer-89757/PicBed/images/2024%2F05%2FFiyiCZ8wVPmgt3VobF8Z-ex8WPqe-85041c.png)

可以看到请求成功了，然后我们看看浏览器中是不是也成功了，如下：

![img](https://cdn.jsdelivr.net/gh/Killer-89757/PicBed/images/2024%2F05%2FFpLlFKwZKjzskWtgy-eYyYiXGldL-5d6d2c.png)

可以看到发包的UA 已经改变了，这就说明我们的插件中切换UA的功能是没有问题的，然后我们再来试试切换代理，先看看没切换之前的，如下：

![img](https://cdn.jsdelivr.net/gh/Killer-89757/PicBed/images/2024%2F05%2FFqqtYUT0btjKLyzYA7fhcLPAHEmC-45e691.png)

之后我们本地发起请求来切换代理，如下：

![img](https://cdn.jsdelivr.net/gh/Killer-89757/PicBed/images/2024%2F05%2FFqEsB3EEHesa4lnzHqg4O_YdYkFB-e61b54.png)

看到请求中是显示成功的，然后我们再来看看浏览器中的代理是否变了，如下：

![img](https://cdn.jsdelivr.net/gh/Killer-89757/PicBed/images/2024%2F05%2FFtzq0NCJtXvbX9K2NhoEbhNI3q5p-b4284c.png)

可以看到代理切换成功了，切换代理和切换UA都是没有问题的，那就说明我们的插件也是没问题的，所以整个插件到这里就完成了。最后如果通信部分大家不想用sekiro的话也可以用其它的方式来代替，我比较懒，所以就直接用的现成的了，有了这个经验之后，后面大家也可以按这种方式来开发其它功能的插件供自己使用。

