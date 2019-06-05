
### javascript的实现
主要由 ECMAScript DOM BOM 组成  
其中  
ECMAScript规定了核心的语言功能
- 语法
- 类型
- 语句
- 关键字
- 保留字
- 操作符
- 对象

DOM 提供了访问和操作网页内容的方法和接口

BOM 提供了与浏览器交互的方法和接口

### 在html中使用js
- 内嵌
```
<script type="text/javascript">
  alert('hello');
</script>
```
- 外部文件
```
<script type="text/javascript">
```

标签属性
- src   外包js文件地址  
- defer 脚本在文档加载完成之后再执行  
- async 脚本不阻塞文档呈现  

文档类型
- 混杂模式
- 标准模式

### 基本概念
区分大小写（包括变量、函数、操作符）  
严格模式 （use strict）  

#### 数据类型  
- 值类型(基本类型)：
  - 字符串（String）
  - 数字(Number)
  - 布尔(Boolean)
  - 对空（Null，通常用来声明一个空对象）
  - 未定义（Undefined，声明了但未赋值）
  - Symbol

- 引用数据类型：
  - 对象(Object)
  - 数组(Array)
  - 函数(Function)

typeof 可以用来返回数据类型  
Infinity无穷可以用isFinite()判断    
NaN非数值  
数值转化
- Number()
- parseInt()
- parseFloat()

转为字符串  
- toString 方法
数值、布尔值、对象和字符串值都有 toString()方法。但 null 和 undefined 值没有这个方法。
- string 函数
如果值有 toString()方法，则调用该方法(没有参数)并返回相应的结果
如果值是 null，则返回"null"，如果值是 undefined，则返回"undefined"。

Object对象的属性和方法
- constructor:保存着用于创建当前对象的函数。对于前面的例子而言，构造函数(constructor)就是 Object()。
- hasOwnProperty(propertyName):用于检查给定的属性在当前对象实例中(而不是在实例 的原型中)是否存在。其中，作为参数的属性名(propertyName)必须以字符串形式指定(例 如:o.hasOwnProperty("name"))。
- isPrototypeOf(object):用于检查传入的对象是否是传入对象的原型(第 5 章将讨论原 型)。
- propertyIsEnumerable(propertyName):用于检查给定的属性是否能够使用 for-in 语句 (本章后面将会讨论)来枚举。与 hasOwnProperty()方法一样，作为参数的属性名必须以字符串形式指定。
- toLocaleString():返回对象的字符串表示，该字符串与执行环境的地区对应。
- toString():返回对象的字符串表示。
- valueOf():返回对象的字符串、数值或布尔值表示。通常与 toString()方法的返回值
相同。

### 操作符
#### 一元操作符
 - ++
 - \--
 - +
 - -

#### 位操作符
- ~
- &
- |
- <<
- \>>
- <<<
- \>>>

#### 布尔操作
- &&
- ||
- !

#### 相等操作符
- ==
- !=
- ===
- !==

### 控制语句
- if
- do-while
- while
- for
- for-in
- label   
  示例：
  ```
  start: for (var i=0; i < count; i++) {
        alert(i);
  }
  ```
  start 标签可以在将来由 break 或 continue 语句引用
- break
- continue
- with  
  示例：
  ```
  var qs = location.search.substring(1);
  var hostName = location.hostname;
  var url = location.href;

  上面几行代码都包含 location 对象,使用 with 语句

  with(location){
   var qs = search.substring(1);
    var hostName = hostname;
    var url = href;
  }
  ```
- switch

### 函数
参数数组   
arguments


## 变量、作用域和内存问题
基本类型
- 字符串
- 数值
- 布尔
- undefined
- null
- symbol
引用类型
- 数值
- 对象
- 函数

instanceof  

执行上下文
只有函数才能创建出作用域
