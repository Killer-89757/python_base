# md5/sha256/hmac512加密

> python/nodejs

### 一、hash加密python版本

在线测试加密 https://www.toolhelper.cn/DigestAlgorithm/HMAC_SHA 

```python
from hashlib import md5
from hashlib import sha1
from hashlib import sha256
from hashlib import sha512
import hmac


def md5_encrypt_text(decrypt_text: str) -> str:
    """
    md5加密
    :param decrypt_text: 明文
    :return: 密文
    """
    return md5(decrypt_text.encode('utf8')).hexdigest()


def sha1_encrypt_text(decrypt_text: str) -> str:
    """
    SHA1加密
    :param decrypt_text: 明文
    :return: 密文
    """
    return sha1(decrypt_text.encode('utf8')).hexdigest()


def sha256_encrypt_text(decrypt_text: str) -> str:
    """
    SHA256加密
    :param decrypt_text: 明文
    :return: 密文
    """
    return sha256(decrypt_text.encode('utf8')).hexdigest()


def sha512_encrypt_text(decrypt_text: str) -> str:
    """
    SHA512加密
    :param decrypt_text: 明文
    :return: 密文
    """
    return sha512(decrypt_text.encode('utf8')).hexdigest()


def hmac_encrypt_text(decrypt_text: str, key: str, mode='md5') -> str:
    """
    SHA1加密
    :param decrypt_text: 明文
    :param key: 密钥
    :param mode: md5/sha512/sha256
    :return: 密文
    """
    if mode == 'md5':
        mac = hmac.new(key.encode('utf-8'), decrypt_text.encode('utf-8'), md5)
    elif mode == 'sha512':
        mac = hmac.new(key.encode('utf-8'), decrypt_text.encode('utf-8'), sha512)
    else:
        mac = hmac.new(key.encode('utf-8'), decrypt_text.encode('utf-8'), sha256)
    return mac.hexdigest()


print(md5_encrypt_text("123"))  # 202cb962ac59075b964b07152d234b70
print(sha1_encrypt_text("123"))  # 40bd001563085fc35165329ea1ff5c5ecbdbbeef
print(sha256_encrypt_text("123"))  # a665a45920422f9d417e4867efdc4fb8a04a1f3fff1fa07e998e86f7f7a27ae3
print(sha512_encrypt_text("123"))  # 3c9909afec25354d551dae21590bb26e38d53f2173b8d3dc3eee4c047e7ab1c1eb8b85103e3be7ba613b31bb5c9c36214dc9f14a42fd7a2fdb84856bca5c44c2
print(hmac_encrypt_text("123", "r3vBrB3fj00jUf330Bve0vjefjrv", 'sha512'))  # 99038ce67e4c811e2aeae3306b8d2f41
```

### 二、hash加密js版本

```js
/*
npm install crypto-js -g --registry=http://registry.npm.taobao.org
npm install md5 -g --registry=http://registry.npm.taobao.org
*/
var CryptoJS = require("crypto-js");
// var md5 = function(a){
//     return CryptoJS.MD5(a).toString()
// };
var md5 = require("md5");
var sha1 = function(a){
    return CryptoJS.SHA1(a).toString();
};
var sha256 = function(a){
    return CryptoJS.SHA256(a).toString();
};
var sha512 = function(a){
    return CryptoJS.SHA512(a).toString();
};
var sha3 = function(a){
    return CryptoJS.SHA3(a).toString();
};
var HmacSHA512 = function(text, key){
    return CryptoJS.HmacSHA512(text, key);
};

console.log("md5", md5("123"))     // 202cb962ac59075b964b07152d234b70
console.log("sha1", sha1("123"))    // 40bd001563085fc35165329ea1ff5c5ecbdbbeef
console.log("sha256", sha256("123"))  // a665a45920422f9d417e4867efdc4fb8a04a1f3fff1fa07e998e86f7f7a27ae3
console.log("sha512", sha512("123"))  // 3c9909afec25354d551dae21590bb26e38d53f2173b8d3dc3eee4c047e7ab1c1eb8b85103e3be7ba613b31bb5c9c36214dc9f14a42fd7a2fdb84856bca5c44c2
console.log("sha3", sha3("123"))    // 8ca32d950873fd2b5b34a7d79c4a294b2fd805abe3261beb04fab61a3b4b75609afd6478aa8d34e03f262d68bb09a2ba9d655e228c96723b2854838a6e613b9d
console.log("HmacSHA512", HmacSHA512("123", "r3vBrB3fj00jUf330Bve0vjefjrv").toString())  // 2331109304ac2082f163a307a7720f4a1502ad8e3fa3fdf2091aac40657a5e2aaabe808e18e2d61e9a03ac7c46950804c90651f12744397a4c4c5cf7b529e3d8
```

