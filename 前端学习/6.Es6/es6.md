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
