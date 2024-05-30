# AES-ECB加解密

> python/nodejs

### 一、AES-ECB加解密python版本

在线测试加解密 https://www.toolhelper.cn/SymmetricEncryption/AES

```python
"""
pip install base64 -i https://mirrors.aliyun.com/pypi/simple/
pip install pycryptodome -i https://mirrors.aliyun.com/pypi/simple/
"""
import base64
from Crypto.Util.Padding import pad
from Crypto.Cipher import AES
from binascii import b2a_hex, a2b_hex


def aes_ecb_encrypt_text(_text: str, key: str, method="base64", m_pad='pkcs7') -> str:
    """
    AES加密
    :param _text: 明文
    :param key: 密钥
    :param method: 用base64加密还是16进制字符串
    :param m_pad: 补位方式
    :return: 密文
    """
    aes = AES.new(key.encode('utf-8'), AES.MODE_ECB)
    encrypt_text = aes.encrypt(pad(_text.encode('utf-8'), AES.block_size, style=m_pad))
    if method == "base64":
        return base64.b64encode(encrypt_text).decode()
    else:
        return b2a_hex(encrypt_text).decode()


def aes_ecb_decrypt_text(_text: str, key: str, method="base64") -> str:
    """
    AES解密
    :param _text: 密文
    :param key: 密钥
    :param method: 用base64解密还是16进制字符串
    :return:解密后的数据
    """
    aes = AES.new(key.encode('utf-8'), AES.MODE_ECB)
    if method == "base64":
        decrypt_text = aes.decrypt(base64.b64decode(_text)).decode('utf8')
    else:
        decrypt_text = aes.decrypt(a2b_hex(_text)).decode('utf8')
    return decrypt_text.strip()


print("\n加密", aes_ecb_encrypt_text('123', '54cea83f35b90a2f', "base64"))
print("解密", aes_ecb_decrypt_text('l91Gj0S+VJeNuyifYAkA3Q==', '54cea83f35b90a2f',  "base64"))
print("\n加密", aes_ecb_encrypt_text('12345', 'G6QMOUDZnKa010vO', "hex"))
print("解密", aes_ecb_decrypt_text('fb179e67abd0e1ae68ef329ce8389805', 'G6QMOUDZnKa010vO', "hex"))
```

### 二、AES-ECB加解密js版本

```js
/*
npm install crypto-js -g --registry=http://registry.npm.taobao.org
此脚本默认CryptoJS.enc.Utf8.parse，实际有 CryptoJS.enc.Latin1.parse以及CryptoJS.enc.Hex.parse可自行替换
*/

var CryptoJS = require("crypto-js");
var aes_ecb_encrypt_req = function(key, text) {
    var l = CryptoJS.enc.Utf8.parse(text);
    var e = CryptoJS.enc.Utf8.parse(key);
    var a = CryptoJS.AES.encrypt(l, e, {
        mode: CryptoJS.mode.ECB,
        padding: CryptoJS.pad.Pkcs7
    })
    // return a.toString()   // 此方式返回base64  7zHGSW218ARpzbHHsA90NuWHufnCLJo94vGad3zzkANQ3sFIWhHY6pDLzelv9XUO
    return a.ciphertext.toString()   // 返回hex格式的密文  ef31c6496db5f00469cdb1c7b00f7436e587b9f9c22c9a3de2f19a777cf3900350dec1485a11d8ea90cbcde96ff5750e
}

var aes_ecb_decrypt_req = function(key, text) {
    var e = CryptoJS.enc.Utf8.parse(key);
    var WordArray = CryptoJS.enc.Hex.parse(text);  // 如果text是base64形式，该行注释掉
    var text = CryptoJS.enc.Base64.stringify(WordArray);  // 如果text是base64形式，该行注释掉
    var a = CryptoJS.AES.decrypt(text, e, {
        mode: CryptoJS.mode.ECB,
        padding: CryptoJS.pad.Pkcs7
    });
    return CryptoJS.enc.Utf8.stringify(a).toString()
}
// ecb模式加密hex
console.log(aes_ecb_encrypt_req('54cea83f35b90a2f', '{"Type":0,"page":3,"expire":1596461032894}'));
// ecb模式解密hex
console.log(aes_ecb_decrypt_req('54cea83f35b90a2f','d0ec82ae57eca54289199d69899103f2c3a701e780427f8d1fc7a633b2f1471057737a36cd8f5413758ebfd425628f0f'));
```



