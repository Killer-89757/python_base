# DES-ECB加解密

> python/nodejs

### 一、DES-ECB加解密python版本

在线测试加解密 https://www.toolhelper.cn/SymmetricEncryption/DES

```python
"""
pip install base64 -i https://mirrors.aliyun.com/pypi/simple/
pip install pycryptodome -i https://mirrors.aliyun.com/pypi/simple/
"""
import base64
from Crypto.Util.Padding import pad
from Crypto.Cipher import DES
from binascii import b2a_hex, a2b_hex


def des_ecb_encrypt_text(decrypt_text: str, key: str, method="base64", _pad='pkcs7') -> str:
    """
    DES加密
    :param decrypt_text: 明文
    :param key: 密钥
    :param _pad: 补位
    :param method: 用base64加密还是16进制字符串
    :return: 加密后的数据
    """
    des_obj = DES.new(key.encode('utf-8'), DES.MODE_ECB)
    encrypt_text = des_obj.encrypt(pad(decrypt_text.encode('utf-8'), DES3.block_size, style=_pad))
    if method == "base64":
        return base64.b64encode(encrypt_text).decode()
    else:
        return b2a_hex(encrypt_text).decode()


def des_ecb_decrypt_text(encrypt_text: str, key: str, method="base64", _pad='pkcs7') -> str:
    """
    DES解密
    :param encrypt_text: 密文
    :param key: 秘钥
    :param _pad: 补位
    :param method: 用base64解密还是16进制字符串
    :return:解密后的数据
    """
    des_obj = DES.new(key.encode('utf-8'), DES.MODE_ECB)
    if method == "base64":
        decrypt_text = des_obj.decrypt(base64.b64decode(encrypt_text)).decode('utf8')
    else:
        decrypt_text = des_obj.decrypt(a2b_hex(encrypt_text)).decode('utf8')
    return decrypt_text


print("加密", des_ecb_encrypt_text('123', '54cea83f', "base64"))
print("解密", des_ecb_decrypt_text('iw1h1XitV2U=', '54cea83f', "base64"))
print("\n加密", des_ecb_encrypt_text('12345', '54cea83f', "hex"))
print("解密", des_ecb_decrypt_text('8758ca32e628c4dc', '54cea83f', "hex"))
```

### 二、DES-ECB加解密js版本

```js
/*
npm install crypto-js -g --registry=http://registry.npm.taobao.org
此脚本默认CryptoJS.enc.Utf8.parse，实际有 CryptoJS.enc.Latin1.parse以及CryptoJS.enc.Hex.parse可自行替换
*/
var CryptoJS = require("crypto-js");
var encrypt_req = function(key, text) {
    var l = CryptoJS.enc.Utf8.parse(text);
    var e = CryptoJS.enc.Utf8.parse(key);
    var a = CryptoJS.DES.encrypt(l, e, {
        mode: CryptoJS.mode.ECB,
        padding: CryptoJS.pad.Pkcs7
    })
    return a.toString()   // 此方式返回base64  nGzKZlCA7AhB7tnRNHxwcGvplRh05W+uhAi3i1c9mV3Qi4Gq+NrHeIO1P/ezY38S
    // return a.ciphertext.toString()   // 返回hex格式的密文  9c6cca665080ec0841eed9d1347c70706be9951874e56fae8408b78b573d995dd08b81aaf8dac77883b53ff7b3637f12
}

var decrypt_req = function(key, text) {
    var e = CryptoJS.enc.Utf8.parse(key);
    // var WordArray = CryptoJS.enc.Hex.parse(text);  // 如果text是base64形式，该行注释掉
    // var text = CryptoJS.enc.Base64.stringify(WordArray);  // 如果text是base64形式，该行注释掉
    var a = CryptoJS.DES.decrypt(text, e, {
        mode: CryptoJS.mode.ECB,
        padding: CryptoJS.pad.Pkcs7
    });
    return CryptoJS.enc.Utf8.stringify(a).toString()
}

// CBC模式加密
console.log(encrypt_req("8c18266c4e8fa5de", '{"Type":0,"page":3,"expire":1596461032894}'));
// CBC模式解密
console.log(decrypt_req("8c18266c4e8fa5de", 'gz4LRzOMhl4hROqy/QjLrqgVqJa5tfwjmkFyMwvVDsZP1eh0KnkOWOZh8gI5rVzs'));
```

