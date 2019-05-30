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
