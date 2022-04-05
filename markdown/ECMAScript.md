# ECMAScript笔记

ECMAScript规定了js基础语法核心知识

[TOC]

---

## 输入输出语法

弹出输入框
`prompt('请输入内容：')`

弹出警示框
`alert('这是一个警示框')`

弹出确认框
`confirm("这是一个确认框")`

页面输出
`document.write("Hello World!")`

控制台console输出
`console.log()`

---

## 变量

### 声明变量

```js
let num = 1
let arr = [1, 2, 3]
```

**let** 和 **var** 的区别

> ES6 新增了let命令，用来声明变量。它的用法类似于var，但是所声明的变量，只在let命令所在的代码块内有效。
>
> ```js
> {
>   let a = 10;
>   var b = 1;
> }
> 
> a // ReferenceError: a is not defined.
> b // 1
> ```
>
> 上面代码在代码块之中，分别用let和var声明了两个变量。
> 然后在代码块之外调用这两个变量，结果let声明的变量报错，var声明的变量返回了正确的值。
> 这表明，let声明的变量只在它所在的代码块有效。

### 使用变量

`document.write("这个数是${num}。")`

### 数据类型

> JS 是==弱数据类型==，变量到底属于哪种类型，只有赋值之后才能确认

#### 基本数据类型

- **number** 数字型
- **string** 字符串型
- **boolean** 布尔型
- **undefined** 未定义型
- **null** 空类型

> - null 和 undefined 区别：
>   1. **undefined** 表示没有赋值
>   2. **null** 表示赋值了，但是内容为空 (把 null 作为尚未创建的对象)

#### 引用数据类型

- **object** 对象
- **function** 函数
- **array** 数组

### 类型转换

#### 隐式转换

- +号两边只要有一个是字符串，都会把另外一个转成字符串
- 除了+以外的算术运算符，比如 - * / 等都会把数据转成数字类型

```js
console.log('pink' + 18) // pink18
console.log(10 + '10') // 1010

console.log(10 - '10') // 0

// 小技巧
let num = '10'
console.log(+num)
console.log(10 + +'10') // 20
```

#### 显式转换

##### 转换为数字

`Number(数据)`

- 如果字符串内容里有非数字，转换失败时结果为 **NaN**（Not a Number）即不是一个数字
- NaN也是number类型的数据，代表非数字

只保留整数： `parseInt(数据)`

可以保留小数： `parseFloat(数据)`

##### 转换为字符型

```js
String(数据)
变量.toString(进制)
```

> .toString()可以将所有的的数据都转换为字符串，但是要排除 null 和 undefined
> String()可以将 null 和 undefined 转换为字符串，但是没法转进制字符串

---

## 数组

### 添加元素

数组.push() 方法将一个或多个元素添加到数组的==末尾==，并返回该数组的新长度
`arr.push(元素1, 元素2, ...)`

数组.unshift() 方法将一个或多个元素添加到数组的==开头==，并返回该数组的新长度
`arr.unshift(元素1, 元素2, ...)`

### 删除元素

数组.pop() 方法从数组中删除==最后一个==元素，并返回该元素的值
`arr.pop()`

数组.shift() 方法从数组中删除==第一个==元素，并返回该元素的值
`arr.shift()`

数组.splice() 方法 删除指定元素
`arr.splice(start, deleteCount)`

- start ：指定修改的开始位置（从0计数）
- deleteCount ：表示要移除的数组元素的个数（可选，默认删除到最后）

---

## 函数

```js
function sayHello() {
    document.write("Hello")
}
```

- 形参如果不被赋值，就是 undefined
- 函数可以没有 return ，这种情况函数默认返回值为 undefined

> 如果函数内部或者块级作用域内部，变量没有声明就直接赋值，会当成全局变量看

### 匿名函数

将匿名函数赋值给一个变量，并且通过变量名称进行调用，称为函数表达式

```js
let fun = function () {
    //function body
}
fun()
```

#### 立即执行函数

声明一个函数，并马上调用这个匿名函数

```js
//第一种：用括号把整个函数定义和调用包裹起来
( function () {
    //function body
} () )

//第二种：用括号把函数定义包裹起来，后面再加括号
( function () {
    //function body
} ) ()
```

- 作用：不必为函数命名，**避免污染全局变量**
- 注意：多个立即执行函数要用 **;** 隔开

---

## 对象

声明对象：

```js
let person = {
    name: "jack",
    age: 18,

    sayHi: function () {
        document.write("hi")
    }
}
```

属性访问：获得对象里面的属性值

```js
console.log(person.name)
console.log(person['name'])
person.sayHi()
```

### 操作对象

#### 增加属性和方法

```js
person.gender = '男'
person['hobby'] = '篮球'

person.move = function() {
    //function body
}
```

- 无论是属性或是方法，同一个对象中出现名称一样的，后面的会覆盖前面的（改）

#### 删除属性

`delete person.age`

### 遍历对象

```js
for (let k in person) {
    document.write(k) // 打印属性名
    document.write(person[k]) // 打印属性值
}
```

- k 是获得对象的属性名， 对象名[k] 是获得该属性的属性值

### 内置对象Math

方法：

- random：生成0-1之间的随机数（包含0不包括1）
  - 生成0-10的随机数： `Math.floor(Math.random() * (10 + 1))`
  - ==生成N-M之间的随机数：== `Math.floor(Math.random() * (M - N + 1)) + N`
- ceil：向上取整
- floor：向下取整
- max：找最大数
- min：找最小数
- pow：幂运算
- abs：绝对值

---

## 注意

### 比较运算符

- ===： 左右两边是否类型和值都相等
- !\==： 左右两边是否不全等

细节：

- NaN不等于任何值，包括它本身
- 尽量不要比较小数，因为小数有精度问题
