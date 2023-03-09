# util工具函数


> ![icon-note.gif](public_sys-resources/icon-note.gif) **说明：**
> 本模块首批接口从API version 7开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。


该模块主要提供常用的工具函数，实现字符串编解码（TextEncoder，TextDecoder）、有理数运算（RationalNumber）、缓冲区管理（LruBuffer）、范围判断（Scope）、Base64编解码（Base64）、内置对象类型检查（Types）等功能。


## 导入模块

```
import util from '@ohos.util';
```

## util.printf

printf(format: string,  ...args: Object[]): string

通过式样化字符串对输入的内容按特定格式输出。

**系统能力：** SystemCapability.Utils.Lang

**参数：**
| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| format | string | 是 | 式样化字符串。 |
| ...args | Object[] | 否 | 替换式样化字符串通配符的数据，此参数缺失时，默认返回第一个参数。 |

**返回值：**
| 类型 | 说明 |
| -------- | -------- |
| string | 按特定格式式样化后的字符串。 |

**示例：**
  ```js
  var res = util.printf("%s", "hello world!");
  console.log(res);
  ```


## util.getErrorString

getErrorString(errno: number): string

获取系统错误码对应的详细信息。

**系统能力：** SystemCapability.Utils.Lang

**参数：**
| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| errno | number | 是 | 系统发生错误产生的错误码。 |

**返回值：**
| 类型 | 说明 |
| -------- | -------- |
| string | 错误码对应的详细信息。 |

**示例：**
  ```js
  var errnum = 10; // 10：a system error number
  var result = util.getErrorString(errnum);
  console.log("result = " + result);
  ```


## util.callbackWrapper

callbackWrapper(original: Function): (err: Object, value: Object )=&gt;void

对异步函数进行回调化处理，回调中第一个参数将是拒绝原因（如果 Promise 已解决，则为 null），第二个参数将是已解决的值。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| original | Function | 是 | 异步函数。 |

**返回值：**
| 类型 | 说明 |
| -------- | -------- |
| Function | 返回一个第一个参数是拒绝原因（如果&nbsp;Promise&nbsp;已解决，则为&nbsp;null），第二个参数是已解决的回调函数。 |

**示例：**
  ```js
  async function promiseFn() {
      return Promise.reject('value');
  }
  var cb = util.callbackWrapper(promiseFn);
  cb((err, ret) => {
      console.log(err);
      console.log(ret);
  })
  ```


## util.promiseWrapper

promiseWrapper(original: (err: Object, value: Object) =&gt; void): Object

对异步函数处理并返回一个promise的版本。

**系统能力：** SystemCapability.Utils.Lang

**参数：**
| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| original | Function | 是 | 异步函数。 |

**返回值：**
| 类型 | 说明 |
| -------- | -------- |
| Function | 采用遵循常见的错误优先的回调风格的函数（也就是将&nbsp;(err,&nbsp;value)&nbsp;=&gt;&nbsp;...&nbsp;回调作为最后一个参数），并返回一个返回&nbsp;promise&nbsp;的版本。 |

**示例：**
  ```js
  function aysnFun(str1, str2, callback) {
      if (typeof str1 === 'string' && typeof str2 === 'string') {
          callback(null, str1 + str2);
      } else {
          callback('type err');
      }
  }
  let newPromiseObj = util.promiseWrapper(aysnFun)("Hello", 'World');
  newPromiseObj.then(res => {
      console.log(res);
  })
  ```


## TextDecoder

### 属性

**系统能力：** 以下各项对应的系统能力均为SystemCapability.Utils.Lang。

| 名称 | 参数类型 | 可读 | 可写 | 说明 |
| -------- | -------- | -------- | -------- | -------- |
| encoding | string | 是 | 否 | 编码格式。<br/>-&nbsp;支持格式：utf-8。 |
| fatal | boolean | 是 | 否 | 是否显示致命错误。 |
| ignoreBOM | boolean | 是 | 否 | 是否忽略BOM（byte&nbsp;order&nbsp;marker）标记，默认值为false&nbsp;，表示解码结果包含BOM标记。 |


### constructor

constructor(encoding?: string, options?: { fatal?: boolean; ignoreBOM?: boolean },)

TextDecoder的构造函数。

**系统能力：** SystemCapability.Utils.Lang

**参数：**
| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| encoding | string | 否 | 编码格式。 |
| options | Object | 否 | 编码相关选项参数，存在两个属性fatal和ignoreBOM。 |

  **表1** options

| 名称 | 参数类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| fatal | boolean | 否 | 是否显示致命错误。 |
| ignoreBOM | boolean | 否 | 是否忽略BOM标记。 |

**示例：**
  ```js
  var textDecoder = new util.TextDecoder("utf-8",{ignoreBOM: true});
  ```


### decode

decode(input: Uint8Array, options?: { stream?: false }): string

通过输入参数解码后输出对应文本。

**系统能力：** SystemCapability.Utils.Lang

**参数：**
| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| input | Unit8Array | 是 | 符合格式需要解码的数组。 |
| options | Object | 否 | 解码相关选项参数。 |

  **表2** options

| 名称 | 参数类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| stream | boolean | 否 | 在随后的decode()调用中是否跟随附加数据块。如果以块的形式处理数据，则设置为true；如果处理最后的数据块或数据未分块，则设置为false。默认为false。 |

**返回值：**
| 类型 | 说明 |
| -------- | -------- |
| string | 解码后的数据。 |

**示例：**
  ```js
  var textDecoder = new util.TextDecoder("utf-8",{ignoreBOM: true});
  var result = new Uint8Array(6);
  result[0] = 0xEF;
  result[1] = 0xBB;
  result[2] = 0xBF;
  result[3] = 0x61;
  result[4] = 0x62;
  result[5] = 0x63;
  console.log("input num:");
  var retStr = textDecoder.decode( result , {stream: false});
  console.log("retStr = " + retStr);
  ```


## TextEncoder

### 属性

**系统能力：** 以下各项对应的系统能力均为SystemCapability.Utils.Lang。

| 名称 | 参数类型 | 可读 | 可写 | 说明 |
| -------- | -------- | -------- | -------- | -------- |
| encoding | string | 是 | 否 | 编码格式，默认值是utf-8。 |


### constructor

constructor()

TextEncoder的构造函数。

**系统能力：** SystemCapability.Utils.Lang

**示例：**
  ```js
  var textEncoder = new util.TextEncoder();
  ```


### encode

encode(input?: string): Uint8Array

通过输入参数编码后输出对应文本。

**系统能力：** SystemCapability.Utils.Lang

**参数：**
| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| input | string | 是 | 需要编码的字符串。 |

**返回值：**
| 类型 | 说明 |
| -------- | -------- |
| Uint8Array | 返回编码后的文本。 |

**示例：**
  ```js
  var textEncoder = new util.TextEncoder();
  var buffer = new ArrayBuffer(20);
  var result = new Uint8Array(buffer);
  result = textEncoder.encode("\uD800¥¥");
  ```


### encodeInto

encodeInto(input: string, dest: Uint8Array, ): { read: number; written: number }

放置生成的UTF-8编码文本。

**系统能力：** SystemCapability.Utils.Lang

**参数：**
| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| input | string | 是 | 需要编码的字符串。 |
| dest | Uint8Array | 是 | Uint8Array对象实例，用于将生成的UTF-8编码文本放入其中。 |

**返回值：**
| 类型 | 说明 |
| -------- | -------- |
| Uint8Array | 返回编码后的文本。 |

**示例：**
  ```js
  var that = new util.TextEncoder();
  var buffer = new ArrayBuffer(4);
  this.dest = new Uint8Array(buffer);
  var result = that.encodeInto("abcd", this.dest);
  ```

## RationalNumber<sup>8+</sup>


### constructor<sup>8+</sup>

constructor(numerator: number,denominator: number)

RationalNumber的构造函数。

**系统能力：** SystemCapability.Utils.Lang

**参数：**
| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| numerator | number | 是 | 分子，整数类型。 |
| denominator | number | 是 | 分母，整数类型。 |

**示例：**
  ```js
  var rationalNumber = new util.RationalNumber(1,2);
  ```


### createRationalFromString<sup>8+</sup>

static createRationalFromString​(rationalString: string): RationalNumber​

基于给定的字符串创建一个RationalNumber对象。

**系统能力：** SystemCapability.Utils.Lang

**参数：**
| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| rationalString | string | 是 | 字符串格式。 |

**返回值：**
| 类型 | 说明 |
| -------- | -------- |
| object | 返回有理数类的对象。 |

**示例：**
  ```js
  var rationalNumber = new util.RationalNumber(1,2);
  var rational = rationalNumer.creatRationalFromString("3/4");
  ```


### compareTo<sup>8+</sup>

compareTo​(another: RationalNumber): number​

将当前的RationalNumber对象与给定的对象进行比较。

**系统能力：** SystemCapability.Utils.Lang

**参数：**
| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| another | RationalNumber | 是 | 其他的有理数对象。 |

**返回值：**
| 类型 | 说明 |
| -------- | -------- |
| number | 如果两个对象相等，则返回0；如果给定对象小于当前对象，则返回1；如果给定对象大于当前对象，则返回-1。 |

**示例：**
  ```js
  var rationalNumber = new util.RationalNumber(1,2);
  var rational = rationalNumer.creatRationalFromString("3/4");
  var result = rationalNumber.compareTo(rational);
  ```


### valueOf<sup>8+</sup>

valueOf(): number

以整数形式或者浮点数的形式获取当前RationalNumber对象的值。

**系统能力：** SystemCapability.Utils.Lang

**返回值：**
| 类型 | 说明 |
| -------- | -------- |
| number | 返回整数或者浮点数的值。 |

**示例：**
  ```js
  var rationalNumber = new util.RationalNumber(1,2);
  var result = rationalNumber.valueOf();
  ```


### equals<sup>8+</sup>

equals​(obj: Object): boolean

将当前的RationalNumber对象与给定的对象进行比较是否相等。

**系统能力：** SystemCapability.Utils.Lang

**参数：**
| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| object | Object | 是 | 其他类型对象。 |

**返回值：**
| 类型 | 说明 |
| -------- | -------- |
| boolean | 如果给定对象与当前对象相同，则返回true；否则返回false。 |

**示例：**
  ```js
  var rationalNumber = new util.RationalNumber(1,2);
  var rational = rationalNumer.creatRationalFromString("3/4");
  var result = rationalNumber.equals(rational);
  ```


### getCommonDivisor<sup>8+</sup>

static getCommonDivisor​(number1: number,number2: number): number

获取两个指定整数的最大公约数。

**系统能力：** SystemCapability.Utils.Lang

**参数：**
| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| number1 | number | 是 | 整数类型。 |
| number2 | number | 是 | 整数类型。 |

**返回值：**
| 类型 | 说明 |
| -------- | -------- |
| number | 返回两个给定数字的最大公约数。 |

**示例：**
  ```js
  var rationalNumber = new util.RationalNumber(1,2);
  var result = rationalNumber.getCommonDivisor(4,6);
  ```


### getNumerator<sup>8+</sup>

getNumerator​(): number

获取当前RationalNumber对象的分子。

**系统能力：** SystemCapability.Utils.Lang

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| number | 返回RationalNumber对象的分子的值。 |

**示例：**
  ```js
  var rationalNumber = new util.RationalNumber(1,2);
  var result = rationalNumber.getNumerator();
  ```


### getDenominator<sup>8+</sup>

getDenominator​(): number

获取当前RationalNumber对象的分母。

**系统能力：** SystemCapability.Utils.Lang

**返回值：**
| 类型 | 说明 |
| -------- | -------- |
| number | 返回RationalNumber对象的分母的值。 |

**示例：**
  ```js
  var rationalNumber = new util.RationalNumber(1,2);
  var result = rationalNumber.getDenominator();
  ```


### isZero<sup>8+</sup>

isZero​():boolean

检查当前RationalNumber对象是否为0。

**系统能力：** SystemCapability.Utils.Lang

**返回值：**
| 类型 | 说明 |
| -------- | -------- |
| boolean | 如果当前对象表示的值为0，则返回true；否则返回false。 |

**示例：**
  ```js
  var rationalNumber = new util.RationalNumber(1,2);
  var result = rationalNumber.isZero();
  ```


### isNaN<sup>8+</sup>

isNaN​(): boolean

检查当前RationalNumber对象是否表示非数字(NaN)值。

**系统能力：** SystemCapability.Utils.Lang

**返回值：**
| 类型 | 说明 |
| -------- | -------- |
| boolean | 如果分母和分子都为0，则返回true；否则返回false。 |

**示例：**
  ```js
  var rationalNumber = new util.RationalNumber(1,2);
  var result = rationalNumber.isNaN();
  ```


### isFinite<sup>8+</sup>

isFinite​():boolean

检查当前RationalNumber对象是否表示一个有限值。

**系统能力：** SystemCapability.Utils.Lang

**返回值：**
| 类型 | 说明 |
| -------- | -------- |
| boolean | 如果分母不为0，则返回true；否则返回false。 |

**示例：**
  ```js
  var rationalNumber = new util.RationalNumber(1,2);
  var result = rationalNumber.isFinite();
  ```


### toString<sup>8+</sup>

toString​(): string

获取当前RationalNumber对象的字符串表示形式。

**系统能力：** SystemCapability.Utils.Lang

**返回值：**
| 类型 | 说明 |
| -------- | -------- |
| string | 返回Numerator/Denominator格式的字符串，例如3/5，如果当前对象的分子和分母都为0，则返回NaN。 |

**示例：**
  ```js
  var rationalNumber = new util.RationalNumber(1,2);
  var result = rationalNumber.toString();
  ```

## LruBuffer<sup>8+</sup>

### 属性

**系统能力：** 以下各项对应的系统能力均为SystemCapability.Utils.Lang。

| 名称 | 类型 | 可读 | 可写 | 说明 |
| -------- | -------- | -------- | -------- | -------- |
| length | number | 是 | 否 | 当前缓冲区中值的总数。 |

**示例：**
  ```js
  var pro = new util.LruBuffer();
  pro.put(2,10);
  pro.put(1,8);
  var result = pro.length;
  ```


### constructor<sup>8+</sup>

constructor(capacity?: number)

默认构造函数用于创建一个新的LruBuffer实例，默认容量为64。

**系统能力：** SystemCapability.Utils.Lang

**参数：**
| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| capacity | number | 否 | 指示要为缓冲区自定义的容量。 |

**示例：**
  ```js
  var lrubuffer= new util.LruBuffer();
  ```


### updateCapacity<sup>8+</sup>

updateCapacity(newCapacity: number): void

将缓冲区容量更新为指定容量，如果newCapacity小于或等于0，则抛出异常。

**系统能力：** SystemCapability.Utils.Lang

**参数：**
| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| newCapacity | number | 是 | 指示要为缓冲区自定义的容量。 |

**示例：**
  ```js
  var pro = new util.LruBuffer();
  var result = pro.updateCapacity(100);
  ```


### toString<sup>8+</sup>

toString(): string

返回对象的字符串表示形式。

**系统能力：** SystemCapability.Utils.Lang

**返回值：**
| 类型 | 说明 |
| -------- | -------- |
| string | 返回对象的字符串表示形式。 |

**示例：**
  ```js
  var pro = new util.LruBuffer();
  pro.put(2,10);
  pro.get(2);
  pro.remove(20);
  var result = pro.toString();
  ```


### getCapacity<sup>8+</sup>

getCapacity(): number

获取当前缓冲区的容量。

**系统能力：** SystemCapability.Utils.Lang

**返回值：**
| 类型 | 说明 |
| -------- | -------- |
| number | 返回当前缓冲区的容量。 |

**示例：**
  ```js
  var pro = new util.LruBuffer();
  var result = pro.getCapacity();
  ```


### clear<sup>8+</sup>

clear(): void

从当前缓冲区清除键值对。后续会调用afterRemoval()方法执行后续操作。

**系统能力：** SystemCapability.Utils.Lang

**示例：**
  ```js
  var pro = new util.LruBuffer();
  pro.put(2,10);
  var result = pro.size();
  pro.clear();
  ```


### getCreateCount<sup>8+</sup>

getCreateCount(): number

获取createDefault()返回值的次数。

**系统能力：** SystemCapability.Utils.Lang

**返回值：**
| 类型 | 说明 |
| -------- | -------- |
| number | 返回createDefault()返回值的次数。 |

**示例：**
  ```js
  var pro = new util.LruBuffer();
  pro.put(1,8);
  var result = pro.getCreateCount();
  ```


### getMissCount<sup>8+</sup>

getMissCount(): number

获取查询值不匹配的次数。

**系统能力：** SystemCapability.Utils.Lang

**返回值：**
| 类型 | 说明 |
| -------- | -------- |
| number | 返回查询值不匹配的次数。 |

**示例：**
  ```js
  var pro = new util.LruBuffer();
  pro.put(2,10);
  pro.get(2);
  var result = pro.getMissCount();
  ```


### getRemovalCount<sup>8+</sup>

getRemovalCount(): number

获取从缓冲区中逐出值的次数。

**系统能力：** SystemCapability.Utils.Lang

**返回值：**
| 类型 | 说明 |
| -------- | -------- |
| number | 返回从缓冲区中驱逐的次数。 |

**示例：**
  ```js
  var pro = new util.LruBuffer();
  pro.put(2,10);
  pro.updateCapacity(2);
  pro.put(50,22);
  var result = pro.getRemovalCount();
  ```


### getMatchCount<sup>8+</sup>

getMatchCount(): number

获取查询值匹配成功的次数。

**系统能力：** SystemCapability.Utils.Lang

**返回值：**
| 类型 | 说明 |
| -------- | -------- |
| number | 返回查询值匹配成功的次数。 |

**示例：**
  ```js
  var pro = new util.LruBuffer();
  pro.put(2,10);
  pro.get(2);
  var result = pro.getMatchCount();
  ```


### getPutCount<sup>8+</sup>

getPutCount(): number

获取将值添加到缓冲区的次数。

**系统能力：** SystemCapability.Utils.Lang

**返回值：**
| 类型 | 说明 |
| -------- | -------- |
| number | 返回将值添加到缓冲区的次数。 |

**示例：**
  ```js
  var pro = new util.LruBuffer();
  pro.put(2,10);
  var result = pro.getPutCount();
  ```


### isEmpty<sup>8+</sup>

isEmpty(): boolean

检查当前缓冲区是否为空。

**系统能力：** SystemCapability.Utils.Lang

**返回值：**
| 类型 | 说明 |
| -------- | -------- |
| boolean | 如果当前缓冲区不包含任何值，则返回true。 |

**示例：**
  ```js
  var pro = new util.LruBuffer();
  pro.put(2,10);
  var result = pro.isEmpty();
  ```


### get<sup>8+</sup>

get(key: K): V | undefined

表示要查询的键。

**系统能力：** SystemCapability.Utils.Lang

**参数：**
| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| key | K | 是 | 要查询的键。 |

**返回值：**
| 类型 | 说明 |
| -------- | -------- |
| V&nbsp;\|&nbsp;undefind | 如果指定的键存在于缓冲区中，则返回与键关联的值；否则返回undefined。 |

**示例：**
  ```js
  var pro = new util.LruBuffer();
  pro.put(2,10);
  var result  = pro.get(2);
  ```


### put<sup>8+</sup>

put(key: K,value: V): V

将键值对添加到缓冲区。

**系统能力：** SystemCapability.Utils.Lang

**参数：**
| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| key | K | 是 | 要添加的密钥。 |
| value | V | 是 | 指示与要添加的键关联的值。 |

**返回值：**
| 类型 | 说明 |
| -------- | -------- |
| V | 返回与添加的键关联的值；如果要添加的键已经存在，则返回原始值，如果键或值为空，则抛出此异常。 |

**示例：**
  ```js
  var pro = new util.LruBuffer();
  var result = pro.put(2,10);
  ```


### values<sup>8+</sup>

values(): V[]

获取当前缓冲区中所有值从最近访问到最近最少访问的顺序列表 。

**系统能力：** SystemCapability.Utils.Lang

**返回值：**
| 类型 | 说明 |
| -------- | -------- |
| V&nbsp;[] | 按从最近访问到最近最少访问的顺序返回当前缓冲区中所有值的列表。 |

**示例：**
  ```js
  var pro = new util.LruBuffer();
  pro.put(2,10);
  pro.put(2,"anhu");
  pro.put("afaf","grfb");
  var result = pro.values();
  ```


### keys<sup>8+</sup>

keys(): K[]

获取当前缓冲区中所有键从最近访问到最近最少访问的升序列表。

**系统能力：** SystemCapability.Utils.Lang

**返回值：**
| 类型 | 说明 |
| -------- | -------- |
| K&nbsp;[] | 按升序返回当前缓冲区中所有键的列表，从最近访问到最近最少访问。 |

**示例：**
  ```js
  var pro = new util.LruBuffer();
  pro.put(2,10);
  var result = pro.keys();
  ```


### remove<sup>8+</sup>

remove(key: K): V | undefined

从当前缓冲区中删除指定的键及其关联的值。

**系统能力：** SystemCapability.Utils.Lang

**参数：**
| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| key | K | 是 | 要删除的密钥。 |

**返回值：**
| 类型 | 说明 |
| -------- | -------- |
| V&nbsp;\|&nbsp;undefind | 返回一个包含已删除键值对的Optional对象；如果key不存在，则返回一个空的Optional对象，如果key为null，则抛出异常。 |

**示例：**
  ```js
  var pro = new util.LruBuffer();
  pro.put(2,10);
  var result = pro.remove(20);
  ```


### afterRemoval<sup>8+</sup>

afterRemoval(isEvict: boolean,key: K,value: V,newValue: V): void

删除值后执行后续操作。

**系统能力：** SystemCapability.Utils.Lang

**参数：**
| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| isEvict | boolean | 否 | 因容量不足而调用该方法时，参数值为true，其他情况为false。 |
| key | K | 是 | 表示删除的键。 |
| value | V | 是 | 表示删除的值。 |
| newValue | V | 否 | 如果已调用put方法并且要添加的键已经存在，则参数值是关联的新值。其他情况下参数值为空。 |

**示例：**
  ```js
  var arr = [];
  class ChildLruBuffer extends util.LruBuffer
  {
  	constructor()
  	{
  		super();
  	}
  	static getInstance()
  	{
  		if(this.instance ==  null)
  		{
  			this.instance = new ChildLruBuffer();
  		}
  		return this.instance;  
  	}
  	afterRemoval(isEvict, key, value, newValue)
  	{
  		if (isEvict === false)
  		{
  			arr = [key, value, newValue];
  		}
  	}
  }
  ChildLruBuffer.getInstance().afterRemoval(false,10,30,null);
  ```


### contains<sup>8+</sup>

contains(key: K): boolean

检查当前缓冲区是否包含指定的键。

**系统能力：** SystemCapability.Utils.Lang

**参数：**
| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| key | K | 是 | 表示要检查的键。 |

**返回值：**
| 类型 | 说明 |
| -------- | -------- |
| boolean | 如果缓冲区包含指定的键，则返回&nbsp;true。 |

**示例：**
  ```js
  var pro = new util.LruBuffer();
  pro.put(2,10);
  var result = pro.contains(20);
  ```


### createDefault<sup>8+</sup>

createDefault(key: K): V

如果未计算特定键的值，则执行后续操作，参数表示丢失的键，返回与键关联的值。

**系统能力：** SystemCapability.Utils.Lang

**参数：**
| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| key | K | 是 | 表示丢失的键。 |

**返回值：**
| 类型 | 说明 |
| -------- | -------- |
| V | 返回与键关联的值。 |

**示例：**
  ```js
  var pro = new util.LruBuffer();
  var result = pro.createDefault(50);
  ```


### entries<sup>8+</sup>

entries(): IterableIterator&lt;[K,V]&gt;

允许迭代包含在这个对象中的所有键值对。

**系统能力：** SystemCapability.Utils.Lang

**返回值：**
| 类型 | 说明 |
| -------- | -------- |
| [K,&nbsp;V] | 返回一个可迭代数组。 |

**示例：**
  ```js
  var pro = new util.LruBuffer();
  pro.put(2,10);
  var result = pro.entries();
  ```


### [Symbol.iterator]<sup>8+</sup>

[Symbol.iterator]\(): IterableIterator&lt;[K, V]&gt;

返回一个键值对形式的二维数组。

**系统能力：** SystemCapability.Utils.Lang

**返回值：**
| 类型 | 说明 |
| -------- | -------- |
| [K,&nbsp;V] | 返回一个键值对形式的二维数组。 |

**示例：**
  ```js
  var pro = new util.LruBuffer();
  pro.put(2,10);
  var result = pro[symbol.iterator]();
  ```


## Scope<sup>8+</sup>


### ScopeType<sup>8+</sup>

用于表示范围中的值的类型。该类型的值，类型可以为ScopeComparable或number。

ScopeComparable类型的值需要实现compareTo方法，确保传入的数据具有可比性。
```js
interface ScopeComparable{
    compareTo(other: ScopeComparable): boolean;
}
type ScopeType = ScopeComparable | number;
```


构造新类，实现compareTo方法。后续示例代码中，均通过Temperature，获取[ScopeType](#scopetype8)的实例化对象。


示例：
```js
class Temperature{
    constructor(value){
       // 当使用ts语言开发时，需要补充以下代码：
       // private readonly _temp: Temperature;
       this._temp = value;
    }
    comapreTo(value){
       return this._temp >= value.getTemp();
    }
    getTemp(){
       return this._temp;
    }
    toString(){
       return this._temp.toString();
    }
}
```


### constructor<sup>8+</sup>

constructor(lowerObj: ScopeType, upperObj: ScopeType)

用于创建指定下限和上限的作用域实例的构造函数，返回一个Scope对象。

**系统能力：** SystemCapability.Utils.Lang

**参数：**
| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| lowerObj | [ScopeType](#scopetype8) | 是 | 指定作用域实例的下限。 |
| upperObj | [ScopeType](#scopetype8) | 是 | 指定作用域实例的上限。 |

**示例：**
  ```js
  var tempLower = new Temperature(30);
  var tempUpper = new Temperature(40);
  var range = new util.Scope(tempLower, tempUpper);
  ```


### toString<sup>8+</sup>

toString(): string

该字符串化方法返回一个包含当前范围的字符串表示形式。

**系统能力：** SystemCapability.Utils.Lang

**返回值：**
| 类型 | 说明 |
| -------- | -------- |
| string | 返回包含当前范围对象的字符串表示形式。 |

**示例：**
  ```js
  var tempLower = new Temperature(30);
  var tempUpper = new Temperature(40);
  var range = new util.Scope(tempLower, tempUpper);
  var result = range.toString();
  ```


### intersect<sup>8+</sup>

intersect(range: Scope): Scope

获取给定范围和当前范围的交集。

**系统能力：** SystemCapability.Utils.Lang

**参数：**
| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| range | [Scope](#scope8) | 是 | 传入一个给定范围。 |

**返回值：**
| 类型 | 说明 |
| -------- | -------- |
| [Scope](#scope8) | 返回给定范围和当前范围的交集。 |

**示例：**
  ```js
  var tempLower = new Temperature(30);
  var tempUpper = new Temperature(40);
  var range = new util.Scope(tempLower, tempUpper);
  var tempMiDF = new Temperature(35);
  var tempMidS = new Temperature(39);
  var rangeFir = new util.Scope(tempMiDF, tempMidS);
  range.intersect(rangeFir );
  ```


### intersect<sup>8+</sup>

intersect(lowerObj:ScopeType,upperObj:ScopeType):Scope

获取当前范围与给定下限和上限范围的交集。

**系统能力：** SystemCapability.Utils.Lang

**参数：**
| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| lowerObj | [ScopeType](#scopetype8) | 是 | 给定范围的下限。 |
| upperObj | [ScopeType](#scopetype8) | 是 | 给定范围的上限。 |

**返回值：**
| 类型 | 说明 |
| -------- | -------- |
| [Scope](#scope8) | 返回当前范围与给定下限和上限范围的交集。 |

**示例：**
  ```js
  var tempLower = new Temperature(30);
  var tempUpper = new Temperature(40);
  var tempMiDF = new Temperature(35);
  var tempMidS = new Temperature(39);
  var range = new util.Scope(tempLower, tempUpper);
  var result = range.intersect(tempMiDF, tempMidS);
  ```


### getUpper<sup>8+</sup>

getUpper(): ScopeType

获取当前范围的上限。

**系统能力：** SystemCapability.Utils.Lang

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| [ScopeType](#scopetype8) | 返回当前范围的上限值。 |

**示例：**
  ```js
  var tempLower = new Temperature(30);
  var tempUpper = new Temperature(40);
  var range = new util.Scope(tempLower, tempUpper);
  var result = range.getUpper();
  ```


### getLower<sup>8+</sup>

getLower(): ScopeType

获取当前范围的下限。

**系统能力：** SystemCapability.Utils.Lang

**返回值：**
| 类型 | 说明 |
| -------- | -------- |
| [ScopeType](#scopetype8) | 返回当前范围的下限值。 |

**示例：**
  ```js
  var tempLower = new Temperature(30);
  var tempUpper = new Temperature(40);
  var range = new util.Scope(tempLower, tempUpper);
  var result = range.getLower();
  ```


### expand<sup>8+</sup>

expand(lowerObj: ScopeType,upperObj: ScopeType): Scope

创建并返回包括当前范围和给定下限和上限的并集。

**系统能力：** SystemCapability.Utils.Lang

**参数：**
| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| lowerObj | [ScopeType](#scopetype8) | 是 | 给定范围的下限。 |
| upperObj | [ScopeType](#scopetype8) | 是 | 给定范围的上限。 |

**返回值：**
| 类型 | 说明 |
| -------- | -------- |
| [Scope](#scope8) | 返回当前范围和给定下限和上限的并集。 |

**示例：**

  ```js
  var tempLower = new Temperature(30);
  var tempUpper = new Temperature(40);
  var tempMiDF = new Temperature(35);
  var tempMidS = new Temperature(39);
  var range = new util.Scope(tempLower, tempUpper);
  var result = range.expand(tempMiDF, tempMidS);
  ```


### expand<sup>8+</sup>

expand(range: Scope): Scope

创建并返回包括当前范围和给定范围的并集。

**系统能力：** SystemCapability.Utils.Lang

**参数：**
| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| range | [Scope](#scope8) | 是 | 传入一个给定范围。 |

**返回值：**
| 类型 | 说明 |
| -------- | -------- |
| [Scope](#scope8) | 返回包括当前范围和给定范围的并集。 |

**示例：**
  ```js
  var tempLower = new Temperature(30);
  var tempUpper = new Temperature(40);
  var tempMiDF = new Temperature(35);
  var tempMidS = new Temperature(39);
  var range = new util.Scope(tempLower, tempUpper);
  var rangeFir = new util.Scope(tempMiDF, tempMidS);
  var result = range.expand(rangeFir);
  ```


### expand<sup>8+</sup>

expand(value: ScopeType): Scope

创建并返回包括当前范围和给定值的并集。

**系统能力：** SystemCapability.Utils.Lang

**参数：**
| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| value | [ScopeType](#scopetype8) | 是 | 传入一个给定值。 |

**返回值：**
| 类型 | 说明 |
| -------- | -------- |
| [Scope](#scope8) | 返回包括当前范围和给定值的并集。 |

**示例：**
  ```js
  var tempLower = new Temperature(30);
  var tempUpper = new Temperature(40);
  var tempMiDF = new Temperature(35);
  var range = new util.Scope(tempLower, tempUpper);
  var result = range.expand(tempMiDF);
  ```


### contains<sup>8+</sup>

contains(value: ScopeType): boolean

检查给定value是否包含在当前范围内。

**系统能力：** SystemCapability.Utils.Lang

**参数：**
| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| value | [ScopeType](#scopetype8) | 是 | 传入一个给定值。 |

**返回值：**
| 类型 | 说明 |
| -------- | -------- |
| boolean | 如果给定值包含在当前范围内返回true，否则返回false。 |

**示例：**
  ```js
  var tempLower = new Temperature(30);
  var tempUpper = new Temperature(40);
  var tempMiDF = new Temperature(35);
  var range = new util.Scope(tempLower, tempUpper);
  range.contains(tempMiDF);
  ```


### contains<sup>8+</sup>

contains(range: Scope): boolean

检查给定range是否在当前范围内。

**系统能力：** SystemCapability.Utils.Lang

**参数：**
| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| range | [Scope](#scope8) | 是 | 传入一个给定范围。 |

**返回值：**
| 类型 | 说明 |
| -------- | -------- |
| boolean | 如果给定范围包含在当前范围内返回true，否则返回false。 |

**示例：**
  ```js
  var tempLower = new Temperature(30);
  var tempUpper = new Temperature(40);
  var range = new util.Scope(tempLower, tempUpper);
  var tempLess = new Temperature(20);
  var tempMore = new Temperature(45);
  var rangeSec = new util.Scope(tempLess, tempMore);
  var result = range.contains(rangeSec);
  ```


### clamp<sup>8+</sup>

clamp(value: ScopeType): ScopeType

将给定值限定到当前范围内。

**系统能力：** SystemCapability.Utils.Lang

**参数：**
| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| value | [ScopeType](#scopetype8) | 是 | 传入的给定值。 |

**返回值：**
| 类型 | 说明 |
| -------- | -------- |
| [ScopeType](#scopetype8) | 如果传入的value小于下限，则返回lowerObj；如果大于上限值则返回upperObj；如果在当前范围内，则返回value。 |

**示例：**
  ```js
  var tempLower = new Temperature(30);
  var tempUpper = new Temperature(40);
  var tempMiDF = new Temperature(35);
  var range = new util.Scope(tempLower, tempUpper);
  var result = range.clamp(tempMiDF);
  ```


## Base64<sup>8+</sup>


### constructor<sup>8+</sup>

constructor()

Base64的构造函数。

**系统能力：** SystemCapability.Utils.Lang

**示例：**
  ```js
  var base64 = new  util.Base64();
  ```


### encodeSync<sup>8+</sup>

encodeSync(src: Uint8Array): Uint8Array

通过输入参数编码后输出对应文本。

**系统能力：** SystemCapability.Utils.Lang

**参数：**
| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| src | Uint8Array | 是 | 编码输入Uint8数组。 |

**返回值：**
| 类型 | 说明 |
| -------- | -------- |
| Uint8Array | 返回编码后新分配的Uint8数组。 |

**示例：**
  ```js
  var that = new util.Base64();
  var array = new Uint8Array([115,49,51]);
  var result = that.encodeSync(array);
  ```


### encodeToStringSync<sup>8+</sup>

encodeToStringSync(src: Uint8Array): string

通过输入参数编码后输出对应文本。

**系统能力：** SystemCapability.Utils.Lang

**参数：**
| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| src | Uint8Array | 是 | 编码输入Uint8数组。 |

**返回值：**
| 类型 | 说明 |
| -------- | -------- |
| string | 返回编码后的字符串。 |

**示例：**
  ```js
  var that = new util.Base64();
  var array = new Uint8Array([115,49,51]);
  var result = that.encodeToStringSync(array);
  ```


### decodeSync<sup>8+</sup>

decodeSync(src: Uint8Array | string): Uint8Array

通过输入参数解码后输出对应文本。

**系统能力：** SystemCapability.Utils.Lang

**参数：**
| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| src | Uint8Array&nbsp;\|&nbsp;string | 是 | 解码输入Uint8数组或者字符串。 |

**返回值：**
| 类型 | 说明 |
| -------- | -------- |
| Uint8Array | 返回解码后新分配的Uint8数组。 |

**示例：**
  ```js
  var that = new util.Base64();
  var buff = 'czEz';
  var result = that.decodeSync(buff);
  ```


### encode<sup>8+</sup>

encode(src: Uint8Array): Promise&lt;Uint8Array&gt;

通过输入参数异步编码后输出对应文本。

**系统能力：** SystemCapability.Utils.Lang

**参数：**
| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| src | Uint8Array | 是 | 异步编码输入Uint8数组。 |

**返回值：**
| 类型 | 说明 |
| -------- | -------- |
| Promise&lt;Uint8Array&gt; | 返回异步编码后新分配的Uint8数组。 |

**示例：**
  ```js
  var that = new util.Base64();
  var array = new Uint8Array([115,49,51]);
  var rarray = new Uint8Array([99,122,69,122]);
  that.encode(array).then(val=>{    
      for (var i = 0; i < rarray.length; i++) {        
          console.log(val[i])
      }
  })
  ```


### encodeToString<sup>8+</sup>

encodeToString(src: Uint8Array): Promise&lt;string&gt;

通过输入参数异步编码后输出对应文本。

**系统能力：** SystemCapability.Utils.Lang

**参数：**
| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| src | Uint8Array | 是 | 异步编码输入Uint8数组。 |

**返回值：**
| 类型 | 说明 |
| -------- | -------- |
| Promise&lt;string&gt; | 返回异步编码后的字符串。 |

**示例：**
  ```js
  var that = new util.Base64();
  var array = new Uint8Array([115,49,51]);
  that.encodeToString(array).then(val=>{    
      console.log(val)
  })
  ```


### decode<sup>8+</sup>

decode(src: Uint8Array | string): Promise&lt;Uint8Array&gt;

通过输入参数异步解码后输出对应文本。

**系统能力：** SystemCapability.Utils.Lang

**参数：**
| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| src | Uint8Array&nbsp;\|&nbsp;string | 是 | 异步解码输入Uint8数组或者字符串。 |

**返回值：**
| 类型 | 说明 |
| -------- | -------- |
| Promise&lt;Uint8Array&gt; | 返回异步解码后新分配的Uint8数组。 |

**示例：**
  ```js
  var that = new util.Base64();
  var array = new Uint8Array([99,122,69,122]);
  var rarray = new Uint8Array([115,49,51]);
  that.decode(array).then(val=>{    
      for (var i = 0; i < rarray.length; i++) {        
          console.log(val[i])
      }
  })
  ```


## types<sup>8+</sup>


### constructor<sup>8+</sup>

constructor()

Types的构造函数。

**系统能力：** SystemCapability.Utils.Lang

**示例：**
  ```js
  var type = new util.types();
  ```


### isAnyArrayBuffer<sup>8+</sup>

isAnyArrayBuffer(value: Object): boolean

检查输入的value是否是ArrayBuffer类型。

**系统能力：** SystemCapability.Utils.Lang

**参数：**
| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| value | Object | 是 | 待检测对象。 |

**返回值：**
| 类型 | 说明 |
| -------- | -------- |
| boolean | 判断的结果，如果是ArrayBuffer类型为true，反之为false。 |

**示例：**
  ```js
  var that = new util.types();
  var result = that.isAnyArrayBuffer(new ArrayBuffer([]));
  ```


### isArrayBufferView<sup>8+</sup>

isArrayBufferView(value: Object): boolean

检查输入的value是否是内置ArrayBufferView辅助类型。

ArrayBufferView辅助类型包括：Int8Array、Int16Array、Int32Array、Uint8Array、Uint8ClampedArray、Uint32Array、Float32Array、Float64Array、DataView。

**系统能力：** SystemCapability.Utils.Lang

**参数：**
| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| value | Object | 是 | 待检测对象。 |

**返回值：**
| 类型 | 说明 |
| -------- | -------- |
| boolean | 判断的结果，如果是内置包含的ArrayBufferView辅助类型为true，反之为false。 |

**示例：**
  ```js
  var that = new util.types();
  var result = that.isArrayBufferView(new Int8Array([]));
  ```


### isArgumentsObject<sup>8+</sup>

isArgumentsObject(value: Object): boolean

检查输入的value是否是一个arguments对象类型。

**系统能力：** SystemCapability.Utils.Lang

**参数：**
| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| value | Object | 是 | 待检测对象。 |

**返回值：**
| 类型 | 说明 |
| -------- | -------- |
| boolean | 判断的结果，如果是内置包含的arguments类型为true，反之为false。 |

**示例：**
  ```js
  var that = new util.types();
  function foo() {
      var result = that.isArgumentsObject(arguments);
  }
  var f = foo();
  ```


### isArrayBuffer<sup>8+</sup>

isArrayBuffer(value: Object): boolean

检查输入的value是否是ArrayBuffer类型。

**系统能力：** SystemCapability.Utils.Lang

**参数：**
| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| value | Object | 是 | 待检测对象。 |

**返回值：**
| 类型 | 说明 |
| -------- | -------- |
| boolean | 判断的结果，如果是内置包含的ArrayBuffer类型为true，反之为false。 |

**示例：**
  ```js
  var that = new util.types();
  var result = that.isArrayBuffer(new ArrayBuffer([]));
  ```


### isAsyncFunction<sup>8+</sup>

isAsyncFunction(value: Object): boolean

检查输入的value是否是一个异步函数类型。

**系统能力：** SystemCapability.Utils.Lang

**参数：**
| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| value | Object | 是 | 待检测对象。 |

**返回值：**
| 类型 | 说明 |
| -------- | -------- |
| boolean | 判断的结果，如果是内置包含的异步函数类型为true，反之为false。 |

**示例：**
  ```js
  var that = new util.types();
  var result = that.isAsyncFunction(async function foo() {});
  ```


### isBooleanObject<sup>8+</sup>

isBooleanObject(value: Object): boolean

检查输入的value是否是一个Boolean对象类型。

**系统能力：** SystemCapability.Utils.Lang

**参数：**
| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| value | Object | 是 | 待检测对象。 |

**返回值：**
| 类型 | 说明 |
| -------- | -------- |
| boolean | 判断的结果，如果是内置包含的Boolean对象类型为true，反之为false。 |

**示例：**
  ```js
  var that = new util.types();
  var result = that.isBooleanObject(new Boolean(true));
  ```


### isBoxedPrimitive<sup>8+</sup>

isBoxedPrimitive(value: Object): boolean

检查输入的value是否是Boolean或Number或String或Symbol对象类型。

**系统能力：** SystemCapability.Utils.Lang

**参数：**
| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| value | Object | 是 | 待检测对象。 |

**返回值：**
| 类型 | 说明 |
| -------- | -------- |
| boolean | 判断的结果，如果是内置包含的Boolean或Number或String或Symbol对象类型为true，反之为false。 |

**示例：**
  ```js
  var that = new util.types();
  var result = that.isBoxedPrimitive(new Boolean(false));
  ```


### isDataView<sup>8+</sup>

isDataView(value: Object): boolean

检查输入的value是否是DataView类型。

**系统能力：** SystemCapability.Utils.Lang

**参数：**
| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| value | Object | 是 | 待检测对象。 |

**返回值：**
| 类型 | 说明 |
| -------- | -------- |
| boolean | 判断的结果，如果是内置包含的DataView对象类型为true，反之为false。 |

**示例：**
  ```js
  var that = new util.types();
  const ab = new ArrayBuffer(20);
  var result = that.isDataView(new DataView(ab));
  ```


### isDate<sup>8+</sup>

isDate(value: Object): boolean

检查输入的value是否是Date类型。

**系统能力：** SystemCapability.Utils.Lang

**参数：**
| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| value | Object | 是 | 待检测对象。 |

**返回值：**
| 类型 | 说明 |
| -------- | -------- |
| boolean | 判断的结果，如果是内置包含的Date对象类型为true，反之为false。 |

**示例：**
  ```js
  var that = new util.types();
  var result = that.isDate(new Date());
  ```


### isExternal<sup>8+</sup>

isExternal(value: Object): boolean

检查输入的value是否是native External类型。

**系统能力：** SystemCapability.Utils.Lang

**参数：**
| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| value | Object | 是 | 待检测对象。 |

**返回值：**
| 类型 | 说明 |
| -------- | -------- |
| boolean | 判断的结果，如果是内置包含native&nbsp;External类型为true，反之为false。 |

**示例：**
  ```js
  var that = new util.types();
  const data = util.createExternalType();
  var result = that.isExternal(data);
  ```


### isFloat32Array<sup>8+</sup>

isFloat32Array(value: Object): boolean

检查输入的value是否是Float32Array数组类型。

**系统能力：** SystemCapability.Utils.Lang

**参数：**
| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| value | Object | 是 | 待检测对象。 |

**返回值：**
| 类型 | 说明 |
| -------- | -------- |
| boolean | 判断的结果，如果是内置包含的Float32Array数组类型为true，反之为false。 |

**示例：**
  ```js
  var that = new util.types();
  var result = that.isFloat32Array(new Float32Array());
  ```


### isFloat64Array<sup>8+</sup>

isFloat64Array(value: Object): boolean

检查输入的value是否是Float64Array数组类型。

**系统能力：** SystemCapability.Utils.Lang

**参数：**
| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| value | Object | 是 | 待检测对象。 |

**返回值：**
| 类型 | 说明 |
| -------- | -------- |
| boolean | 判断的结果，如果是内置包含的Float64Array数组类型为true，反之为false。 |

**示例：**
  ```js
  var that = new util.types();
  var result = that.isFloat64Array(new Float64Array());
  ```


### isGeneratorFunction<sup>8+</sup>

isGeneratorFunction(value: Object): boolean

检查输入的value是否是generator函数类型。

**系统能力：** SystemCapability.Utils.Lang

**参数：**
| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| value | Object | 是 | 待检测对象。 |

**返回值：**
| 类型 | 说明 |
| -------- | -------- |
| boolean | 判断的结果，如果是内置包含的generator函数类型为true，反之为false。 |

**示例：**
  ```js
  var that = new util.types();
  var result = that.isGeneratorFunction(function* foo() {});
  ```


### isGeneratorObject<sup>8+</sup>

isGeneratorObject(value: Object): boolean

检查输入的value是否是generator对象类型。

**系统能力：** SystemCapability.Utils.Lang

**参数：**
| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| value | Object | 是 | 待检测对象。 |

**返回值：**
| 类型 | 说明 |
| -------- | -------- |
| boolean | 判断的结果，如果是内置包含的generator对象类型为true，反之为false。 |

**示例：**
  ```js
  var that = new util.types();
  function* foo() {}
  const generator = foo();
  var result = that.isGeneratorObject(generator);
  ```


### isInt8Array<sup>8+</sup>

isInt8Array(value: Object): boolean

检查输入的value是否是Int8Array数组类型。

**系统能力：** SystemCapability.Utils.Lang

**参数：**
| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| value | Object | 是 | 待检测对象。 |

**返回值：**
| 类型 | 说明 |
| -------- | -------- |
| boolean | 判断的结果，如果是内置包含的Int8Array数组类型为true，反之为false。 |

**示例：**
  ```js
  var that = new util.types();
  var result = that.isInt8Array(new Int8Array([]));
  ```


### isInt16Array<sup>8+</sup>

isInt16Array(value: Object): boolean

检查输入的value是否是Int16Array数组类型。

**系统能力：** SystemCapability.Utils.Lang

**参数：**
| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| value | Object | 是 | 待检测对象。 |

**返回值：**
| 类型 | 说明 |
| -------- | -------- |
| boolean | 判断的结果，如果是内置包含的Int16Array数组类型为true，反之为false。 |

**示例：**
  ```js
  var that = new util.types();
  var result = that.isInt16Array(new Int16Array([]));
  ```


### isInt32Array<sup>8+</sup>

isInt32Array(value: Object): boolean

检查输入的value是否是Int32Array数组类型。

**系统能力：** SystemCapability.Utils.Lang

**参数：**
| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| value | Object | 是 | 待检测对象。 |

**返回值：**
| 类型 | 说明 |
| -------- | -------- |
| boolean | 判断的结果，如果是内置包含的Int32Array数组类型为true，反之为false。 |

**示例：**
  ```js
  var that = new util.types();
  var result = that.isInt32Array(new Int32Array([]));
  ```


### isMap<sup>8+</sup>

isMap(value: Object): boolean

检查输入的value是否是Map类型。

**系统能力：** SystemCapability.Utils.Lang

**参数：**
| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| value | Object | 是 | 待检测对象。 |

**返回值：**
| 类型 | 说明 |
| -------- | -------- |
| boolean | 判断的结果，如果是内置包含的Map类型为true，反之为false。 |

**示例：**
  ```js
  var that = new util.types();
  var result = that.isMap(new Map());
  ```


### isMapIterator<sup>8+</sup>

isMapIterator(value: Object): boolean

检查输入的value是否是Map的Iterator类型。

**系统能力：** SystemCapability.Utils.Lang

**参数：**
| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| value | Object | 是 | 待检测对象。 |

**返回值：**
| 类型 | 说明 |
| -------- | -------- |
| boolean | 判断的结果，如果是内置包含的Map的Iterator类型为true，反之为false。 |

**示例：**
  ```js
  var that = new util.types();
  const map = new Map();
  var result = that.isMapIterator(map.keys());
  ```


### isNativeError<sup>8+</sup>

isNativeError(value: Object): boolean

检查输入的value是否是Error类型。

**系统能力：** SystemCapability.Utils.Lang

**参数：**
| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| value | Object | 是 | 待检测对象。 |

**返回值：**
| 类型 | 说明 |
| -------- | -------- |
| boolean | 判断的结果，如果是内置包含的Error类型为true，反之为false。 |

**示例：**
  ```js
  var that = new util.types();
  var result = that.isNativeError(new TypeError());
  ```


### isNumberObject<sup>8+</sup>

isNumberObject(value: Object): boolean

检查输入的value是否是Number对象类型。

**系统能力：** SystemCapability.Utils.Lang

**参数：**
| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| value | Object | 是 | 待检测对象。 |

**返回值：**
| 类型 | 说明 |
| -------- | -------- |
| boolean | 判断的结果，如果是内置包含的Number对象类型为true，反之为false。 |

**示例：**
  ```js
  var that = new util.types();
  var result = that.isNumberObject(new Number(0));
  ```


### isPromise<sup>8+</sup>

isPromise(value: Object): boolean

检查输入的value是否是Promise类型。

**系统能力：** SystemCapability.Utils.Lang

**参数：**
| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| value | Object | 是 | 待检测对象。 |

**返回值：**
| 类型 | 说明 |
| -------- | -------- |
| boolean | 判断的结果，如果是内置包含的Promise类型为true，反之为false。 |

**示例：**
  ```js
  var that = new util.types();
  var result = that.isPromise(Promise.resolve(1));
  ```


### isProxy<sup>8+</sup>

isProxy(value: Object): boolean

检查输入的value是否是Proxy类型。

**系统能力：** SystemCapability.Utils.Lang

**参数：**
| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| value | Object | 是 | 待检测对象。 |

**返回值：**
| 类型 | 说明 |
| -------- | -------- |
| boolean | 判断的结果，如果是内置包含的Proxy类型为true，反之为false。 |

**示例：**
  ```js
  var that = new util.types();
  const target = {};
  const proxy = new Proxy(target, {});
  var result = that.isProxy(proxy);
  ```


### isRegExp<sup>8+</sup>

isRegExp(value: Object): boolean

检查输入的value是否是RegExp类型。

**系统能力：** SystemCapability.Utils.Lang

**参数：**
| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| value | Object | 是 | 待检测对象。 |

**返回值：**
| 类型 | 说明 |
| -------- | -------- |
| boolean | 判断的结果，如果是内置包含的RegExp类型为true，反之为false。 |

**示例：**
  ```js
  var that = new util.types();
  var result = that.isRegExp(new RegExp('abc'));
  ```


### isSet<sup>8+</sup>

isSet(value: Object): boolean

检查输入的value是否是Set类型。

**系统能力：** SystemCapability.Utils.Lang

**参数：**
| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| value | Object | 是 | 待检测对象。 |

**返回值：**
| 类型 | 说明 |
| -------- | -------- |
| boolean | 判断的结果，如果是内置包含的Set类型为true，反之为false。 |

**示例：**
  ```js
  var that = new util.types();
  var result = that.isSet(new Set());
  ```


### isSetIterator<sup>8+</sup>

isSetIterator(value: Object): boolean

检查输入的value是否是Set的Iterator类型。

**系统能力：** SystemCapability.Utils.Lang

**参数：**
| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| value | Object | 是 | 待检测对象。 |

**返回值：**
| 类型 | 说明 |
| -------- | -------- |
| boolean | 判断的结果，如果是内置包含的Set的Iterator类型为true，反之为false。 |

**示例：**
  ```js
  var that = new util.types();
  const set = new Set();
  var result = that.isSetIterator(set.keys());
  ```


### isStringObject<sup>8+</sup>

isStringObject(value: Object): boolean

检查输入的value是否是String对象类型。

**系统能力：** SystemCapability.Utils.Lang

**参数：**
| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| value | Object | 是 | 待检测对象。 |

**返回值：**
| 类型 | 说明 |
| -------- | -------- |
| boolean | 判断的结果，如果是内置包含的String对象类型为true，反之为false。 |

**示例：**
  ```js
  var that = new util.types();
  var result = that.isStringObject(new String('foo'));
  ```


### isSymbolObjec<sup>8+</sup>

isSymbolObject(value: Object): boolean

检查输入的value是否是Symbol对象类型。

**系统能力：** SystemCapability.Utils.Lang

**参数：**
| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| value | Object | 是 | 待检测对象。 |

**返回值：**
| 类型 | 说明 |
| -------- | -------- |
| boolean | 判断的结果，如果是内置包含的Symbol对象类型为true，反之为false。 |

**示例：**
  ```js
  var that = new util.types();
  const symbols = Symbol('foo');
  var result = that.isSymbolObject(Object(symbols));
  ```


### isTypedArray<sup>8+</sup>

isTypedArray(value: Object): boolean

检查输入的value是否是TypedArray类型的辅助类型。

TypedArray类型的辅助类型，包括Int8Array、Int16Array、Int32Array、Uint8Array、Uint8ClampedArray、Uint16Array、Uint32Array、Float32Array、Float64Array、DataView。

**系统能力：** SystemCapability.Utils.Lang

**参数：**
| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| value | Object | 是 | 待检测对象。 |

**返回值：**
| 类型 | 说明 |
| -------- | -------- |
| boolean | 判断的结果，如果是内置包含的TypedArray包含的类型为true，反之为false。 |

**示例：**
  ```js
  var that = new util.types();
  var result = that.isTypedArray(new Float64Array([]));
  ```


### isUint8Array<sup>8+</sup>

isUint8Array(value: Object): boolean

检查输入的value是否是Uint8Array数组类型。

**系统能力：** SystemCapability.Utils.Lang

**参数：**
| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| value | Object | 是 | 待检测对象。 |

**返回值：**
| 类型 | 说明 |
| -------- | -------- |
| boolean | 判断的结果，如果是内置包含的Uint8Array数组类型为true，反之为false。 |

**示例：**
  ```js
  var that = new util.types();
  var result = that.isUint8Array(new Uint8Array([]));
  ```


### isUint8ClampedArray<sup>8+</sup>

isUint8ClampedArray(value: Object): boolean

检查输入的value是否是Uint8ClampedArray数组类型。

**系统能力：** SystemCapability.Utils.Lang

**参数：**
| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| value | Object | 是 | 待检测对象。 |

**返回值：**
| 类型 | 说明 |
| -------- | -------- |
| boolean | 判断的结果，如果是内置包含的Uint8ClampedArray数组类型为true，反之为false。 |

**示例：**
  ```js
  var that = new util.types();
  var result = that.isUint8ClampedArray(new Uint8ClampedArray([]));
  ```


### isUint16Array<sup>8+</sup>

isUint16Array(value: Object): boolean

检查输入的value是否是Uint16Array数组类型。

**系统能力：** SystemCapability.Utils.Lang

**参数：**
| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| value | Object | 是 | 待检测对象。 |

**返回值：**
| 类型 | 说明 |
| -------- | -------- |
| boolean | 判断的结果，如果是内置包含的Uint16Array数组类型为true，反之为false。 |

**示例：**
  ```js
  var that = new util.types();
  var result = that.isUint16Array(new Uint16Array([]));
  ```


### isUint32Array<sup>8+</sup>

isUint32Array(value: Object): boolean

检查输入的value是否是Uint32Array数组类型。

**系统能力：** SystemCapability.Utils.Lang

**参数：**
| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| value | Object | 是 | 待检测对象。 |

**返回值：**
| 类型 | 说明 |
| -------- | -------- |
| boolean | 判断的结果，如果是内置包含的Uint32Array数组类型为true，反之为false。 |

**示例：**
  ```js
  var that = new util.types();
  var result = that.isUint32Array(new Uint32Array([]));
  ```


### isWeakMap<sup>8+</sup>

isWeakMap(value: Object): boolean

检查输入的value是否是WeakMap类型。

**系统能力：** SystemCapability.Utils.Lang

**参数：**
| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| value | Object | 是 | 待检测对象。 |

**返回值：**
| 类型 | 说明 |
| -------- | -------- |
| boolean | 判断的结果，如果是内置包含的WeakMap类型为true，反之为false。 |

**示例：**
  ```js
  var that = new util.types();
  var result = that.isWeakMap(new WeakMap());
  ```


### isWeakSet<sup>8+</sup>

isWeakSet(value: Object): boolean

检查输入的value是否是WeakSet类型。

**系统能力：** SystemCapability.Utils.Lang

**参数：**
| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| value | Object | 是 | 待检测对象。 |

**返回值：**
| 类型 | 说明 |
| -------- | -------- |
| boolean | 判断的结果，如果是内置包含的WeakSet类型为true，反之为false。 |

**示例：**
  ```js
  var that = new util.types();
  var result = that.isWeakSet(new WeakSet());
  ```
