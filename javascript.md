# javascript

## 总章
由三部分组成
* 核心(ECMAScript)
* 文档对象模型(DOM)
* 浏览器对象模型(BOM)

### 核心(ECMScript)

由一下基本分组成
* 语法
* 类型
* 语句
* 关键字
* 保留字
* 操作符
* 对象

### 文本对象模型(DOM)

功能使获取所有的html标签，开始标签或者删除标签，并且可以给标签添加事件(点击、拖动)
基于一下接口
* DOM 遍历和范围：可以知道页面中所有的标签；
* DOM 事件：例如给某个图片添加拖动事件，使图片可以随意拖动；
* DOM 样式：可以更改页面中所有元素的样式；如颜色等

### 浏览器对象模型(BOM)

BOM只会处理跟浏览器相关的东西

* 弹出新窗口功能
* 移动、缩放、关闭浏览器窗口功能
* 给用户提供显示器分辨率的功能
* 提供浏览器信息

## 基础

### 书写位置

与CSS相似，嵌入在HTML中，用```<script></script>```标签
规范卸载``body``标签内部，并且保证是在尾部

与CSS相同，写在HTML外部，写在XXX.js文件中，引入标签即可，用```src=""```属性引入

### 注释

与java相同

### 字符串

可以用```" "```也可用```' '```,类似python

### Console

javascript的输出结果在控制台显示，用```console```可以访问控制台，```log()```表示在控制台输出信息
```console.log();```

### 模板字符串

核心为反引号```' '```与占位符```${exprsion}```

#### 反引号

* 作用是将字符串为变量包裹起来

#### 占位符

* 作用是在字符串中插入变量

如：
```javascript
let firstName = "胡";
let lastName = "雪岩";

let say = "大家好，我姓" + firstName + "，名" + lastName;

console.log(say);
```
转换成：
```javascript
let firstName = "胡";
let lastName = "雪岩";

let say = `大家好，我姓${firstName}，名${lastName}`;

console.log(say);
```

### 转义符```(\)```

类似java，想要输出```" "```，需要用转义
如：
```javascript
let str = "华为正式发布操作系统---\"鸿蒙OS\"";
console.log(str);
```

用```\n````换行

### 在字符串中可以使用表达式
如：
```javascript
let number1 = 20;
let number2 = 10;
console.log(`两个数的和是：${number1 + number2} 
两个数的差是：${number1 - number2} 。`);
```

### 可以使用三目运算符

```javascript
let str = `这里是${false ? "浙江" : "江苏"}`;

console.log(str); // 江苏
```

```javascript
let str = `这里是${true ? "江苏" : "浙江"}-${true ? "南京" : "常州"}`;

console.log(str); // 这里是江苏-南京
```

### 变量

定义:```let```与```const```，不需要添加类型(同python)
语法与java类似
```let```定义变量
```const```定义常量

### 数值类型

* 八进制 ```let number1 = 010; // 八进制的8--->0表示八进制```
* 十六进制```let number1 = 0x010; // 十六进制的16--->0x表示十六进制```
* 浮点数
```javascript
let floatNumber1 = 2.0;
let floatNumber2 = 0.4;
let floatNumber3 = .2; // 正确，但是不推荐

let bigNumber = 9.43e7; // 等于94300000
let smallNumber = 3e-7; // 等于0.0000003
```
* 精度丢失
	* 0.1 + 0.2 != 0.3
```javascript
let number1 = 0.1;
let number2 = 0.2;
console.log(number1 + number2); // 0.30000000000000004
```

* NaN (Not a Number) 非数值
```javascript
let a = 'number';
let b = 10;
let c = a / b;
console.log(c); // NaN
console.log(typeof c); // number
```
出现NaN的情况
1. 0/0
2. 字符串乘以数字
3. ```NaN```和任何数进行运算
```javascript
let a = 'number';
let b = 10;
let c = a / b;
// 此时`c`和任何数进行运算结果都是`NaN`
```

> 可以用typeof (变量) 来判断变量类型

### 类型转换

#### 隐式转换

* 数字加字符串，数字隐式转换为字符串
* 数字字符串与数字做非加法运算，字符串隐式转换为数字
* 数字字符串与数字字符串做非加法运算，隐式转换为数字

#### 强制类型转换

##### parseint

* 整数字符串转换为整数
```javascript
let number = "20";
//  将number转换为整数类型
let converNumber = parseInt(number);
console.log(converNumber); // 20
// 判断转换后的数据类型
console.log(typeof converNumber); // number
```
* 小数字符串转换为整数
```javascript
let number = "20.5";
let converNumber = parseInt(number);
console.log(converNumber); // 20  不足21一律按照20算
console.log(typeof converNumber); // number
```
* 小数转换为整数
```javascript
let number = 20.5;
let converNumber = parseInt(number);
console.log(converNumber); // 20
```

##### parseFloat

* 将小数字符串转换为小数
```javascript
let number = "20.9";
let converNumber = parseFloat(number);
console.log(converNumber); // 20.9
console.log(typeof converNumber); // number
```

#### 相等/全等

* 相等：```==``` ——>判断值是否相同
* 全等：```===```——>在相等的基础上还要判断类型是否相同
***推荐使用全等***

#### 自增自减

与Java类似 

#### 布尔类型

与Java类似
不能用and与or，要使用```&&``` 与``` ||```

### 数组

与python类似;
* 在末尾增加元素：变量名.push("内容");
* 在开头增加元素：变量名.unshift("内容");
* 从后往前删：变量名.pop();
* 从前往前删：变量名.shift();
* 删除/替换指定位置：变量名.splice(int x, int y, n);  //x为起始位置，y为步长，n为要替换的值
	* 插入
```javascript
let schools = ['清华大学', '北京大学', '浙江大学', '同济大学'];

schools.splice(2, 0, '江西理工大学');
console.log(schools); //  ["清华大学", "北京大学", "江西理工大学", "浙江大学", "同济大学"]
```
*	* 替换
```javascript
let schools = ['清华大学', '北京大学', '浙江大学', '同济大学'];

schools.splice(2, 1, '江西理工大学');
console.log(schools); // ["清华大学", "北京大学", "江西理工大学", "同济大学"]
```
*	* 覆盖
```javascript
let schools = ['清华大学', '北京大学', '浙江大学', '同济大学'];

schools.splice(2, 2, '江西理工大学');
console.log(schools); // ["清华大学", "北京大学", "江西理工大学"]
```
* 查询：对象名.indexOf("查询值" , n); //n为开始查询位置 ,输出为查询对象的位置，找不到返回-1
```javascript
let schools = ['清华大学', '北京大学', '浙江大学', '同济大学'];

let result = schools.indexOf('大连理工');
console.log(result); // -1
```

```javascript
let schools = ['清华大学', '北京大学', '浙江大学', '同济大学'];

let result = schools.indexOf('浙江大学', 3);
console.log(result); // -1
```