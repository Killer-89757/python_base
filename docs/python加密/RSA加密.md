# RSA加密

> python

### 一、RSA加密python版本

```python
"""
pip install base64 -i https://mirrors.aliyun.com/pypi/simple/
pip install rsa -i https://mirrors.aliyun.com/pypi/simple/
"""
import base64
import rsa
from binascii import b2a_hex, a2b_hex
from Crypto.PublicKey import RSA
from Crypto.Cipher import PKCS1_OAEP, PKCS1_v1_5
import binascii

class RsaUtil:

    @staticmethod
    def rsa_encrypt_text1(public_key, decrypt_text: str, method="base64") -> str:
        """
        RSA加密
        :param public_key:  公钥
        :param decrypt_text: 明文
        :param method: 用base64加密还是16进制字符串
        :return: 加密后的数据
        """
        encrypt_text = rsa.encrypt(decrypt_text.encode('utf-8'), rsa.PublicKey.load_pkcs1(public_key))
        if method == "base64":
            return base64.b64encode(encrypt_text).decode()
        else:
            return b2a_hex(encrypt_text).decode()

    @staticmethod
    def rsa_encrypt_text2(public_key, _text: str, method="base64") -> str:
        """
        RSA加密，针对setPublicKey
        :param public_key:  公钥
        :param _text: 明文
        :param method: 用base64加密还是16进制字符串
        :return: 加密后的数据
        """
        encrypt_text = rsa.encrypt(_text.encode('utf-8'), rsa.PublicKey.load_pkcs1_openssl_pem(public_key))
        if method == "base64":
            return base64.b64encode(encrypt_text).decode()
        else:
            return b2a_hex(encrypt_text).decode()

    @staticmethod
    def rsa_encrypt_text3(key, _text: str, method="base64"):
        """
        RSA加密，针对new RSAKeyPair
        import rsa
        from binascii import b2a_hex
        :param key: 公钥的参数
        :param _text: 待加密的明文
        :param method: 用base64加密还是16进制字符串
        :return: 加密后的数据
        """
        e = int('010001', 16)
        n = int(key, 16)
        pub_key = rsa.PublicKey(e=e, n=n)
        encrypt_text = rsa.encrypt(_text.encode(), pub_key)
        if method == "base64":
            return base64.b64encode(encrypt_text).decode()
        else:
            return b2a_hex(encrypt_text).decode()

    @staticmethod
    def rsa_decrypt_text(private_key, encrypt_text: str, method="base64") -> str:
        """
        RSA解密
        :param private_key: 私钥
        :param encrypt_text: 密文
        :return: 明文
        """
        if method == "base64":
            decrypt_text = rsa.decrypt(base64.b64decode(encrypt_text), rsa.PrivateKey.load_pkcs1(private_key)).decode('utf8')
        else:
            decrypt_text = rsa.decrypt(a2b_hex(encrypt_text), rsa.PrivateKey.load_pkcs1(private_key)).decode('utf8')
        return decrypt_text

    @staticmethod
    def rsa_sign(private_key, decrypt_text, method="MD5"):
        """
        rsa签名
        :param private_key: 私钥
        :param decrypt_text: 明文
        :param method: 'MD5', 'SHA-1','SHA-224', SHA-256', 'SHA-384' or 'SHA-512'
        :return:
        """
        sign_text = rsa.sign(decrypt_text.encode('utf-8'), rsa.PrivateKey.load_pkcs1(private_key), method)
        sign_text = base64.b64encode(sign_text).decode()
        return sign_text

    @staticmethod
    def rsa_verify(signature, public_key, decrypt_text):
        """
        rsa验签
        :param signature: rsa签名
        :param public_key: 公钥
        :param decrypt_text: 明文
        :return:
        """
        return rsa.verify(decrypt_text.encode('utf-8'), base64.b64decode(signature), rsa.PublicKey.load_pkcs1(public_key))


rsa_obj = RsaUtil()

# rsa加密解密
publicKey = '''
-----BEGIN RSA PUBLIC KEY-----
MIGJAoGBANkDMlvSfrZaowpBQUF0gFRzwt3w0q4rWet33FdWuq39TBdCVicy4Zzw zX5ziuFExkdwbVrhEHBRkGNBJYVJ/1F1gAwd3KdyaId5NwATFkkLyM3wOtFqttwm o888U9KwIyhGH2bFkRIsk+KQmNQIR1m8Fgpdsy2JbnLd559HpTZZAgMBAAE=
-----END RSA PUBLIC KEY----- 
'''
_decrypt_str = "nihao@456"
_encrypt_str = rsa_obj.rsa_encrypt_text1(publicKey, _decrypt_str)
print(f"RSA加密: {_encrypt_str}")


public_key = """
-----BEGIN PUBLIC KEY-----
MIGfMA0GCSqGSIb3DQEBAQUAA4GNADCBiQKBgQDXQG8rnxhslm+2f7Epu3bB0inrnCaTHhUQCYE+2X+qWQgcpn+Hvwyks3A67mvkIcyvV0ED3HFDf+ANoMWV1Ex56dKqOmSUmjrk7s5cjQeiIsxX7Q3hSzO61/kLpKNH+NE6iAPpm96Fg15rCjbm+5rR96DhLNG7zt2JgOd2o1wXkQIDAQAB
-----END PUBLIC KEY-----"""
_encrypt_str = rsa_obj.rsa_encrypt_text2(public_key, "12242")
print(f"RSA加密setPublicKey: 加密{_encrypt_str}")


key = "978C0A92D2173439707498F0944AA476B1B62595877DD6FA87F6E2AC6DCB3D0BF0B82857439C99B5091192BC134889DFF60C562EC54EFBA4FF2F9D55ADBCCEA4A2FBA80CB398ED501280A007C83AF30C3D1A142D6133C63012B90AB26AC60C898FB66EDC3192C3EC4FF66925A64003B72496099F4F09A9FB72A2CF9E4D770C41"
_encrypt_str = rsa_obj.rsa_encrypt_text3(key, "12242", 'hex')
print(f"RSA加密new RSAKeyPair: 加密{_encrypt_str}")


print("\n================================================================================================\n================================================================================================\n")

"""公钥格式如下
来源于文章： https://mp.weixin.qq.com/s/el9zsj1EeQ4fHkVoWNRhVQ
第一种：
    -----BEGIN PUBLIC KEY-----\nMIGfMA0GCSqGSIb3DQEBAQUAA4GNADCBiQKBgQC5gsH+AA4XWONB5TDcUd+xCz7ejOFHZKlcZDx+pF1i7Gsvi1vjyJoQhRtRSn950x498VUkx7rUxg1/ScBVfrRxQOZ8xFBye3pjAzfb22+RCuYApSVpJ3OO3KsEuKExftz9oFBv3ejxPlYc5yq7YiBO8XlTnQN0Sa4R4qhPO3I2MQIDAQAB\n-----END PUBLIC KEY-----
第二种： base64值
    MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAok58IrYXjeFjb6hPgrcvKis43ARDVIqowS2AJKivDp4+8uKDCWnjzBZTsuVvwKPzvVCxBzON2/DPpHU3wnRtdKSVzWju7HMKhuLxe04FsVw8+xvZTmguBj4jTczNLSLjK13lQr46J8j7JrmVUlPqGxIL/Bd3HNAIFuarZQkDsgx5fvdNrMbmT4edr1b3A8wRkhfo9tuE5Tmlx0YVUwybzcI6hgLggCfNwwaClXyBt08NbGSIBcKYKjiQErND0EOnWcGyto7EhkpgGRfAeESo3hbmsiabThLd4t9iOWVHFSl+7B0q+1IGFjSo9qkvNdMUI4ZYdIKq+nCHufpuFMl7SwIDAQAB"
第三种： hex值
    3.1这是字符串类型的
    模数：'00C1E3934D1614465B33053E7F48EE4EC87B14B95EF88947713D25EECBFF7E74C7977D02DC1D9451F79DD5D1C10C29ACB6A9B4D6FB7D0A0279B6719E1772565F09AF627715919221AEF91899CAE08C0D686D748B20A3603BE2318CA6BC2B59706592A9219D0BF05C9F65023A21D2330807252AE0066D59CEEFA5F2748EA80BAB81'
    指数："010001"
    3.2这是int类型的
    模数：136153462421446847404340432441046996374735571025589056967906613334049032306309642600950180794472974184474850029075084679952125029724775675860862428869529368335136951744118770626613042094193316007621445630035543273179259178158896311604233203144417656446177150555868699549873157540592293125574640692009097735041
    指数：65537
"""
public_key_str = """-----BEGIN PUBLIC KEY-----
MIGfMA0GCSqGSIb3DQEBAQUAA4GNADCBiQKBgQC5gsH+AA4XWONB5TDcUd+xCz7ejOFHZKlcZDx+pF1i7Gsvi1vjyJoQhRtRSn950x498VUkx7rUxg1/ScBVfrRxQOZ8xFBye3pjAzfb22+RCuYApSVpJ3OO3KsEuKExftz9oFBv3ejxPlYc5yq7YiBO8XlTnQN0Sa4R4qhPO3I2MQIDAQAB
-----END PUBLIC KEY-----"""

public_key = RSA.importKey(public_key_str)
print("》》》》》》》》》》公钥：", public_key_str)
print("指数：", public_key.e)
print("模数：", public_key.n)

public_key_str = "MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAok58IrYXjeFjb6hPgrcvKis43ARDVIqowS2AJKivDp4+8uKDCWnjzBZTsuVvwKPzvVCxBzON2/DPpHU3wnRtdKSVzWju7HMKhuLxe04FsVw8+xvZTmguBj4jTczNLSLjK13lQr46J8j7JrmVUlPqGxIL/Bd3HNAIFuarZQkDsgx5fvdNrMbmT4edr1b3A8wRkhfo9tuE5Tmlx0YVUwybzcI6hgLggCfNwwaClXyBt08NbGSIBcKYKjiQErND0EOnWcGyto7EhkpgGRfAeESo3hbmsiabThLd4t9iOWVHFSl+7B0q+1IGFjSo9qkvNdMUI4ZYdIKq+nCHufpuFMl7SwIDAQAB"
key_bytes = base64.b64decode(public_key_str)
public_key = RSA.importKey(key_bytes)
print("》》》》》》》》》》公钥：", public_key_str)
print("指数：", public_key.e)
print("模数：", public_key.n)

exponents = "010001"
moduluss = '00C1E3934D1614465B33053E7F48EE4EC87B14B95EF88947713D25EECBFF7E74C7977D02DC1D9451F79DD5D1C10C29ACB6A9B4D6FB7D0A0279B6719E1772565F09AF627715919221AEF91899CAE08C0D686D748B20A3603BE2318CA6BC2B59706592A9219D0BF05C9F65023A21D2330807252AE0066D59CEEFA5F2748EA80BAB81'
modulus = int(moduluss, 16)
exponent = int(exponents, 16)

public_key = RSA.construct((modulus, exponent))
print("》》》》》》》》》》str指数：", exponents)
print("指数：", public_key.e)
print("str模数：", moduluss)
print("模数：", public_key.n)


class RSAUtilGeneral:
    def __init__(self, key_str: str = None, _modulus: str | int = None, _exponent: str | int = None, _PKCS: int = 1):
        """
        参数样式
        :param key_str:
        第一种：
        "-----BEGIN PUBLIC KEY-----\n" \
        "MIGfMA0GCSqGSIb3DQEBAQUAA4GNADCBiQKBgQC5gsH+AA4XWONB5TDcUd+xCz7ejOFHZKlcZDx+pF1i7Gsvi1vjyJoQhRtRSn950x498VUkx7rUxg1/ScBVfrRxQOZ8xFBye3pjAzfb22+RCuYApSVpJ3OO3KsEuKExftz9oFBv3ejxPlYc5yq7YiBO8XlTnQN0Sa4R4qhPO3I2MQIDAQAB\n" \
        "-----END PUBLIC KEY-----"
        第二种：
        'MIGfMA0GCSqGSIb3DQEBAQUAA4GNADCBiQKBgQC5gsH+AA4XWONB5TDcUd+xCz7ejOFHZKlcZDx+pF1i7Gsvi1vjyJoQhRtRSn950x498VUkx7rUxg1/ScBVfrRxQOZ8xFBye3pjAzfb22+RCuYApSVpJ3OO3KsEuKExftz9oFBv3ejxPlYc5yq7YiBO8XlTnQN0Sa4R4qhPO3I2MQIDAQAB'

        :param _modulus:
        第一种（str类型）：
        '00C1E3934D1614465B33053E7F48EE4EC87B14B95EF88947713D25EECBFF7E74C7977D02DC1D9451F79DD5D1C10C29ACB6A9B4D6FB7D0A0279B6719E1772565F09AF627715919221AEF91899CAE08C0D686D748B20A3603BE2318CA6BC2B59706592A9219D0BF05C9F65023A21D2330807252AE0066D59CEEFA5F2748EA80BAB81'
        第二种（int类型）：
        136153462421446847404340432441046996374735571025589056967906613334049032306309642600950180794472974184474850029075084679952125029724775675860862428869529368335136951744118770626613042094193316007621445630035543273179259178158896311604233203144417656446177150555868699549873157540592293125574640692009097735041

        :param _exponent:
        第一种（str类型）：
        "010001"
        第二种（int类型）：
        65537

        :param _PKCS
        1: PKCS1_OAEP
        2: PKCS1_v1_5
        """
        if key_str and "-----" in key_str:
            key_str = key_str.replace("\n", "").replace(" ", "").split("-----")
            key_str = [x for x in key_str if len(x) > 25][0]
            _key_bytes = base64.b64decode(key_str)
            _public_key = RSA.importKey(_key_bytes)
        elif key_str:
            _key_bytes = base64.b64decode(key_str)
            _public_key = RSA.importKey(_key_bytes)
        elif _modulus and _exponent:
            if isinstance(_modulus, str) and isinstance(_exponent, str):
                _modulus = int(_modulus, 16)
                _exponent = int(_exponent, 16)
            _public_key = RSA.construct((_modulus, _exponent))
        else:
            raise Exception("搞什么，给的key不合符类型啊~")
        self.bits_len = int(_public_key.size_in_bits() / 1024 * 100)

        if _PKCS == 1:
            self.cipher = PKCS1_OAEP.new(_public_key)
        elif _PKCS == 2:
            self.cipher = PKCS1_v1_5.new(_public_key)
        else:
            raise Exception("搞什么，给的填充类型不合符啊~")

    def __encrypt(self, plaintext: str) -> bytes:
        # 这里采用分段加密，防止明文太长
        ciphertext = b""
        for i in range(0, len(plaintext), self.bits_len):
            ciphertext += self.cipher.encrypt(plaintext[i: i + self.bits_len].encode())
        return ciphertext

    def encrypt_to_string(self, plaintext: str) -> str:
        # 一般来说，都报错，因为不能保证你的结果就一定能转成str
        return self.__encrypt(plaintext).decode('utf-8')
    
    def encrypt_to_base64(self, plaintext: str) -> str:
        return base64.b64encode(self.__encrypt(plaintext)).decode('utf-8')

    def encrypt_to_hexstr(self, plaintext: str) -> str:
        return binascii.b2a_hex(self.__encrypt(plaintext)).decode('utf-8')

    def encrypt_to_bytes(self, plaintext: str) -> bytes:
        return self.__encrypt(plaintext)


# 使用示例
_plaintext = "Spider 乾坤！"

public_key_str = "MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAok58IrYXjeFjb6hPgrcvKis43ARDVIqowS2AJKivDp4+8uKDCWnjzBZTsuVvwKPzvVCxBzON2/DPpHU3wnRtdKSVzWju7HMKhuLxe04FsVw8+xvZTmguBj4jTczNLSLjK13lQr46J8j7JrmVUlPqGxIL/Bd3HNAIFuarZQkDsgx5fvdNrMbmT4edr1b3A8wRkhfo9tuE5Tmlx0YVUwybzcI6hgLggCfNwwaClXyBt08NbGSIBcKYKjiQErND0EOnWcGyto7EhkpgGRfAeESo3hbmsiabThLd4t9iOWVHFSl+7B0q+1IGFjSo9qkvNdMUI4ZYdIKq+nCHufpuFMl7SwIDAQAB"
# public_key_str = "-----BEGIN PUBLIC KEY-----\nMIGfMA0GCSqGSIb3DQEBAQUAA4GNADCBiQKBgQC5gsH+AA4XWONB5TDcUd+xCz7ejOFHZKlcZDx+pF1i7Gsvi1vjyJoQhRtRSn950x498VUkx7rUxg1/ScBVfrRxQOZ8xFBye3pjAzfb22+RCuYApSVpJ3OO3KsEuKExftz9oFBv3ejxPlYc5yq7YiBO8XlTnQN0Sa4R4qhPO3I2MQIDAQAB\n-----END PUBLIC KEY-----"
# public_key_str = """
# -----BEGIN PUBLIC KEY-----
# MIICIjANBgkqhkiG9w0BAQEFAAOCAg8AMIICCgKCAgEAxswpnvTGXHaDHawDl6Vs
# wYeL3Y05jFB8JWpVSFqk6XzElvKOByeDx1CQ0J4T3L1wb3O35KkSb+37+cBFB0vj
# E510/gQg3n1DLYGy2QYa7rJ5e0sCyHZZBL1f8cN5Ei1PemOCeEk8uKHUe50AEBpf
# 4GsJMSJ2QdZ7Wn46hjex9J/nVi/OPgsLUwzL6Ty92kV/96dWypHxRqBqXsY1WOeZ
# S6nIObKv+5/6nDoatEe5R8L0W7iCAwJbrCP4BsD/CAig0vlk12e0u+CRPJzg11KL
# kIGFCTIY3SgLyAg8RYaP6WQkDrKBCdLqQITvo3KShA+UZM0ftToVqObCG7dspSW/
# CIiwq/RXX9D/PJkvFJjMrpC18yTUZFE0cjVmYh9fr8E3BZZFtgo1/Aoi62QCnK8F
# vpv8hEN4b4m5pyM6WsXDZCmT1EPzCYJgYIaZHNC0eb9YVE3Wh/GAw7JhAsZXF4Ex
# xkH2E1Hm13ae7xoF8ly4h1nsVi8+E80GyIvTHo3+mDD7qZOetQyxV5jG1fhFk+tD
# uf7Jp4Ruu6YOmDT3jW8uSsLIMz9NiB7zunxj+nZU6a6GSgIdyE6gLKXhFQzA0M3d
# kMjNflT2vUnrHocJl9v3EgJKJ/InY0qjFYCfQ2EZKHGwqDw2u0i/NBRzPlbcSClx
# ekX0cxtzTKuVLhoMYrSrVNMCAwEAAQ==
# -----END PUBLIC KEY-----
# """
_rsa = RSAUtilGeneral(key_str=public_key_str)
#
# e = "010001"
# m = '00C1E3934D1614465B33053E7F48EE4EC87B14B95EF88947713D25EECBFF7E74C7977D02DC1D9451F79DD5D1C10C29ACB6A9B4D6FB7D0A0279B6719E1772565F09AF627715919221AEF91899CAE08C0D686D748B20A3603BE2318CA6BC2B59706592A9219D0BF05C9F65023A21D2330807252AE0066D59CEEFA5F2748EA80BAB81'
# rsa = RSAUtil(modulus=m, exponent=e)

# e = 65537
# m = 136153462421446847404340432441046996374735571025589056967906613334049032306309642600950180794472974184474850029075084679952125029724775675860862428869529368335136951744118770626613042094193316007621445630035543273179259178158896311604233203144417656446177150555868699549873157540592293125574640692009097735041
# rsa = RSAUtil(modulus=m, exponent=e)

# 加密
encrypted_text = _rsa.encrypt_to_base64(_plaintext)
# encrypted_text = rsa.encrypt_to_hexstr(_plaintext)
# encrypted_text = rsa.encrypt_to_string(_plaintext)
# encrypted_text = rsa.encrypt_to_bytes(_plaintext)
print("加密结果:", encrypted_text)
```

