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

### for 循环

* 写法与JAVA类似
```javascript
let peppaFamily = ["佩奇", "乔治", "猪妈妈", "猪爸爸"];

for (let i = 0; i < peppaFamily.length; i++) {
  console.log(peppaFamily[i]);
}
```
* for...in
```javascript
let peppaFamily = ["佩奇", "乔治", "猪妈妈", "猪爸爸"];

for (let i in peppaFamily) {
  console.log(peppaFamily[i]);
}
```
* for...of 
```javascript
let peppaFamily = ["佩奇", "乔治", "猪妈妈", "猪爸爸"];

for (let item of peppaFamily) {
  console.log(item);
}
```
> for...in 与for...of 的区别:for....in遍历数组下标;for...of遍历数组值

### while 循环
* 与JAVA类似

```javascript
let peppaFriends = ['小狗丹尼', '小猫坎迪', '狐狸弗雷迪', '小狼温蒂', '大象艾米丽', '小兔瑞贝卡', '小羊苏西'];

let i = 0;
while (i < peppaFriends.length ) {
  console.log(peppaFriends[i]);
  i++;
}
```

* do...while

```javascript
let i = 0;

do {
  console.log(i); // 输出：0
  i++;
} while (i < 0 );
```
### 函数

#### 随机函数
Math.random()  -> [0 , 1)

#### 自定义函数

* 用function声明
* es6中声明
```javascript
let print = () => {
  console.log("JavaScript 真有趣");
};
```
* function函数声明后会被提升到代码头部 -----函数声明可以写在调用后面
* function 声明```{}```后不需要加```;```
* es6函数表达式结尾```{}```后要加```;```
* function 声明有提升
* es6函数声明没有提升
* 重复声明会覆盖
* 函数只使用一次用IIFE
```javascript
(function() {
  console.log("这个函数只执行一次");
})();
```

#### 内置函数——计时器

```javascript
console.log(1);

/**
 * 第一个参数是代码，注意代码需用引号包裹，否则会立即执行代码
 * 第二个参数是 1000，即 1000ms 后执行 console.log(2)
 */
setTimeout('console.log(2)', 1000);

/**
 * 第一个参数是匿名函数
 * 第二个参数是 2000，即 2s 后执行 console.log(3)
 */
setTimeout(function () {
  console.log(3);
}, 2000);

// 第一个参数是函数名，注意函数名后不要加小括号“()”，否则会立即执行 print4
setTimeout(print4, 3000);

console.log(5);

function print4() {
  console.log(4);
}
```

* setTimeout是一个“回调函数”，将函数指针传入，当条件成立时调用指针对应的函数
* setTimeout只能调用一次

```javascript
let timer = setInterval(print, 1000);

function print() {
  console.log(1);
}
```
* setInterval为无限调用函数

### 对象

```javascript
let person = {
  name: 'henry',
  age: 18,
  run: function() {
    console.log('running');
  }
}
person.run();
```

* 创建
```javascript
// 第一步：创建构造函数
function People(name, age) {
  this.name = name;
  this.age = age;
}

// 第二步：通过 new 创建对象实例
let person = new People('henry', 18);
console.log(person);
```

* 属性读取
```javascript
let person = {
  name: 'henry',
  age: 18
}

console.log(person.name); //henry
console.log(person['name']); //henry
```

```javascript
let person = {
  name: 'henry',
  age: 18
}

let variable = 'name';
console.log(person[variable]);

variable = 'age';
console.log(person[variable]);
```

* 属性赋值

```javascript
let person = {
  name: 'henry',
  age: 18
}

person.name = 'tom';
person['age'] = 10

console.log(person.name);
console.log(person.age);
```

* 属性查看

```javascript
let person = {
  name: 'henry',
  age: 18
}

console.log(Object.keys(person));
```

* 属性删除和增加

// 删除
```javascript
let person = {
  name: 'henry',
  age: 18
}

delete person.name;

console.log(person);
```
// 增加
```javascript
let person = {
  name: 'henry',
  age: 18
}

person.gender = 'male';
```
#### 遍历对象属性

* ```for...in```

```javascript

let person = {
  name: 'henry',
  age: 18,
}

for (let key in person) {
  console.log('键名：' + key + '；键值：' + person[key]);
}
```

* ```Object.keys```

```javascript
let person = {
  name: 'henry',
  age: 18,
}

let keys = Object.keys(person);

for (let i = 0; i < keys.length; i++) {
  console.log('键名：' + keys[i] + '；键值：' + person[keys[i]]);
}
```

### 继承

#### 判断属性是否存在

* 使用 ```hasOwnProperty```方法 ---> 由Object对象提供（Object是所有对象的原型）
* '属性名' in 对象 : 返回true of false 判断是否存在属性

#### 对象转化

* JSON --> Object
```javascript
const obj = JSON.parser(jsonstr);
```

* Object --> JSON
```javascript
const jsonstr2 = JSON.stringfy(object);
```
[Map 与 Object](https://www.jianshu.com/p/94cf51649517)

#### 内置对象(Math 、 Storage)

##### Storage对象

* Storage 接口用于脚本在浏览器中保存数据。两个对象部署了这个接口 window.sessionStorage 与 window.localStorage
* sessionStorage 保存的数据用于浏览器一次会话(session) ， 当会话结束(通常是窗口关闭)，数据会被清空
* localStorage 保存的数据长期存在，下一次访问该网址的时候，网页可以直接读取以前保存的数据。

* 数据存入 : ```setltem```
```javascript
window.localStorage.setItem(key, value);
```
> 如果要存入的数据不是字符串最好先转化为字符串类型
```javascript
const obj = {
  name: 'henry',
  age: 18
}
const value = JSON.stringify(obj);
window.localStorage.setItem('myLocalStorage', value);
```
* 数据读取
```javascript
window.localStorage.getItem(key);
```

* 清除缓存
```javascript
window.localStorage.clear();
```

##### String(内置对象)

* length(属性值)
```let len = 'here is an apple'.length;```
* 查找字符: indexOf()

查找某个字符是否存在
```javascript
let str = 'here is an apple';
const index = str.indexOf('an');
console.log(index);
```
若存在返回该字符首字符在的位置，否则返回-1
* trim()
去掉两端空格
```javascript
// 'here' 之前有一个空格，'apple' 之后有三个空格
let str = ' here is an apple   ';
const trimedStr = str.trim();
console.log(str.length);
console.log(trimedStr.length);
```
> trim 不会改变原字符，而是复制一个处理过后的字符串返回

* 截取字符串：substring/substr

substring第二个值为右限
substr第二个值为截取长度
```javascript
let url = 'https://www.youkeda.com/userhome#collect';

// 首先找到 # 后第一个字母的下标
const index = url.indexOf('#') + 1;

// 有 hash 才能进行截取，没有就直接提示不存在
if (index) {
  // 用 substring 截取字符串
  const hash1 = url.substring(index, url.length);

  // 计算 hash 的长度
  const lenHash = url.length - index;
  // 用 substr 截取字符串
  const hash2 = url.substr(index, lenHash);

  console.log(hash1);
  console.log(hash2);
} else {
  console.log('不存在 hash');
}
```
* split
分割字符串
```javascript
const splitedStr = 'a|b|c'.split('|');
console.log(splitedStr);
```
返回一个由分割出来的子字符串形成的一个数组
> split也只是复制一个处理过后的返回值，不改变原字符串

##### Array(内置对象)

* join()
连接数组
```javascript
let arr = [1, 2, 3, 4];

arr.join(" "); // '1 2 3 4'
arr.join(" | "); // "1 | 2 | 3 | 4"
arr.join(); // "1,2,3,4"
```
* reverse()
倒置排序
```javascript
let arr = ["a", "b", "c"];

arr.reverse(); // ["c", "b", "a"]
arr; // ["c", "b", "a"]
```
* sort()
排序
```javascript
let arr = [
  { name: "jenny", age: 18 },
  { name: "tom", age: 10 },
  { name: "mary", age: 40 },
];

arr.sort(function (a, b) {
  return a.age - b.age;
}); 

console.log(arr);
```
sort()内要传入参数必须为一个函数，函数中a,b为将要比较的两个值，返回正则左边的a排在右边的b的后面，反之为负a排在b的前面，相等不变。

* map/forEach
  遍历

  * 有返回值的遍历:map
  ```javascript
    let arr = [
    { name: "jenny", age: 18 },
    { name: "tom", age: 10 },
    { name: "mary", age: 40 },
    ];
	// elem: 数组成员
	// index: 成员下标
	// a: 整个数组
	const handledArr = arr.map(function (elem, index, a) {
  		elem.age += 1;
  		console.log(elem, index, a);
  		return elem.name;
	});
	console.log(arr);
	console.log(handledArr);
	```
	* forEach
	无返回值
~~~javascript
const handledArr = arr.forEach(function (elem, index, a){
	elem.age += 1;
	console.log(elem, index, a);
	return elem.name;
	});
	
console.log(handledArr);	
~~~
此程序输出```undefined```

##### Date(内置对象)
* new Date()
获取当前时间
```javascript
let now = new Date();
console.log(now);
```
* 传入参数可构造特定的时间
```javascript
// 传入表示“年月日时分秒”的数字
let dt1 = new Date(2020, 0, 6, 0, 0, 0);
console.log(dt1);

// 传入日期字符串
let dt2 = new Date("2020-1-6");
console.log(dt2);

// 传入距离国际标准时间的毫秒数
let dt3 = new Date(1578240000000);
console.log(dt3);
```
* 日期运算

	* 两个时间对象相减返回值为毫秒数差
	* 用```<```与```>```比较时间早晚
* Date.parse()
解析日期字符串，返回该时间距离时间零点(1970年1月1日00:00:00)的毫秒数
```javascript
let dt = Date.parse("2020-1-6");
console.log(dt); // 1578240000000
```
* 类型转换
	* to方法 ---> toJSON()
	* get方法
```javascript
let dt = new Date();
dt.getTime(); // 返回实例距离1970年1月1日00:00:00的毫秒数。
dt.getDate(); // 返回实例对象对应每个月的几号（从1开始）。
dt.getDay(); // 返回星期几，星期日为0，星期一为1，以此类推。
dt.getFullYear(); // 返回四位的年份。
dt.getMonth(); // 返回月份（0表示1月，11表示12月）。
dt.getHours(); // 返回小时（0-23）。
dt.getMilliseconds(); // 返回毫秒（0-999）。
dt.getMinutes(); // 返回分钟（0-59）。
dt.getSeconds(); // 返回秒（0-59）。
```
> 除了日期外其他的时间的都是从0开始的
* set方法
设置对象的时间
```javascript
let dt = new Date();
dt.setTime(ms); // 设置实例距离1970年1月1日00:00:00的毫秒数。
dt.setDate(date); // 设置实例对象对应每个月的几号（从1开始）。
dt.setFullYear(year); // 设置四位的年份。
dt.setMonth(month); // 设置月份（0表示1月，11表示12月）。
dt.setHours(hour); // 设置小时（0-23）。
dt.setMilliseconds(ms); // 设置毫秒（0-999）。
dt.setMinutes(min); // 设置分钟（0-59）。
dt.setSeconds(sec); // 设置秒（0-59）。
```

> 没有setDay方法，星期是通过计算得到的

![Date](https://qgt-document.oss-cn-beijing.aliyuncs.com/P3-4-HTML-CSS/7/3.jpg?x-oss-process=image/resize,w_800/watermark,image_d2F0ZXJtYXNrLnBuZz94LW9zcy1wcm9jZXNzPWltYWdlL3Jlc2l6ZSx3XzEwMA==,t_60,g_se,x_10,y_10)

### BOM

> 浏览器对象模型

* 对象 -> window（窗口）、navigator（浏览器）、history（历史）、screen（显示屏幕）、location（地址）

> screen 电脑唯一；
> navigator 是整个浏览器唯一的，如果有多个浏览器就会有多个navigator；
> window 是每个网页唯一的，每个网页都有一个独立的window；
> history,location 是每个网页的信息，当然也是网页唯一的；

#### window 对象是浏览器中默认对象，可以隐式引用window对象的属性和方法
如：
```javascript
console.log('优课达');
window.console.log('优课达');

console.log(navigator);
console.log(window.navigator);

function hello() {}
console.log(hello);
console.log(window.hello);
```

#### location
![location](https://style.youkeda.com/img/course/f4/8/3.jpeg?x-oss-process=image/resize,w_800/watermark,image_d2F0ZXJtYXNrLnBuZz94LW9zcy1wcm9jZXNzPWltYWdlL3Jlc2l6ZSx3XzEwMA==,t_60,g_se,x_10,y_10)

* reload 方法，用于刷新页面，可以用setTimeout来进行延迟操作
```javascript
setTimeout(function () {
  window.location.reload();
}, 3000);
```
> setTimeout 只会执行一次，但在此会不断被执行，因为网页每次被reload（刷新）都会重新执行js文件，达到不断刷新的效果

* 跳转到新的页面

刷新后将会跳转到新的页面
```javascript
window.location = 'https://www.youkeda.com';
```

#### history

储存会话记录
储存到一个栈数组中
* back()
  对应浏览器左键头

* forward()
  对应浏览器右箭头

#### navigator

* useragent代表用户数据

#### screen

### DOM

文档对象模型

* web 页面
HTML和CSS绘制的页面，也称为文档

* 脚本或编程语言
#### DOM映射
DOM树：
![DOM树](https://style.youkeda.com/img/course/f4/9/1.jpeg?x-oss-process=image/resize,w_800/watermark,image_d2F0ZXJtYXNrLnBuZz94LW9zcy1wcm9jZXNzPWltYWdlL3Jlc2l6ZSx3XzEwMA==,t_60,g_se,x_10,y_10)

* DOM节点（Node/Element）
每个HTML标签
* 分支称为儿子节点
* 之后是孙子节点
* 所有其父标签为祖先节点
* 平行的为兄弟节点

#### 访问
```window.document;```

* 选择器查询

```querySelector()```

```javascript
document.querySelector('main .core .subtitle');
```

* 迭代查询
```javascript
let subtitle = document.querySelector('main .core .subtitle');
console.log(subtitle.querySelector('a'));
```

* 选择器全量查询
查询所有满足条件的节点
```javascript
document.querySelectorAll('input');
```

* 其他
```getElementById();``` 根据Id查询某个节点
```getElementsByClassName();```根据class查询多个节点
```getElementsByTagName();```根据标签名查询多个节点

> querySelector系列与getElement系列的区别在与querySelector系列没有动态性

#### DOM属性

* DOM种类
每一种HTML标签都有一种DOM类型对应
* DOM属性
	* DOM类别
	1. 元素节点 --> HTML中所有标签
	2. 文本节点 --> 如纯文本节点
	3. 特性节点 --> 标签属性

```javascript
let divDom = document.querySelecor('duv#test');
console.log(divDom.nodeType, divDom.nodeName, divDom.nodeValue);
//			节点类型			节点名称		节点值

let txtDom = divDom.firstChild; //返回的divDom的第一个子节点
console.log(txtDom.nodeType, txtDom.nodeName, txtDom.nodeValue);

let attDom = divDom.attributes.id; //获取divDom的id属性
console.log(attom.nodeType, attom.nodeName, attom.nodeValue);
```
> attributes可以获取元素节点的所有属性，得到的结果是一个字典，可以通过属性Key获取对应的特性系节点

* DOM内容
获取内容
```javascript
let divDom = document.querySelector('div#test');
console.log(div.outerHTML); // 输出divDom的整个HTML代码

console.log(div.innerHTML); // 输出divDom的内部HTML代码

console.log(div.innerText); // 输出DOM内部纯文本内容
```

* DOM亲属
```javascript
let divDom = document.querySelecor('div#text');
console.log(divDom.firstChild, divDom.lastChild); // 输出divDom节点的第一个和最后一个子节点

console.log(divDom.childNodes); // 输出一个子节点组成的nodeList

console.log(divDom.parentNodes); // 输出父节点包括本身
```

* DOM样式
```javascript
let h1Dom = document.querySelecor('h1');
console.log(h1Dom.classList); // 输出h1的class名称组成的数组

console.log(h1Dom.style); // 对象或者字典的方法储存CSSStyle

console.log(h1Dom.style.color); // 输出其中一个color属性的值
```
* DOM数据属性

利用```data-*```允许我们在标准内于HTML元素中存储额外的信息
```HTML
<article data-parts="3" data-words="1314" data-category="python"></article>
```

* js获取DOM属性
```javascript
const article = document.querySelector('article');
console.log(article.dataset);
//dataset是一个Map对象，他是data-*中*的Key-Value集合
```
#### DOM操作

* DOM样式修改
```javascript
// 保存当前是否选中的状态
let isSelected = false;

// 获取整个元素的节点
const box = document.querySelector('.box');

// 获取select框节点
const select = document.querySelector('.select');

// 给整个元素添加点击事件【大家可以先忽略这部分】
box.addEventListener('click', function () {
  // 点击以后触发这个函数

  // 修改当前选中状态，取反即可
  isSelected = !isSelected;

  // 如果当前是选中状态、则添加img到select中
  if (isSelected) {
    // 创建一个img标签节点
    const img = document.createElement('img');

    // 设置img的src属性和样式，让其撑满select框
    img.src = 'https://style.youkeda.com/img/sandwich/check.png';
    img.setAttribute('style', 'width: 100%; height: 100%;');

    // 将这个节点添加到select框中
    select.appendChild(img);
  } else {
    // 如果不是选择状态，则清空内部子元素
    select.innerHTML = '';
  }
});
```
* 添加新节点
```appendChild(newNode)```
此方法可以添加子节点
```inserBefore(newNode,referenceNode)```
此方法与appendChild相反，实在所有目标子节点之前添加节点
> newNode为新节点，referenceNode为目标节点
```javascript
function createDisease(txt) {
  const dom = document.createElement('li');
  const domTxt = document.createTextNode(txt);
  dom.appendChild(domTxt);
  return dom;
}

const root = document.querySelector('ul.root');
const sars = document.querySelector('li.sars');

// 创建 H1N1
const H1N1 = createDisease('H1N1');
root.appendChild(H1N1);

// 创建 新型冠状病毒
const nCoV = createDisease('新型冠状病毒');
root.insertBefore(nCoV, sars);
```
* 设置样式、属性
```img.setAttribute('style', 'width: 100%; height: 100%;');```
```dom.style.color = 'xxxx';```
两者均可
> 可用classList来操作节点class属性

* innerHTML
用```innerHTML = ' '```来清空节点内容