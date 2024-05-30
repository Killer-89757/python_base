# uuid唯一标识符生成

> python/nodejs

### 一、uuid介绍

1. uuid是指通用唯一识别码，全称是Universally Unique Identifier，UUID的目的在于让分布式系统中的节点拥有唯一的标识符，不需要进行集中式的控制，即不需要为每个节点分配唯一的ID，在一般情况下，UUID的概率很大不会重复，可以用于唯一标识符

2. uuid格式为8个十六进制数字，分别用 - 分隔，每 4 个十六进制数字为一组，比如**23e934f0-5745-11ee-b20a-49cf046cc420**

3. uuid当前共有5个版本，每个版本都有不同的生成方式

   - UUIDv1：基于时间戳和MAC地址生成，但同一台机器上不同进程之间可能会有重复

   - UUIDv2：基于DCE安全性的UUID生成，不常用

   - UUIDv3：基于命名空间和名称的MD5散列值生成，名称和命名空间可以随意设定，只要在不同的命名空间中保证名称的唯一性即可

   - UUIDv4：随机生成，所以在同一机器上生成的两个v4 UUID有很小的概率会重复，但在不同机器上生成的UUID几乎可以认为是完全不同的

   - UUIDv5：基于命名空间和名称的SHA-1散列值生成

### 二、uuid生成python版本

```python
import uuid

namespace_uuid = uuid.NAMESPACE_DNS
name = "syy"
v1 = uuid.uuid1() 
v3 = uuid.uuid3(namespace_uuid,name)
v4 = uuid.uuid4()
v5 = uuid.uuid5(namespace_uuid, name)
print(v1, v3, v4, v5)

random_uuid = uuid.uuid4()
print(uuid)
print(random_uuid.hex)
print(random_uuid.int)
print(random_uuid.bytes)
print(random_uuid.urn)
```

### 三、uuid生成js版本

```js
/*
nodejs 提供了一个 node-uuid 模块用于生成 uuid（唯一标识符）
npm install uuid -g  --registry=http://registry.npm.taobao.org
*/

const uuid = require("uuid");
namespace = '1b671a64-40d5-491e-99b0-da01ff1f3341'
console.log("v1", uuid.v1())
console.log("v2", uuid.v3('hello', namespace))
console.log("v3", uuid.v4())
console.log("v5", uuid.v5('hello', namespace))


function ruuid() {
	var s = [];
	var hexDigits = "0123456789abcdef";
	for (var i = 0; i < 36; i++) {
		s[i] = hexDigits.substr(Math.floor(Math.random() * 0x10), 1);
	}
	s[14] = "4"; // bits 12-15 of the time_hi_and_version field to 0010
	s[19] = hexDigits.substr((s[19] & 0x3) | 0x8, 1); // bits 6-7 of the clock_seq_hi_and_reserved to 01
	s[8] = s[13] = s[18] = s[23] = "-";

	var uuid = s.join("");
	return uuid;
}
console.log(ruuid())

function guid() {
	return 'xxxxxxxx-xxxx-4xxx-yxxx-xxxxxxxxxxxx'.replace(/[xy]/g, function (c) {
		var r = Math.random() * 16 | 0,
			v = c == 'x' ? r : (r & 0x3 | 0x8);
		return v.toString(16);
	});
}
console.log(guid())


function guid2() {
	function S4() {
		return (((1 + Math.random()) * 0x10000) | 0).toString(16).substring(1);
	}
	return (S4() + S4() + "-" + S4() + "-" + S4() + "-" + S4() + "-" + S4() + S4() + S4());
}
console.log(guid2())
```

