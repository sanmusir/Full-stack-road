### var let const

var a = 10;  
var 可以重复定义赋值 作用域：函数  
let 不可以重复定义，可赋值 作用域：块级  
const 不可以重复定义和赋值 作用域：块级  
const person = {name:'jj',age:20}  
person.age = 18  //可以执行
若要对象属性也不能改变的话可以这样操作  
const Ljj = object.freeze(person)  

立即执行函数  
作用：创建一个独立的作用域，避免全局变量污染  
(function(){})()  

可使用let来限定作用域

```
for(let i = 0;i < 10;i++){
  console.log(i);
  setTimeout(function(){
    console.log(i);
    },1000)
}

```
变量提升

```
console.log(name); //undefined
var name = 'sanmu';

console.log(name); //RefrenceError
let|const name = 'sanmu';

```

### 箭头函数

去掉function 加箭头
单个参数可去括号，多个参数逗号隔开
=>
```
 const numbers = [1,2,3,4];
 const double = numbers.map((num) =>{
      return num * 2;
   });
 console.log(double);

 const who = (name) => {console.log(name);}
 who('xiaom');
```

隐式返回

```
  const numbers = [1,2,3,4];
  const double2 = numbers.map((num) => num * 2);
  console.log(double2);
```
this
一个函数独立运行的时候，this指向window、global、undefined
```
const sanmu = {
  name: 'sanmu',
  like: ['banana','orange','apple'],
  printLike: function(){
    this.like.map(function(body){
      console.log(`${this.name} like ${body}`);
      })
  }
}
sanmu.printLike()
```
箭头函数的this 继承于父作用域
```
const sanmu = {
  name: 'sanmu',
  like: ['banana','orange','apple'],
  printLike: function(){
    this.like.map( body =>{
      console.log(`${this.name} like ${body}`);
      })
  }
}
sanmu.printLike()
```
不适用场景
- 作为构造函数 箭头函数不会绑定this
- 一个对象的方法
- 箭头函数没有arguments


### 模板字符串

`${变量} 字符串`

### 标签模板字符串

标签`${变量} 字符串`
```
const name = 'sanmu';
const topic = 'learn to use markdown'
const sentence = highlight`${name} has publish ${topic}`
function highlight(strings, ...values){
  const highlighted = values.map(value => `<span class='highlight'>${value}</span>`);
  let str = '';
  strings.forEach((string,i)=> str += `${string}${highlighted[i] || ''}`);
  return str;
}
```
### 新增的字符串函数

string.startsWith('要匹配字符串','起始位置')
string.endsWith('要匹配字符串','结束位置')
string.includes('要查询的字符串','起始位置')
string.repeat(10) 重复10次

### 对象解构

```
const sanmu = {
  name: 'sanmu',
  age: 18
}
const {name:newname, age, sex = 'man'} = sanmu;
```
### 数组解构

```
const numbers = [1,2,3,4];
const [one,,two] = numbers;
const [one, ...others] = numbers;

let a = 1;
let b = 2;
[a,b] = [b,a];
```

### for of

通常循环数组的做法：
- for循环
- 数组自带函数forEach  不支持 终止或跳过循环
- for in 循环   会便利数组上的非数字属性

for of （不支持对象）
```
const fruits = ['a','b','c'];
for(let fruit of fruits){
  console.log(fruit)
}
for(let[index,value] of fruits.entries()){
    console.log(index);
    console.log(value);
}
```

### 数组新方法

Array.from(目标数组,要执行的方法) 将类数组转化为数组，调用方法执行  
Array.of(1) 创建数组[1],而不是长度为1的数组  
.find(回调函数) 回调函数返回true 就停止查询 返回查询到的值
.findIndex(回调函数) 回调函数返回true 就停止查询 返回查询到的index
.some(回调函数) 只需要一个满足即可返回true
.every(回调函数) 全部满足才反馈true

### 剩余参数

...args

### 扩展运算符

...  把一个可遍历对象每个元素扩展到数组或函数中
let a = [1,2,3];
let b = [5,6];
let c = [...a,4,...b];
console.log(c);

### 对象字面量

```
const name = 'sanmu';
const age = 2;
const sanmu = {
  name: name,  
  age         //属性和值一样可以省略掉
  getAge: function(){
    console.log(this.age)
  },
  getName(){
      console.log(this.age)  //省略掉function
  }
}
```
计算属性

```
const keys = ['sanmu','zm'];
const values = [18,10];
const age = {
  [keys.shift()]:values.shift(),
  [keys.shift()]:values.shift()
}
```

### promise

Ajax 返回的顺序不确定

```
<head>
	<title>Promise Intro</title>
<script src="https://cdnjs.cloudflare.com/ajax/libs/jquery/3.3.1/jquery.min.js"></script>
</head>
<body>
	<script type="text/javascript">
		let user;

		$.get('https://api.github.com/users',data=>{
			console.log('fetched all users');
			user = data[0].login;
		});

		$.get(`https://api.github.com/users/${user}/repos`,data => {
			console.log('fetched user repos');
			console.log(data);
		})
	</script>
</body>
```
嵌套写法，写在第一个请求的回调函数里，嵌套越多越混乱，会坠入回调地狱。
```
<script type="text/javascript">
		let user;

		$.get('https://api.github.com/users',data=>{
			console.log('fetched all users');
			user = data[0].login;

			$.get(`https://api.github.com/users/${user}/repos`,data => {
			console.log('fetched user repos');
			console.log(data);
		})
		});

	</script>
```

为解决回调不确定性和回调地狱，ES6提供了Promise承诺，
用axios包来做下
.then()//事件监听成功之后执行 .catch()//返回错误信息
```
<head>
	<title>Promise Intro</title>
<script src="https://cdnjs.cloudflare.com/ajax/libs/axios/0.17.1/axios.min.js"></script>
</head>
<body>
	<script type="text/javascript">
		const usersPromise = axios.get('https://api.github.com/user');

		//$('p').on('click',function(){})  用.then()方法
		usersPromise
		.then(reponse =>{
			username =reponse.data[0].login;
			return axios.get(`https://api.github.com/users/${username}/repos`);
		})
		.then(reponse =>{
			console.log(reponse.data);
		})
		.catch(err =>{
			console.log(err);
		})
	</script>
</body>
```

### symbol

生成唯一标识符

const sanmu = Symbol();
const zm = Symbol();
sanmu == zm //false

Object.getOwnPropertySymbols(对象) 可以遍历出symbol 属性

### esLint
代码监测工具

### 模块
export import

config.js

```
export const appKey = 'abc123'  //命名导出，可以多个导出
export default appKey; //默认导出 只能一个导出

```

app.js

```
import app_key from './config'  //默认导出名字可以替换掉
import { appKey as app_key }from './config'  //命名导出名称可以通过as更改

console.log(appKey);

```

### babel
将es6的语法转换为es5

### class

类的声明
类的表达式

```
class User {
  constructor(name, email){
    this.name = name;
    this.email = email;
  }

  name(){
    console.log(this.name);
  }

  static des(){
    console.log(‘静态方法’);
  }

  set age(value) {
    this.age = value;
  }
«»
  get age() {
    return this.age
  }

}

```
