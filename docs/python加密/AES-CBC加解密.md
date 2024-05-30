# AES-CBC加解密

> python/nodejs

### 一、AES-CBC加解密python版本

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


def aes_cbc_encrypt_text(_text: str, key: str, iv="", method="base64", m_pad='pkcs7') -> str:
    """
    AES加密
    :param _text: 明文
    :param key: 密钥
    :param iv: 密钥偏移量，只有CBC模式有
    :param method: 用base64加密还是16进制字符串
    :param m_pad: 补位方式
    :return: 密文
    """
    aes = AES.new(key.encode('utf-8'), AES.MODE_CBC, iv.encode('utf-8'))
    encrypt_text = aes.encrypt(pad(_text.encode('utf-8'), AES.block_size, style=m_pad))
    if method == "base64":
        return base64.b64encode(encrypt_text).decode()
    elif method == "iv_arr":
        result_bytes = iv.encode("utf-8") + encrypt_text
        return base64.b64encode(result_bytes).decode()
    else:
        return b2a_hex(encrypt_text).decode()


def aes_cbc_decrypt_text(_text: str, key: str, iv="", method="base64") -> str:
    """
    AES解密
    :param _text: 密文
    :param key: 密钥
    :param iv: 密钥偏移量，只有CBC模式有
    :param method: 用base64解密还是16进制字符串
    :return:解密后的数据
    """
    aes = AES.new(key.encode('utf-8'), AES.MODE_CBC, iv.encode('utf-8'))
    if method == "base64":
        decrypt_text = aes.decrypt(base64.b64decode(_text)).decode('utf8')
    else:
        decrypt_text = aes.decrypt(a2b_hex(_text)).decode('utf8')
    return decrypt_text.strip()


print("加密", aes_cbc_encrypt_text('ts=1695014591749', '54cea83f35b90a2fa4d268d2c071bf0d', 'G6QMOUDZnKa010vO', "iv_arr"))
print("\n加密", aes_cbc_encrypt_text('123', '54cea83f35b90a2f', 'G6QMOUDZnKa010vO', "base64"))
print("解密", aes_cbc_decrypt_text('7+z1xoIqhkPtUasiPfiYoA==', '54cea83f35b90a2f', 'G6QMOUDZnKa010vO', "base64"))
print("\n加密", aes_cbc_encrypt_text('12345', '54cea83f35b90a2f', 'G6QMOUDZnKa010vO', "hex"))
print("解密", aes_cbc_decrypt_text('a9a001c295c7e9ac3707681f640fe2a0', '54cea83f35b90a2f', 'G6QMOUDZnKa010vO', "hex"))
```

### 二、AES-CBC加解密js版本

```js
/*
npm install crypto-js -g --registry=http://registry.npm.taobao.org
此脚本默认CryptoJS.enc.Utf8.parse，实际有 CryptoJS.enc.Latin1.parse以及CryptoJS.enc.Hex.parse可自行替换
*/
var CryptoJS = require("crypto-js");
var aes_cbc_encrypt_req = function(key, iv, text) {
    var l = CryptoJS.enc.Utf8.parse(text);
    var e = CryptoJS.enc.Utf8.parse(key);
    var a = CryptoJS.AES.encrypt(l, e, {
        mode: CryptoJS.mode.CBC,
        padding: CryptoJS.pad.Pkcs7,
        iv: CryptoJS.enc.Utf8.parse(iv)
    })
    // return a.toString()   // 此方式返回base64  7zHGSW218ARpzbHHsA90NuWHufnCLJo94vGad3zzkANQ3sFIWhHY6pDLzelv9XUO
    return a.ciphertext.toString()   // 返回hex格式的密文  ef31c6496db5f00469cdb1c7b00f7436e587b9f9c22c9a3de2f19a777cf3900350dec1485a11d8ea90cbcde96ff5750e
}

var aes_cbc_decrypt_req = function(key, iv, text) {
    var e = CryptoJS.enc.Utf8.parse(key);
    var WordArray = CryptoJS.enc.Hex.parse(text);  // 如果text是base64形式，该行注释掉
    var text = CryptoJS.enc.Base64.stringify(WordArray);  // 如果text是base64形式，该行注释掉
    var a = CryptoJS.AES.decrypt(text, e, {
        mode: CryptoJS.mode.CBC,
        padding: CryptoJS.pad.Pkcs7,
        iv: CryptoJS.enc.Utf8.parse(iv)
    });
    return CryptoJS.enc.Utf8.stringify(a).toString()
}
// CBC模式加密hex
console.log(aes_cbc_encrypt_req('54cea83f35b90a2f', "8c18266c4e8fa5de", '{"Type":0,"page":3,"expire":1596461032894}'));
// CBC模式解密hex
console.log(aes_cbc_decrypt_req('54cea83f35b90a2f', "8c18266c4e8fa5de", 'dcc52f059054900e168571b8ccccdf8454e7501d579b7a65ddc6112e7d1bfa789b92c90d4536a654ba85b1bd03da45de'));
```

