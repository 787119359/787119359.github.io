---
layout: post
title: "JavaScript 继承的理解"
date: 2019-07-26
tag: 学习
---



js中的继承就是获取存在对象已有属性和方法的一种方式.



### 属性拷贝

> 就是将对象的成员复制一份给需要继承的对象

```
// 创建父对象
var superObj = {
  name: 'Li',
  age: 25,
  friends: ['小明', '小李', '小赵'],
  showName: function(){
    alert(this.name);
  }
}

// 创建需要继承的子对象
var subObj = {};

// 开始拷贝属性(使用for...in...循环)
for( var i in superObj ){
  subObj[i] = superObj[i];
}

console.log(subObj)
console.log(superObj)
```

**存在问题：**

> 如果继承过来的成员是引用类型的话,
> 那么这个引用类型的成员在父对象和子对象之间是共享的,
> 也就是说修改了之后, 父子对象都会受到影响.



### 原型式继承

> 原型式继承就是借用构造函数的原型对象实现继承. 即 子构造函数.prototype = 父构造函数.prototype

```
// 创建父构造函数
function SuperClass(name){
  this.name = name;
  this.showName = function(){
    alert(this.name);
  }
}

// 设置父构造器的原型对象
SuperClass.prototype.showAge = function(){
  console.log(this.age);
}

// 创建子构造函数
function SubClass(){

}

// 设置子构造函数的原型对象实现继承
SubClass.prototype = SuperClass.prototype;

var child = new SubClass()
```

**问题:**

> 1. 父构造函数的原型对象和子构造函数的原型对象上的成员有共享问题
> 2. 只能继承父构造函数的原型对象上的成员, 不能继承父构造函数的实例对象的成员



### 原型链继承

> 即 子构造函数.prototype = new 父构造函数()

```
// 创建父构造函数
function SuperClass(){
    this.name = 'liyajie';
    this.age = 25;
    this.showName = function(){
        console.log(this.name);
    }
}
// 设置父构造函数的原型
SuperClass.prototype.friends = ['小名', '小强'];
SuperClass.prototype.showAge = function(){
    console.log(this.age);
}
// 创建子构造函数
function SubClass(){

}
// 实现继承
SubClass.prototype = new SuperClass();
// 修改子构造函数的原型的构造器属性
SubClass.prototype.constructor = SubClass;

var child = new SubClass();
console.log(child.name); // liyajie
console.log(child.age);// 25
child.showName();// liyajie
child.showAge();// 25
console.log(child.friends); // ['小名','小强']

// 当我们改变friends的时候, 父构造函数的原型对象的也会变化
child.friends.push('小王八');
console.log(child.friends);["小名", "小强", "小王八"]
var father = new SuperClass();
console.log(father.friends);["小名", "小强", "小王八"]
```

**问题:**

> 不能给父构造函数传递参数，父子构造函数的原型对象之间有共享问题



### 借用构造函数

> 使用`call`和`apply`借用其他构造函数的成员, 可以解决给父构造函数传递参数的问题, 但是获取不到父构造函数原型上的成员.也不存在共享问题

```
// 创建父构造函数
function Person(name){
  this.name = name;
  this.freinds = ['小王', '小强'];
  this.showName = function(){
     console.log(this.name);
  }
}

// 创建子构造函数
 function Student(name){
  // 使用call借用Person的构造函数
  Person.call(this, name);
 }

 // 测试是否有了 Person 的成员
 var stu = new Student('Li');
 stu.showName(); // Li
 console.log(stu.friends); // ['小王','小强']
```



### 组合继承

>  借用构造函数 + 原型式继承

```
// 创建父构造函数
function Person(name,age){
    this.name = name;
    this.age = age;
    this.showName = function(){
        console.log(this.name);
    }
}
// 设置父构造函数的原型对象
Person.prototype.showAge = function(){
    console.log(this.age);
}
// 创建子构造函数
function Student(name){
    Person.call(this,name);
}
// 设置继承
Student.prototype = Person.prototype;
Student.prototype.constructor = Student;
```

> 解决了 父构造函数的属性继承到了子构造函数的实例对象上了,
> 并且继承了父构造函数原型对象上的成员
> 解决了给父构造函数传递参数问题

**问题:**

> 共享的问题



### 借用构造函数 + 深拷贝

```
function Person(name,age){
    this.name = name;
    this.age = age;
    this.showName = function(){
        console.log(this.name);
    }
}
Person.prototype.friends = ['小王','小强','小王八'];

function Student(name,25){
    // 借用构造函数(Person)
    Person.call(this,name,25);
}
// 使用深拷贝实现继承
deepCopy(Student.prototype,Person.prototype);
Student.prototype.constructor = Student;
```

> 这样就将Person的原型对象上的成员拷贝到了Student的原型上了, 这种方式没有属性共享的问题.



**原文**：https://www.jianshu.com/p/1016160e91fe

