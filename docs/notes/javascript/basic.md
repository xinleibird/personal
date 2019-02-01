# 1. 基础内容

## 1.1 JavaScript 组成

* ECMAScript(ES)
* DOM
* BOM

---

## 1.2 全局对象和全局的对象

1. 全局对象 global object
   > window
2. 全局的对象（标准内置对象） global objects
   > String, Array, Function ...

---

## 1.3 创建变量

1. var
2. function
3. let
4. const
5. import
6. class

---

## 1.4 数据类型分类

### 基本数据类型

1. number
2. string
3. boolean
4. null
5. undefined

### 引用数据类型

1. object
   1. 普通对象
   2. 数组对象
   3. 正则对象
   4. 日期对象
   5. ...
2. function
3. Symbol 创建一个唯一的值

---

## 1.5 数据类型剖析

### number

- NaN typeof
  - NaN !== NaN
- isNaN() 和 Number.isNaN()
  - isNaN() 全局对象，强制类型转换
  - Number.isNaN() 加强版，不进行类型转换
- parseInt()
- parseFloat()

### boolean

- !
- !! 只有这些情况为假
  - !!0
  - !!false
  - !!''
  - !!null
  - !!NaN
  - !!undefined

### null && undefined

### object

---

## 数据类型检测

1. typeof
2. instanceof
3. constructor()
4. Object.prototype.toString.call()

---

## 操作语句

1. 判断

- if / else
- switch / case
- 三元运算符

2. 循环

- for
- for in
- while

---

# 2. 基础进阶

## JavaScript 中的数据类型转换

### 把非 number 类型转换为 number 类型

1. 发生转换的情况

- Number 强制转换
- isNaN 转换的时候
- 基于 parseInt 或者 parseFloat 去手动转换
- 数学运算 + - \* / % （需要注意 + 也是字符串拼接运算）

2. 转换规律

- 把字符串转换为数字，只要遇到一个非有效数字，结果即为 NaN
- 把布尔转换为数字，true 1， false 0
- 把空转换为数字，null 0， undefined NaN, NaN NaN
- 把引用类型转换为数字，先 toString，再参考条目 1

### 把非字符串类型转换为字符串

1. 发生转换的情况

- 基于 alert，confirm，prompt，和 document.write
- 基于 + 进行字符串拼接时
- 给对象设置属性名时（对象的属性名只能是数字或者字符串）
- 手动调用 toString，toFixed，join 时
  ...

2. 转换规律

- 基本上都是调用 toString
- 除了对象，都是直觉式的结果

```
1 -> '1'
NaN -> 'NaN'
null -> 'null'
undefined -> 'undefined'
[] -> ''
[12] -> '12'
[12, 23] -> '12, 23'
{} -> '[object Object]'
```

3. 特殊情况

- 数学运算 +
  `1 + true -> 2`
- 字符串拼接
  `'1' + true -> '1true'`
- 对于引用类型，先将引用类型转换为字符串，再进行字符串拼接
  `[12] + 34 -> '1234'`
- **特别需注意**
  `{} + 10 -> 10` 其中花括号不被认为是对象，而被看做代码块
  `({}) + 10 -> [object Object]10` 加括号才被看做对象
  == 比较运算，先转换为相同的类型，再进行比较

### 比较运算中的类型转换

---

## 数组及常用方法

数组是对象类型，也是由键值对组成的

### 特征

1. 索引递增，任意类型
2. length 属性

### 常用方法

#### 改变原数组

1. push

- 作用：数组末尾追加
- 参数：追加的内容（一个或多个）
- 返回：追加后数组的 length
- 改变：改变原数组

2. pop

- 作用：删除末尾项
- 参数：无
- 返回：被删除项
- 改变：改变原数组

3. shift

- 作用：删除首项
- 参数：无
- 返回：被删除项
- 改变：改变原数组

4. unshift

- 作用：增加首项
- 参数：追加的内容（一个或多个）
- 返回：追加后数组的 length
- 改变：改变原数组

5. splice（英文组接）

- 作用：分割数组
  - ary.splice(n, m) 从索引 n 开始 删除 m 项内容
  - 作用：删除部分数组
  - 参数： 起始索引 n， 删除长度 m
  - 返回：数组  形式的被删除项
  - 改变：改变原数组
- 作用：新增项目
  - ary.splice(n, 0, x, ...)
  -  作用：在索引 n 之前，插入 x ...
  - 返回：空数组
  - 改变：改变原数组
- 作用：修改数组
  - ary.splice(n, m, x, ...)
  -  作用：在索引 n 之后删除 m 项，并在 n 之前，插入 x ...
  - 返回：数组形式的被删除项
  - 改变：改变原数组

6. sort

- 作用：无参数时按照 unicode 码顺序进行排序，可接受一个回调函数作为排序函数
- 返回：排序后的数组
- 改变：改变原数组

7. reverse

- 作用：颠倒数组顺序
- 参数：无
- 返回：颠倒后端数组
- 改变：改变原数组

8. ary.length-- 可删除数组末尾项

9. 关于 delete 操作符

- 对象属性

- 数组项
  可参考 [MDN: delete 操作符](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/delete)

#### 不改变原数组

1. slice（英文切片）

- 作用：查找指定索引到末尾的内容
  - ary.slice(n) 查找从索引 n 到数组末尾的内容
  - 作用：查找数组内容
  - 参数： 起始索引 n
  - 返回：数组  形式的被查找项
  - 改变：不改变原数组
- 作用：查找指定索引与长度的内容
  - ary.slice(n, m) 查找从索引 n 开始 到索引 m 处内容 **半开半闭区间**
  - 作用：查找数组内容
  - 参数： 起始索引 n，查找长度 m
  - 返回：数组  形式的被查找项
  - 改变：不改变原数组
- 作用： 数组克隆
  - ary.slice(0 或不填)
  - 作用：克隆数组
  - 参数：0 或不填
  - 返回：数组  形式的克隆
  - 改变：不改变原数组
- 关于负数索引
   假如有数组 ary = [1, 2, 3, 4, 5] - ary.slice(-2, -1) 从倒数第二项开始，倒数第一元素不被包含（第二项为负数固定如此），因此只有倒数第二个元素 - ary.slice(-3, -1) -> [3, 4] - ary.slice(-3, -2) -> [3]

2. concat

- 作用：数组拼接
- 参数：拼接的内容(可以是数组）
- 返回：拼接后端数组
- 改变：不  改变原数组

3. toString

- 作用：转换为字符串
- 参数：无
- 返回：转换后的字符串
- 改变：不改变原数组

4. join

- 作用：和 toString 类似，但是分隔符可选
- 参数：分隔符
- 返回：转换后的字符串
- 改变：不改变原数组

5. indexOf

- 作用：查找存在某项的索引
- 参数：要查找的  项
- 返回：找到该项的索引，未找到则返回 -1
- 改变：不改变原数组

6. lastIndexOf

- 作用：查找存在某项的索引
- 参数：要查找的  项
- 返回：找到该项的索引，未找到则返回 -1
- 改变：不改变原数组

---

## 字符串及常用方法

length 属性

字符串是基本数据类型，其操作为值类型操作， 而非引用类型操作，也就不存在是否改变原字符串的问题。所有字符串操作函数均不改变原字符串。

### 常用方法

1. charAt

- 作用：根据索引，获取指定位置的字符
- 参数：索引位置
- 返回：索引位置的字符

2. charCodeAt

- 作用：根据索引，获取指定位置的 Unicode 编号（对于汉字，可识别双字节汉字）
- 参数：索引位置
- 返回：索引位置字符的 Unicode  编号
  _相对的 `String.fromCharCode`_

3. indexOf

4. lastIndexOf

5. slice

- 作用：ary.slice(n, m) 查找从索引 n 处到索引 m 处到字符串 **半开半闭区间**
- 参数：开始索引，结束索引
- 返回：切片的字符串

6. substring

- 作用：ary.substring(n, m) 查找从索引 n 处到索引 m 处到字符串 **半开半闭区间**
- 参数：开始索引，结束索引
- 返回：切片的字符串

7. substr

- 作用：ary.substr(n, m) 查找从索引 n 处长度为 m 的字符串
- 参数：开始索引，子串长度（可选）
- 返回：切片的字符串

8. toUpperCase

- 作用：小写转大写

9. toLowerCase

- 作用：大写转小写

10. split

- 作用：与数组 join 逆运算，把字符串转换为数组

11. replace

- 作用：替换字符串中的原有字符
- 参数：ary.replace(n, m)，n 原字符，m 需特换的字符
- 返回：替换后的字符串

---

## 数学运算及常用方法

### Math 的静态方法

- Math.abs 绝对值
- Math.ceil 向上取整
- Math.floor 向下取整
- Math.round 四舍五入取整
- Math.sqrt 开平方
- Math.pow 指数运算 Math.pow(2, 10) -> 2 的 10 次幂
- Math.min 取多个参数中的最小值
- Math.max 取多个参数中的最大值
- Math.random 取 [0, 1) 中的随机数

### Math 的静态属性

- Math.PI

---

## DOM 及常用方法

### DOM 树

1. 获取 DOM 元素的方法

- getElementById 上下文只能是 document
- getElementsByTagName
- getElementsByClassName
- getElementsByName 上下文只能是 document
- querySelector 类似于 CSS 中的选择器，只选择一个
- querySelectorAll 选择全部 (注意：获取到的是非映射的静态集合)
- document.head
- document.body
- document.documentElement
  - document.documentElement.clientWidth
  - document.body.clientWidth
  - document.documentElement.clientHeight
  - document.body.clientHeight

2. DOM 中的节点

- 元素节点（HTML 标签）
- 文本节点（文字内容）
- 注释节点（注释内容）
- 文档节点（document）
- ...

### 节点自身属性

nodeType - nodeName - nodeValue

1. 元素节点

- nodeType 1
- nodeName 大写标签名
- nodeValue null

2. 文本节点

- nodeType 3
- nodeName '#text'
- nodeValue 文本内容

3. 注释节点

- nodeType 8
- nodeName '#common'
- nodeValue 注释内容

4. 文档节点

- nodeType 9
- nodeName '#document'
- nodeValue null

5. 描述节点之间关系的属性

- parentNode 获取唯一的父节点
- childNodes 获取所有的子节点
- children 获取所有的**元素**子节点
- previousSibling 获取上一个兄弟节点
- previousElementSibling 获取上一个**元素**兄弟节点
- nextSibling 获取下一个兄弟节点
- nextElementSibling 获取下一个**元素**兄弟节点
- firstChild 获取第一个子节点
- firstElementChild 获取第一个**元素**子节点
- lastChild 获取最后一个子节点
- lastElementChild 获取最后一个**元素**子节点

7. DOM 中的增删改

- createElement 创建一个元素节点
- appendChild 在此元素容器末尾增加一个元素子节点
- insertBefore 在此元素节点之前增加一个元素节点
- cloneNode 克隆节点（接受一个布尔参数，为真则为深克隆，包括子元素）
- removeChild 删除子元素
- set/get/removeAttribute 修改节点的属性（直接更改页面呈现，普通对象增加属性的方式则不会修改页面呈现）

# 3. 语言细节

## JavaScript 是 Object Based

一切皆克隆, 所有对象都是基于原型的克隆, 这种特性与 Object Oriented 截然不同. 原型链与原型链的理解是理解 JavaScript 的钥匙.

> 多说一句, 所谓栈内存时不可能存在于动态语言中的。所谓原生数据类型的存在，仅仅在于原生数据类型的字面量或者赋值前阶段，一旦压栈成功，立刻变成引用类型，具体值存入堆内存。

1. 所有函数类型都自带一个 prototype 属性，指向原型对象
2. 此 prototype 属性包含一个 constructor 属性，该属性指向自身
3. 所有实例对象都包含一个 \***\*proto\*\*** 属性，该属性指向当前实例所属原型对象的 prototype 属性
   this 只在函数体内部有意义
   箭头函数无 this

条件区域内的 var 赋值，不管条件是否成立，都会进行变量提升。

1. 作为实例对象的方法调用时，指向该实例对象
2. 作为普通函数调用时，指向 window
3. 作为构造方法中的 this，指向构造出的实例对象
4. 匿名函数式的 IIFE，因为是自执行，实际上执行环境就是全局作用域，this 始终是 window
5. 箭头函数的不持有 this，按照词法作用域向上查找最近的非箭头函数的作用域，如果无则是 window
6. call，apply

> 值得注意的是，关键是何时调用，也就是何时执行，()

形参赋值
变量提升
变量赋值开辟空间
顺序运行
运行结束销毁内存

函数的 constructor 属性实际上只是历史遗留物，不会影响实际对象的构造，不会影响原型链的继承，仅仅作为一种提示存在。切记。

`fn.call(obj);`

1. 找到原型链上的 Function.call 方法并执行
2. 在执行时内部处理了一些事情

- 首先把要操作的 fn 函数中的要指定的 this 值作为第一个实参传递给 call 函数
- 然后把余下的参数作为实参传递给 fn 执行

`fun.call(thisArg, arg1, arg2, ...)`

call 与 apply 的区别，call 接受多个参数，apply 接受参数数组

## 集中映射

1. 在全局作用域下提升的变量，相当于给 window 对象添加属性，并且此属性存在映射。
2. 在非严格模式下，function 的形参变量与 arguments 中的元素一一对应，并且存在映射
3. DOM 映射：浏览器中的 HTML 元素和通过 JavaScript 方法获取到的元素对象或者集合存在映射机制

## Data

数据绑定

1. 字符串拼接

- 普通字符串拼接
- ES6 模板字符串
- 模板引擎

2. DOM 操作

- 动态创建 DOM 的方式 (外层容器基于 createElement 完成, 内层容器通过外层容器的 .innerHTML 属性添加完成, 最后 appendChild 外层容器)

> innerHTML 在处理添加大量节点的操作上是要比 DOM 操作要更块, 性能更好.
> 对于简单的文本操作, 还是用 DOM 操作来完成也确实没错.

# 4. 浏览器的重排和重绘 (Reflow and Repaint)

## 1. 浏览器渲染的一般步骤

1. 浏览器使用流式布局模型 (Flow Based Layout)
2. 浏览器把 HTML 解析成 DOM, 把 CSS 解析成 CSSOM
3. DOM 和 CSSOM 合并生成渲染树 (Render Tree)
4. 浏览器基于 GPU 开始按照 Render Tree 渲染页面

> 由于浏览器使用流式布局, 对 Render Tree 的计算通常只需要遍历一次就可以完成, 但 table 及其内部元素除外, 他们可能需要多次计算, 通常要花 3 倍于同等元素的时间, 这也是为什么要避免使用 table 布局的原因之一.

## 2. 重排 Reflow

当 Render Tree 中的一部分或全部元素因为元素的规模尺寸, 布局, 隐藏等改变而需要重新构建的过程称之为重排 (Reflow); 每个页面生存周期中至少发生一次重排, 即页面第一次加载时. 在重排过程中, 浏览器会使渲染树中收到改变影响到部分失效, 并重新构造这一部分渲染树. 完成回流后, 任务交由下一步重绘进行.

### 下列情况会发生重排

1. 页面初始化
2. 调整窗口大小, 浏览器尺寸改变
3. 增加或者移出样式表
4. 元素位置改变, 元素尺寸改变 (width / height / margin / padding / border)
5. 内容改变, 例如文本改变或者图片大小改变引起的宽度高度计算值的改变.
6. 改变字体
7. 激活 CSS 伪类
8. 操作 class 属性
9. 外部脚本操作 DOM, 增删改可见的 DOM 元素
10. 计算 offsetWidth 和 offsetHeight 属性
11. 设置 style 属性的值

### 分类助记

1. JavaScript 修改以下 Style 信息时, 会触发重排
   - clientWidth / clientHeight / clientTop / clientLeft
   - offsetWidth / offsetHeight / offsetTop / offsetLeft
   - scrollWidth / scrollHeight / scrollTop / scrollLeft
   - width / height
   - getComputedSytle()
   - getBoundingClientRect()
2. CSS 中修改如下属性, 会触发重排
   - width / height / margin / border / padding
   - font / line-height / font-weithg
   - position / display / float / clear

## 3. 重绘 Repaint

由重排教由的命令或者当页面中的外观, 风格等等不影响布局的部分发生改变时, 会触发页面的重绘 (Repaint). 例如 background-color 的改变.

### 何时触发重绘

outline, visibility, background, color

## 4. 优化方式

### CSS

- 避免 table 布局,  另外一个实体如果不是语义明确的表格, 就不要用表格.
- 尽可能在 DOM Tree 的最末端改变 class
-  避免设置多层  行内样式 (inline style), 或者说压根就不应该设置行内样式
- 将动画效果应用到 position 属性为 absolute 或者 fixed 的元素上
- 避免使用 CSS 表达式 ( 例如: calc())

### JavaScript

- 避免频繁操作样式, 最好一次性重写 style 属性, 或者将样式表定义为 class 并一次性更改
- 避免频繁的 DOM 操作, 有可能的话, 创建一个 documentFragment, 在它上面  应用所有的 DOM 操作, 最后把它添加到文档中
- 也可以先为元素设置 display: none, 操作结束后把它显示出来. display: none 的元素上进行 DOM 操作不会引发重排和重绘.
- 避免频繁读取会引发重排重绘的属性, 如果确实需要多次使用, 就用个变量存起来
- 对具有复杂动画的元素使用绝对定位, 使它脱离文档流, 否则会引起子元素乃至父元素的频繁重绘. 基本原则  是, 把  动画元素用 position: absolute 踢出标准流, 这样重排重绘就限制在 absolute 元素及其子节点.

# 5. 正则

元字符
修饰符

中括号中出现的元字符一般是代表本身含义

分组的作用

- 改变默认的优先级
- 分组捕获 ()
- 分组引用 (?:)

RegExp.exec() 返回一个数组 (未匹配到则返回 null)
RegExp.test() 返回 true 或 false。

String.match() 返回一个数组或者在未匹配到时返回 null
String.search() 返回匹配到的位置索引, 或者在失败时返回-1
Stirng.replace() 使用替换字符串替换掉匹配到的子字符串
String.split() 分隔一个字符串, 并将分隔后的子字符串存储到数组中

定时器

setTimeout(), setInterval, clearTimeout(timer number), clearInterval(timer number)

设置定时器时会返回一个值, 即是 timer number
`const timer = setTimeout(....);`

1. 所有的事件绑定都是异步
2. 所有的定时器都是异步
3. ajax 一般都使用异步
4. 回调函数也算是异步
