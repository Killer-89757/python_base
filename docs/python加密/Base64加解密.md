# Base64加解密

> python/nodejs

### 一、Base64加解密python版本

在线测试加解密 https://tool.chinaz.com/tools/base64.aspx

```python
"""
pip install base64 -i https://mirrors.aliyun.com/pypi/simple/
"""
import base64


def base64_encrypt_text(_text: str) -> str:
    """
    Bse64加密
    :param _text: 明文
    :return: 密文
    """
    return base64.b64encode(_text.encode("utf-8")).decode()


def base64_decrypt_text(_text: str) -> str:
    """
    Bse64解密
    :param _text: 密文
    :return: 明文
    """
    return base64.b64decode(_text).decode("utf-8")


print(base64_encrypt_text("123"))  # MTIz
print(base64_decrypt_text("MTIz"))  # 123
```

### 二、base64加解密js版本

```js
/*
npm install btoa -g --registry=http://registry.npm.taobao.org
npm install atob -g --registry=http://registry.npm.taobao.org
*/

var btoa = require('btoa')
var base64_encode = function(a){
	return btoa(a)
}
var atob = require('atob')
var base64_decode = function(a){
	return atob(a)
}

console.log(base64_encode(12345))  // MTIzNDU=
console.log(base64_decode('MTIzNDU='))  // 12345
```

