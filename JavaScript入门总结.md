
[TOC]

## JavaScript入门总结

### 1. 变量
JavaScript变量是存储数据的容器，JavaScript是弱类型编程语言，使用var定义变量，不需要指定具体的类型，会根据值推断出变量类型，变量可以随时赋值为其他类型。

```
var y; //A variable declared without a value will have the value undefined.
y = 3; 

var x = 5; // x is a number
x = 'JavaScript'; // x is a string
x = true; // x is a boolean
x = new Date(); // x is a date object

var name = 'JS', price = 20, age = 30; //一行定义多个变量

var carName = "GM";
var carName; //重复定义一个变量，这时carName的值仍然是GM
```
    
JavaScript的变量必须标识为唯一的名字，而这些唯一的名字称之为**标识符**。
**标识符的规则：**
- 可以包含字母、数字、下划线和美元符号
- 必须由字母、下划线或美元符号开头
- 大小写敏感
- 保留关键字不能作为标识符

**示例**

```
var name  = 'Jack'; //正确
var $name = 'Jack'; //正确，但不推荐
var _name = 'Jack'; //正确，但不推荐
var 8name = 'Jack'; //错误，Invalid or unexpected token
var #name = 'Jack'; //错误，Invalid or unexpected token
var while = 'Jack'; //错误，保留关键字不能作为变量标识符
```

### 2. 保留关键字

| abstract      |  arguments  |        await*|   boolean    |
| :-------- | :--------| :--------| :--------|
|break| byte | case| catch|
|char|class*| case| catch|
|char|class|const|continue|
|debugger|default|delete|do|
|double|else|enum*|eval|
|export*|extends*|false|final|
|finally|float|for|function|
|goto|if|implements|import*|
|in|instanceof|int|interface|
|let*|long|native|new|
|null|package|private|protected|
|public|return|short|static|
|super*|switch|synchronized|this|
|throw|throws|transient|true|
|try|typeof|var|void|
|volatile|while|with|yield|
上面带*的是ECMAScript 5 and 6新加的关键字

**下面的保留关键字已经从ECMAScript 5 and 6标准中移除**

| abstract      |     boolean |   byte   |char|
| :-------- | :--------| :------ |:------ |
| double    |   final |  float  |goto|
| int    |   long |  native  |short|
| synchronized    |   throws |  transient  |volatile|


### 3. 注释
**单行注释 //**

```
// var name = 'JavaScript';
var name = 'JavaScript'; // 名字，这是用于行末的单行注释
```

**多行注释 /* */**

```
/*
 该方法用于计算
 两个数的和
 */
function sum(num1, num2) {
    return num1 + num2;
}
```

### 4. 数据类型
#### 原始数据类型(primitive types)
- string
- number 
- boolean 
- undefined
> 请注意JavaScript中只有一种数值类型number, 都是64位的双精度浮点数。不像其他编程语言有byte/short/int/long/float/double那么多数值类型.

```
var name = 'Jack';
var pi = 3.14;
var bTrue = true;
var bFalse = false;
var x;
   
alert(typeof name);    // Returns "string" 
alert(typeof pi) ;     // Returns "number"
alert(typeof bTrue);   // Returns "boolean"
alert(typeof bFalse);  // Returns "boolean"
alert(typeof x);       // Returns "undefined" (x has no value)
```
#### 对象类型
- function (function也是object)
- object

typeof操作符对于objects、arrays、null返回object
typeof操作符对于functions不返回object，而是返回function,  但其实function也是object

```
typeof {name:'John', age:34} // Returns "object"
typeof [1,2,3,4]             // Returns "object" (not "array")
typeof null                  // Returns "object"
typeof function myFunc(){}   // Returns "function"

function fn(){}
var obj = {};
console.log(fn instanceof Function)//true
console.log(obj instanceof Object)//true
console.log(fn instanceof Object)//true
console.log(obj instanceof Function)//false
```

### 5. 类型转换
#### 使用转换函数进行转换
数值转字符串

```
String(x)         // returns a string from a number variable x
String(123)       // returns a string from a number literal 123
String(100 + 23)  // returns a string from a number from an expression
```
布尔类型转字符串

```
String(false)        // returns "false"
String(true)         // returns "true"
```
日期类型转字符串

```
String(Date())      // returns "Thu Jul 17 2014 15:38:19 GMT+0200 (W. Europe Daylight Time)"
Date().toString()   // returns "Thu Jul 17 2014 15:38:19 GMT+0200 (W. Europe Daylight Time)"
```

字符串转数值

```
Number("3.14")    // returns 3.14
Number(" ")       // returns 0 
Number("")        // returns 0
Number("99 88")   // returns NaN
```
布尔类型转数值

```
Number(false)     // returns 0
Number(true)      // returns 1
```
日期类型转数值

```
d = new Date();
Number(d)          // returns 1404568027739

d = new Date();
d.getTime()        // returns 1404568027739
```

#### 自动转换

https://www.w3schools.com/js/js_type_conversion.asp

### 6. 程序控制语句
#### 条件分支语句
##### if语句

```
语法
if (condition) {
   //condition为true时执行的代码
}

if (condition) {
    //
} else {
    //
}

if (condition1) {
    //
} else if (condition2) {
   //
} else if (condition3) {
    //
} else {
    //
}
```

##### switch语句

```
语法
switch(expression) {
    case n:
        code block
        break;
    case n:
        code block
        break;
    default:
        code block
}
请注意：case后面的n可以是数值、布尔值、对象等
```

expression表达式计算一次。表达式的值和case的值逐个比较，如果匹配则执行case内的代码，如果无匹配则执行default内的代码

**示例**

```
switch (new Date().getDay()) {
    case 0:
        day = "Sunday";
        break;
    case 1:
        day = "Monday";
        break;
    case 2:
        day = "Tuesday";
        break;
    case 3:
        day = "Wednesday";
        break;
    case 4:
        day = "Thursday";
        break;
    case 5:
        day = "Friday";
        break;
    case 6:
        day = "Saturday";
}
```

#### 循环语句
> ***JavaScript supports different kinds of loops:***
**for** - loops through a block of code a number of times
**for/in** - loops through the properties of an object
**while** - loops through a block of code while a specified condition is true
**do/while** - also loops through a block of code while a specified condition is true

##### for循环

```
语法:
for (语句1; 语句2;语句3) {
    code block to be executed
}
语句1：在循环开始之前执行一次
语句2：循环条件，每次循环开始时都执行，结果为true则执行循环体，否则循环结束
语句3：每次循环结束后都执行
注：语句1、语句2、语句3都是可缺省的
```

***示例***

```
var sum = 0;
for (var i = 0; i < 5; i++) {
    sum += i;
}
alert(sum);
//输出: 10
```

##### for in 循环
for in循环用于遍历对象的属性

```
var person = {firstName:'Jandy', lastName:'Way', sex:'Male'}
var output = "";
var x;
for (x in person) {
    output += person[x] + ' ';
}
alert(output);
//输出：Jandy Way Male
```

##### while循环

```
语法:
while (condition) {
    code block to be executed if condition is true
}
//每次循环体之前都执行循环条件的检查，循环条件为true则执行循环体代码，否则结束循环
```

***示例***

```
var sum = 0;
var i = 0;
while (i < 5) {
    sum += i;
    i++;
}
alert(sum);
//输出10
```

##### do while循环

```
语法:
do {
    code block to be executed (be executed at least once)
} while (condition);

特点：循环体内代码至少执行一次
```

***示例***

```
var i = 0;
var sum = 0;
do {
    sum += i;
    i++;
} while (i < 5);
alert(sum);
//输出: 10
```
    
##### break / continue
break用在switch语句中表示分支条件代码执行结束，for循环, while / do while循环中表示跳出整个循环
continue用在for循环, while / do while循环中, 表示跳过当次循环

```
var name = 'GM';
switch (name) {
    case 'JavaScript' :
        alert('JavaScript');
        break;
        alert('这一行在break之后，所以不会被执行');
    case 'GM': 
        alert('GM')
        alert('这一行在break之前，所以会被执行');
        break;
}
//输出: JavaScript

for (var i=0; i<3; i++) {
    if (i == 1) {
        break;
    }
    alert(i);
}
//输出: 0

for (var i=0; i<3; i++) {
    if (i == 1) {
        continue;
    }
    alert(i);
}
//输出: 0 2
```

### 7. 运算语句/运算符

#### 算术运算符
***适用于数值(numbers)变量或数值字面量的运算符***
| Operator      |     Description | 
| :-------- | :--------|
|+  |加（Addition）|
|-  |减（Subtraction）|
|*  |乘（Multiplication）|
|/  |除（Division）|
|%  |求余数（Modulus）|
|++ |自增（Increment）|
|-- |自减（Decrement）|

***示例***
    
```
var x = 8;
var y = 9;
// + 加
var z = x + y; //17

// - 减
var z = x - y; //-1

// * 乘
var z = x * y; //72

// / 除
var z = x / y; //0.8888888888888888

// % 求余数, 支持整数、浮点数的求余操作
var z = x % y; //8
var z = 8.2 % 9; //8.2
var z = 8.1 % 8.1; //0
var z = 8.2 % 8.1; //0.09999999999999964

// ++ 自增
var i = 8;
var z = i++;//先参与运算，然后才自增
alert(z);//8
alert(i);//9

var i = 8;
var z = ++i;//先自增, 然后参与运算
alert(z);//9
alert(i);//9

// -- 自减
var i = 8;
var z = i--;//先参与运算，然后才自减
alert(z);//8
alert(i);//7

var i = 8;
var z = --i;//先自减, 然后参与运算
alert(z);//7
alert(i);//7
```

#### 比较运算符
***假设x = 5***
| Operator      |     Description |   Comparing   |  Returns|
| :-------- | :--------| :------ | :------ |
| == | equal to | x == 8<br />x == 5<br />x == "5"| false<br />true<br />true |
| === | equal value and equal type | x===  5 <br /> x=== "5" | true<br /> false |
| != | not equal | x != 8 | true    |
| !== | not equal value or not equal type | x !== 5<br />x !== "5"<br />x !== 8 | false<br />true<br />true |
| &gt;  | greater than  | x &gt; 8  | false |
| &lt   | less than | x &lt 8   | true |
| &ge;= | greater than or equal to | x &ge;= 8 | false |
| &le;= | less than or equal to | x &le;= 8 | true |

***示例***

```
var age = 22;
if (age < 18) {
    alert('Too young!')
}
```

##### 不同数据类型之前的比较
**boolean布尔类型与number数值类型之间的比较**，会将布尔类型转换成数值类型(true转为1，false转为0)

```
console.log( true == 1) //true
console.log( false == 0) //true
```

**number数值类型与string字符串类型之间比较**，会将字符串转为数值(空字符串转换成0, 非数字字符串转换为NaN且比较结果总是返回false)

```
console.log( '' == 0)//true
console.log( '2' == 2)//true
console.log( '2a' == 2)//false
```

**boolean布尔类型与string字符串类型之间比较,** 会将布尔类型转换成数值类型(true转为1，false转为0), 将字符串转为数值(空字符串转换成0，非数字字符串转换为NaN且比较结果总是返回false)

```
console.log( false == '0')//true
console.log( true == '1')//true
```

**undefined类型与其他类型比较**总是返回false

```
console.log(undefined == undefined);//true
console.log(undefined == 'undefined');//false

console.log(undefined == 1);//false
console.log(undefined == '2');//false
console.log(undefined == true);//false
console.log(undefined == false);//false
console.log(undefined == {});//false

console.log(undefined > 1);//false
console.log(undefined >'2');//false
console.log(undefined > true);//false
console.log(undefined > false);//false

console.log(undefined < {});//false
console.log(undefined < 1);//false
console.log(undefined < '2');//false
console.log(undefined < true);//false
console.log(undefined < false);//false
console.log(undefined < {});//false
```

**对象类型与非对象类型比较总是返回false,  两个不同的对象之间比较总是返回false** 

```
var obj1 = {};
var obj2 = {};
console.log(obj1 == obj2);//false
console.log(obj1 == obj1);//true
```

#### 逻辑运算符
***假设x = 6, y = 3***

| Operator | Description | Example |
| :-------- | :--------| :------ |
| &&    | 与 and：两个都是true结果才为true否则为false|  (x < 10 && y > 1) is true | 
| &#124;&#124;  | 或 or：其中一个为true结果就为true否则为false| (x == 5 &#124;&#124; y == 5) is false | 
| ! |  非 not: 取反|  !(x == y) is true | 

***示例***

```
//&&是短路与, ||是短路或, 即如果左侧的表达式已经可以决定最终结果，则右侧的表达式不执行计算
var x = 10;
if (10 < 9 && (x = 12)) {
    alert(x);
}
alert(x);
//输出10，而不是12， 因为左侧10<9的结果false已经可以决定整个&&操作的结果是false，右侧x=12表达式不执行
```

#### 条件运算符

```
语法
variablename = (condition) ? value1:value2 

等价于
var variablename;
if (condition) {
    variablename = value1;
} else {
    variablename = value2;
}
```
    
***示例***

```
var age = 17;
var tip = (age >= 18) ? '大家都成年人了, 一起玩' : '未成年人请自觉离开';
console.log(tip);
//输出：未成年人请自觉离开
```

#### 位运算符

| Operator      |     Name |   Description   |
| :-------- | :--------| :------ |
| & | AND   Sets each bit to 1 if both bits are 1 | 
| &#124; | OR   | Sets each bit to 1 if one of two bits is 1 | 
| ^ | XOR   | Sets each bit to 1 if only one of two bits is 1 | 
| ~ | NOT   | Inverts all the bits | 
| <<    | Zero fill left shift  Shifts left by pushing zeros<br/> in from the right and let the leftmost bits fall off | |
| \>\>  | Signed right shift    Shifts right by pushing copies<br/> of the leftmost bit in from the left, and let the rightmost bits fall off |  |
| \>\>\>    | Zero fill right shift Shifts right by pushing zeros<br/> in from the left, and let the rightmost bits fall off | | 

示例：

| Operation      |     Result |   Same as   | Result |
| :-------- | :--------| :--------|:--------|
| 5 & 1  | 1     | &nbsp;&nbsp;&nbsp;0101 <br/>& <br />&nbsp;&nbsp;&nbsp;0001     | 0001 | 
 | 5 &#124; 1    | 5     | &nbsp;&nbsp;&nbsp;0101<br/> &#124; <br/>&nbsp;&nbsp;&nbsp;0001    |  0101 | 
 | ~ 5   | 10     | ~0101 | 1010 | 
 | 5 << 1    | 10    | 0101 << 1     |  1010 | 
 | 5 ^ 1     | 4     | 0101 ^ 0001   |  0100 | 
 | 5 >> 1    | 2     | 0101 >> 1     |  0010 | 
 | 5 >>> 1   | 2     | 0101 >>> 1    |  0010 | 


#### 赋值运算符
| Operator | Example | Same As  |
| :-------- | :--------| :------ |
|=  |x = y  |x = y|
|+= |x += y |x = x + y|
|-= |x -= y |x = x - y|
|*= |x *= y |x = x * y|
|/= |x /= y |x = x / y|
|%= |x %= y |x = x % y|
|<<= |x <<= y |x = x << y|
|>>= |x >>= y |x = x >> y|
|>>>=   |x >>>= y |x = x >>> y|
|&= |x &= y |x = x & y|
|^= |x ^= y |x = x ^ y|
|&#124;= |x &#124;= y |x = x &#124; y|
|**=    |x **= y    |x = x ** y|

### 8. 函数

JavaScript函数(function)就是实现特定任务的一段代码。

```
语法：与其他编程语言不同，JavaScript函数的参数不需要指定数据类型
function functionName(parameter1, parameter2, parameter3) {
    //code to be executed
}
```
> **parameters**就是函数定义的参数名字. 参数可缺省
> **arguments**就是函数调用时实际传人parameter参数的值
> 在函数内部，arguments(parameters)当做**局部变量**处理
> 使用**( )**来调用函数
> 使用**return**来返回结果

***示例:***

```
function printAge() {
    //不带参数的函数
    var age = 20;
    alert(age);
}

function setUser(name, age) {
    //带参数的函数
    alert(name, age);
}

function getAge() {
    //有返回值的函数
    var age = 30;
    return age;
}

function toCelsius(fahrenheit) {
    return (5/9) * (fahrenheit-32);
}

var x = toCelsius(77);
var text = "The temperature is " + x + " Celsius";
var text2 = "The temperature is " + toCelsius(77) + " Celsius";
```

函数本身也是一个变量

```
function sum(a, b) {
    return a + b;
}

var myFunc =  sum;
var result = myFunc(12, 10);
alert(result);
```

### 9. 作用域
JavaScript中变量有两种类型的作用域
1. 局部作用域(也叫函数作用域)
2. 全局作用域
> ES6后引入了块作用域，使用let声明定义变量： let carName = 'Toyota';

#### 局部作用域(Local scope)
JavaScript中，函数内声明定义的变量具有局部作用域，只能在函数内部访问，函数外部无法访问函数内部定义的变量

```
function myFunction() {
    var name = 'My name is JavaScript';
    alert(name);
}
myFunction();
alert(name);//undefined, 未定义，不能访问函数内部的变量
```

    
> 函数参数是作为函数内部的局部变量

```
function setAge(age) {
    alert(age);//20
    age = 33;  
    alert(age);//33
}
var age = 20;
setAge(age);
alert(age);//20 原生数据类型作为函数调用的参数传值是用值复制的方式传递

function printPerson(person) {
    alert(person.age);//20
    person.age = 33;
    alert(person.age);//33
}

var person = {age:20};
printPerson(person);
alert(person.age);//33，对象类型作为函数调用参数的传值是用引用复制的方式传递
```

#### 全局作用域
JavaScript中，函数外声明定义的变量具有全局作用域，其他地方都可以访问

```
var carName = 'Toyota'
alert(carName);

function myFunction() {
    alert(carName);//函数内部可以访问全局变量
}
myFunction();
```

>在JavaScript中，对象和函数也是变量

**自动成为全局作用域变量**
当给一个未声明的变量赋值时，该变量会自动成为具有全局作用域的变量

```
myFunction();
alert(myCarName);//输出Toyota

function myFunction() {
    myCarName = 'Toyota';//未声明变量，直接赋值，该变量自动成为全局变量
}
```

#### 变量生命周期
变量的生命周期从变量声明时开始，局部变量（或函数内变量）在函数结束时被删除，全局变量在关闭浏览器Window或Tab时被删除。

### 10. 对象
> JavaScript **variables** are **containers** for **data values**.
> **Objects** are variables too. But objects **can contain many values**. 
> The **values** are written as **name:value** pairs (name and value separated by a colon).

#### 定义对象
1. **使用大括号定义对象,  属性名和值之间使用冒号**:**分割,  属性之间使用逗号**,**分割**

```
{
    name1 : value1,
    name2 : value2,
}
```
2. **使用new创建对象**

```
var obj = new Object();
var no = new Number(12);
var bo = new Boolean(true);
var so = new String('13');
```

示例:

```
var person = {
    name : 'JavaScritp', 
    age : 19,
    isPretty : true,
    getAgeAndName: function() {
        return this.age + this.name;
    },
    setAgeAndName: function(age, name) {
        this.age = age;
        this.name = name;
    }
}
person.setAgeAndName(30, 'JS');
console.log(person.name);
console.log(person.age);
console.log(person.isPretty);
console.log(person.getAgeAndName());

等价于

var person = new Object();
person.name = 'JavaScritp';
person.age = 19;
person.isPretty = true;
person.getAgeAndName = function() {
    return this.age + this.name;
}
person.setAgeAndName = function(age, name) {
    this.age = age;
    this.name = name;
}
person.setAgeAndName(30, 'JS');
console.log(person.name);
console.log(person.age);
console.log(person.isPretty);
console.log(person.getAgeAndName());
```

#### 访问对象的属性

```
objectName.propertyName

或者

objectName["propertyName"]
```

#### 访问对象的方法

```
objectName.methodName()

//比如：
name = person.fullName();
person.setAgeAndName(30, 'JS');
```
#### 给对象添加属性或方法
在JavaScript中可以通过赋值的方式给对象添加属性和方法
```
var person = {age:12, sex:'male'};
//添加name属性
person.name = 'JS';
//添加getNameAndAge方法
person.getNameAndAge = function() {
    return this.name + this.age;
}
console.log(person.name);//JS
console.log(person.getNameAndAge());//JS12
```
#### 不要将字符串、数值、布尔类型声明为对象类型
不要将字符串、数值、布尔类型声明为对象类型，这将让你的代码变得复杂而且执行速度变慢.

```
var str = 'a';
var num = 12;
var b = true;
var strObj = new String('a');       // Declares strObj as a String object
var numObj = new Number(12);        // Declares numObj as a Number object
var bObj = new Boolean(true);       // Declares bObj as a Boolean object
console.log(typeof str);//string
console.log(typeof num);//number
console.log(typeof b);//boolean
console.log(typeof strObj);//object
console.log(typeof numObj);//object
console.log(typeof bObj);//object
```

#### 在JavaScript中对象就是国王
In JavaScript, objects are king. If you understand objects, you understand JavaScript.

In JavaScript, almost "everything" is an object.

- Booleans can be objects (if defined with the new keyword)
- Numbers can be objects (if defined with the new keyword)
- Strings can be objects (if defined with the new keyword)
- Dates are always objects
- Maths are always objects
- Regular expressions are always objects
- Arrays are always objects
- Functions are always objects
- Objects are always objects

**All JavaScript values, except primitives, are objects.**

JavaScript Primitives
A primitive value is a value that has no properties or methods.
A primitive data type is data that has a primitive value.

JavaScript defines 5 types of primitive data types:
1. string
2. number
3. boolean
4. null
5. undefined

**Primitive values are immutable (they are hardcoded and therefore cannot be changed).**

#### 对象构造器(Object Constructor)
在之前的例子中，只是方便地定义了一个对象。当需要方便地定义很多有相同属性的对象时，需要用到对象构造器函数

```
function Person(first, last, age, eye) {
    this.firstName = first;
    this.lastName = last;
    this.age = age;
    this.eyeColor = eye;
    this.setAge = function(age) {
        this.age = age;
    }
}
var myFather = new Person("John", "Doe", 50, "blue");
var myMother = new Person("Sally", "Rally", 48, "green");
myFather.setAge(50);
myMother.setAge(51);
console.log(myFather.age + ' ' + myFather.firstName);
console.log(myMother.age + ' ' + myMother.firstName);
```
##### 内建的JavaScript对象构造器

```
var x1 = new Object();    // A new Object object
var x2 = new String();    // A new String object
var x3 = new Number();    // A new Number object
var x4 = new Boolean();   // A new Boolean object
var x5 = new Array();     // A new Array object
var x6 = new RegExp();    // A new RegExp object
var x7 = new Function();  // A new Function object
var x8 = new Date();      // A new Date object
```
#### this关键字
In JavaScript, the thing called this, is the object that "owns" the JavaScript code.

- The value of this, when used in a function, is the object that "owns" the function.

- The value of this, when used in an object, is the object itself.

- The this keyword in an object constructor does not have a value. It is only a substitute for the new object.

- The value of this will become the new object when the constructor is used to create an object.

- Note that this is not a variable. It is a keyword. You cannot change the value of this.

#### 继承

```
function Person(first, last) {
    this.firstName = first;
    this.lastName = last;
    this.setAge = function(age) {
        this.age = age;
    }
}

function Student(stID, first, last) {
    Person.call(this, first, last);
    this.stID = stID;
}

var student = new Student(10003, 'Jiandong', 'Wei');
console.log(student.stID + ' ' + student.firstName, +' ' + student.lastName);
```

### 11. 错误(异常)处理

> The **try** statement lets you test a block of code for errors.
  The **catch** statement lets you handle the error.
  The **throw** statement lets you create custom errors.
  The **finally** statement lets you execute code, after try and catch, regardless of the result.

#### 使用try/catch/finally捕捉异常

```
   try {
        //可能抛出错误或异常的代码
    } catch (err) {
        //捕捉到err错误或异常时的处理代码
    } finally {
        //在try/catch代码执行完后始终会执行的代码
    }
```
    
**示例**    

```
try {
    alert123('Ha Ha');
} catch (err) {
    alert(err.message);
}
//输出: alert123 is not defined
```
    
#### 使用throw来抛出自定义异常/错误
*异常或错误可以是: **字符串、数值、布尔值、对象***
***示例***

```
function setName(name) {
    if (typeof(name) != 'string') {
        throw 'name should be a string';
    } else {
        alert(name);
    }
}

try {
    setName(20);
} catch (err) {
    alert(err);
} finally {
    alert('-----finally----');
}
输出:
name should be a string
-----finally----
```
    
### 12. 严格模式(Strict Mode)
**"use strict";**
 这行代码将使得JavaScript代码在严格模式中被执行
use strict是Java Script1.8.5(即ECMAScript version 5)中新添加的。它不是一条语句，它是字面表达式，在旧版本的JavaScript中会被忽略。

启用严格模式只要将**"use strict";**放在代码或函数开头就可以，如果放在最开头则具有全局作用域

示例1：

```
"use strict";
x = 3.14;       // This will cause an error because x is not declared
```

示例2：

```
myFunction();
function myFunction() {
    y = 3.14;   // This will also cause an error because y is not declared
}
```

示例3：

```
//在函数内部使用"use strict"; 则只在函数内部启用了严格模式
x = 3.14;       // This will not cause an error. 
myFunction();
function myFunction() {
    "use strict";
    y = 3.14;   // This will cause an error
}
```

#### 为什么使用严格模式Strict Mode
1. 严格模式使得更容易编写安全的JavaScript代码
2. 严格模式下将之前可接受的但不良的语法写法当成是错误来处理 

#### 严格模式下不允许的行为：
1. 不允许使用未声明的变量(或对象)

```
"use strict";
x = 3.14;                // This will cause an error
x = {p1:10, p2:20};      // This will cause an error
```

2. 不允许删除变量（或对象）

```
"use strict";
var x = 3.14;
delete x;                // This will cause an error
```

3. 不允许删除函数

```
"use strict";
function x(p1, p2) {}; 
delete x;                // This will cause an error 
```

4. 函数的参数名不能重复

```
"use strict";
function x(p1, p1) {};   // This will cause an error
```

5. 不允许使用八进制的数值字面值

```
"use strict";
var x = 010;             // This will cause an error
```

6. Escape characters are not allowed

```
"use strict";
var x = \010;            // This will cause an error
```
    
7. 不允许对只读(read-only)属性进行写操作

```
"use strict";
var obj = {};
Object.defineProperty(obj, "x", {value:0, writable:false});
obj.x = 3.14;            // This will cause an error
```

8. 不允许对只取(get-only)属性进行写操作

```
"use strict";
var obj = {get x() {return 0} };
obj.x = 3.14;            // This will cause an error
```

9. 不允许删除“不可删除"的属性

```
"use strict";
delete Object.prototype; // This will cause an error
```

10. 不允许使用eval作为变量名

```
"use strict";
var eval = 3.14;         // This will cause an error
```

11. 不允许使用arguments作为变量名

```
"use strict";
var arguments = 3.14;    // This will cause an error
```

12. 不允许使用with语句

```
"use strict";
with (Math){x = cos(2)}; // This will cause an error
```

13. For security reasons, eval() is not allowed to create variables in the scope from which it was called

```
"use strict";
eval ("var x = 2");
alert (x);               // This will cause an error
```
14. In function calls like f(), the this value was the global object. In strict mode, it is now undefined.


### 13. Boolean(布尔类型)

布尔类型只有两个值: true false
#### Boolean()函数
```
Boolean(10 > 9) // returns true
Boolean(10 < 9) // returns false

简写

(10 > 9) // returns true
10 > 9   // returns true
```

#### Comparisons and Conditions
表达式的布尔值结果是JavaScript中比较运算和条件运算的基础
| Operator | Description | Example |
| :------- | :---------- | :------ |
|  ==      | equal to    | if (day == "Monday") |
|  >       | greater than | if (salary > 9000) |
|  <       | less than    | if (age < 18) |

#### Everything With a "Real" Value is True
```
console.log(Boolean(100)); //true
console.log(Boolean(3.14)); //true
console.log(Boolean(-15)); //true
console.log(Boolean("Hello")); //true
console.log(Boolean("false")); //true
console.log(Boolean(7 + 1 + 3.14)); //true
console.log(Boolean(5 < 6)); //true

```

#### Everything Without a "Real" Value is False
- The Boolean value of 0 (zero) is false:
```
var x = 0;
console.log(Boolean(x)); //false

```
- The Boolean value of -0 (minus zero) is false:
```
var x = -0;
console.log(Boolean(x)); //false
```
- The Boolean value of "" (empty string) is false:
```
var x = '';
console.log(Boolean(x)); //false
```
- The Boolean value of undefined is false:
```
var x;
console.log(Boolean(x)); //false
```

- The Boolean value of null is false:
```
var x = null;
console.log(Boolean(x)); //false
```
- The Boolean value of false is (you guessed it) false:
```
var x = false;
console.log(Boolean(x)); //false
```

- The Boolean value of NaN is false:
```
var x = 10 / 'H';
console.log(Boolean(x)); //false
```

#### 布尔对象
通常，通过字面值创建的是原始数据类型
var x = false; //boolean
但同样可以通过new创建布尔对象类型
var y = new Boolean(false);
var y2 = new Boolean(true);
```
var x = false;
var y = new Boolean(false);
console.log(typeof x); //boolean
console.log(typeof y); //object

```
请不要创建布尔对象类型，它会导致执行速度变慢。 new关键字使得代码变复杂。 会产生一些不可预期的结果。

```
var x = false;
var y = new Boolean(false);
var y2 = new Boolean(false);

console.log(x == y);  // x == y is true because x and y have equal values.
console.log(x === y); // x === y is false because x and y have different types.
console.log(y == y2); // y == y2 is false because objects cannot be compared. 

```

**原始的布尔类型boolean是没有属性和方法的，但为什么我们可以对原始布尔类型使用属性和方法呢。原因是当原始布尔类型使用属性或方法时会被JavaScript当做对象看待。**

#### 布尔对象类型的属性列表
| Property | Description |
| :------- | :---------- |
| constructor | Returns the function that created JavaScript's Boolean prototype |
| (__proto__)prototype | Allows you to add properties and methods to the Boolean prototype |

#### 布尔对象类型的方法列表
| Method | Description |
| :------- | :---------- |
| toString() | Converts a boolean value to a string, and returns the result |
| valueOf() | Returns the primitive value of a boolean |

```
var x = false;
console.log(x.constructor); //ƒ Boolean() { [native code] }
console.log(x.__proto__); //Boolean {[[PrimitiveValue]]: false, constructor: ƒ, toString: ƒ, valueOf: ƒ}
console.log(x.toString() == 'false'); //true
console.log(x.valueOf() == false); //true
```

### 14. Number(数值类型)
在JavaScript中只有一种数值类型，数值是带小数点的浮点数也可以是不带小数点的整数。不像其他编程语言，JavaScript没有byte/short/int/long/float/double这些数值类型。
```
var x = 3.14;//带小数点
var y = 3;//不带小数点
```
很大或很小的数可以使用科学计数法的写法
```
var x = 123e5;   //12300000
var y = 123e-5;  //0.00123
```
#### JavaScript数值始终是64位的双精度的浮点数
|Value (aka Fraction/Mantissa)|Exponent指数|Sign符号位|
|:--|:--|:--|
|2 bits (0 - 51) |11 bits (52 - 62)|1 bit (63)|
精度
Integers (numbers without a period or exponent notation) are accurate up to 15 digits.
```
var x = 999999999999999;   // x will be 999999999999999
var y = 9999999999999999;  // y will be 10000000000000000
```
小数点后最大占17位，而且浮点数运算不总是100%精确
```
var x = 0.2 + 0.1;         
console.log(x); // x will be 0.30000000000000004

//解决这个问题可以用先乘后除的方法
var x2 = (0.2 * 10 + 0.1 * 10) / 10; // x will be 0.3
console.log(x2);

```

> 警告
> JavaScript中+操作符可用于加法运算和连接操作
> 在数值之间使用+操作符时是进行加法运算，在字符串中使用+操作符时是进行字符串连接操作

#### 相加操作
1. 如果是两个数值相加，结果是数值
```
var x = 10;
var y = 20;
var z = x + y; // z will be 30 (a number)
```
2. 如果是两个字符串相加, 结果是字符串的连接
```
var x = '10';
var y = '20';
var z = x + y; // z will be 1020 (a string)
```
3. 如果是数值和字符串相加，结果是字符串的连接
```
var x1 = 10;
var y1 = '20';
var z1 = x + y; // z1 will be 1020 (a string)

var x2 = '10';
var y2 = 20;
var z2 = x + y; // z2 will be 1020 (a string)
```
4. 常见的错误场景
```
var x = 10;
var y = 20;
var z = 'The result is: ' + x + y;//错误期望:The result is: 30  结果：The result is: 1020
console.log(z);

var x2 = 10;
var y2 = 20;
var z2 = '30';
var result = x2 + y2 + z2;//错误期望:102030  结果：3030
console.log(result);
```
> JavaScript编译器是从左到右执行的。
> 先是 10 + 20 数值相加等于30， 然后30 + ‘30’进行字符串连接等于3030

#### 数值型字符串
JavaScript中字符串可以包含数值内容
```
var x = 100; // x is a nubmer;
var y = '100'; // y is a string
```
JavaScript在数值运算中会尝试将字符串转成数值
```
var x = '100';
var y = '10';
var z = x / y; // z will be 10
console.log(z);

var z2 = x * y // z2 will be 1000
console.log(z2);

var z3 = x - y // z3 will be 90
console.log(z3);

var z4 = x + y // z3 will be 10010 注意这里执行的是字符串连接
console.log(z4);
```

#### NaN - Not a Number
NaN is a JavaScript reserved word indicating that a number is not a legal number.
Trying to do arithmetic with a non-numeric string will result in NaN (Not a Number):
```
var x = 100 / 'Apple'; // x will be NaN (Not a Number)
console.log(x);

```

You can use the global JavaScript function isNaN() to find out if a value is a number:
```
var x = 100 / 'Apple'; // x will be NaN (Not a Number)
console.log(isNaN(x)); // true
```
- 如果在数学运算中使用NaN, 那么结果也将是NaN
```
var x = NaN;
var y = 5;
var z = x + y; // z will be NaN
console.log(z);

var x1 = NaN;
var y1 = "5";
var z1 = x1 + y1; // z1 will be NaN5
console.log(z1);
```

- NaN is a number: typeof NaN returns number:
```
console.log(typeof NaN); // number
```

#### Infinity无穷
Infinity (or -Infinity) is the value JavaScript will return if you calculate a number outside the largest possible number.
```
var myNumber = 2;
while (myNumber != Infinity) {          // Execute until Infinity
    myNumber = myNumber * myNumber;
}
```
除于0的结果是Infinity
```
var x = 2 / 0;   // x will be Infinity
var y = - 2 / 0; // y will be -Infinity
console.log(x);
console.log(y);
```
Infinity is a number: typeof Infinity returns number.
```
console.log(typeof Infinity); // number
```
#### 16进制表示
- JavaScript中将0x开头的数值常量解释为16进制数值。通常的数值都是10进制的。
```
var x = 0xFF; // x will be 255
console.log(x);
```
- 使用toString函数转换成其他进制的字符串
```
var myNumber = 128;
console.log(myNumber.toString(16)); //returns 80
console.log(myNumber.toString(8));  //returns 200
console.log(myNumber.toString(2));  //returns 10000000
```

#### 数值对象
通常从字面值创建的是原始的数值类型，但同样可以用new关键字创建数值对象。但是请不要创建数值对象，它将降低执行速度， new关键字使得代码变复杂，且会产生一些不可预期的结果。
```
var x = 123;
var y = new Number(123);
var y2 = new Number(123);
console.log(typeof x); // number
console.log(typeof y); // object
console.log(x == y);   // (x == y) is true because x and y have equal values
console.log(x === y);   // (x === y) is false because x and y have different types
console.log(y == y2);   // (y === y2) is false because objects cannot be compared

```

#### Number对象的属性列表
| Property | Description |
| :------- | :---------- |
| constructor | Returns the function that created JavaScript's Number prototype |
| (__proto__)prototype | Allows you to add properties and methods to the Number prototype |
|MAX_VALUE | Returns the largest number possible in JavaScript|
|MIN_VALUE | Returns the smallest number possible in JavaScript|
| NEGATIVE_INFINITY| Represents negative infinity (returned on overflow)|
| POSITIVE_INFINITY| Represents infinity (returned on overflow)|
| NaN| Represents a "Not-a-Number" value|

```
var x = 0.0;
console.log(Number.MAX_VALUE); //1.7976931348623157e+308
console.log(Number.MIN_VALUE); //5e-324
console.log(Number.NEGATIVE_INFINITY); //-Infinity
console.log(Number.POSITIVE_INFINITY); //Infinity
console.log(Number.NaN); //NaN
console.log(x.constructor); //ƒ Number() { [native code] }
console.log(x.__proto__); //Number {constructor: ƒ, toExponential: ƒ, toFixed: ƒ, toPrecision: ƒ, toString: ƒ, …}
```

#### Number对象的方法列表
| Method | Description |
| :------- | :---------- |
| isFinite() | Checks whether a value is a finite number |
| isInteger() | Checks whether a value is an integer |
| isNaN() | Checks whether a value is Number.NaN |
| isSafeInteger() | Checks whether a value is a safe integer |
| toExponential(x) | Converts a number into an exponential notation, returns string|
| toFixed(x) | Formats a number with x numbers of digits after the decimal point, returns string|
| toPrecision(x) | Formats a number to x length, returns string |
| toString() | Converts a number to a string |
| valueOf() | Returns the primitive value of a number |
```
Number.isFinite(123) //true
Number.isFinite(-1.23) //true
Number.isFinite(5-2) //true
Number.isFinite(0) //true
Number.isFinite('123') //false
Number.isFinite('Hello') //false
Number.isFinite('2005/12/12') //false
Number.isFinite(Infinity) //false
Number.isFinite(-Infinity) //false
Number.isFinite(0 / 0) //false

Number.isInteger(123) //true
Number.isInteger(-123) //true
Number.isInteger(5-2) //true
Number.isInteger(0) //true
Number.isInteger(0.5) //false
Number.isInteger('123') //false
Number.isInteger(false) //false
Number.isInteger(Infinity) //false
Number.isInteger(-Infinity) //false
Number.isInteger(0 / 0) //false

Number.isNaN(123) //false
Number.isNaN(-1.23) //false
Number.isNaN(5-2) //false
Number.isNaN(0) //false
Number.isNaN('123') //false
Number.isNaN('Hello') //false
Number.isNaN('2005/12/12') //false
Number.isNaN('') //false
Number.isNaN(true) //false
Number.isNaN(undefined) //false
Number.isNaN('NaN') //false
Number.isNaN(NaN) //true
Number.isNaN(0 / 0) //true

Number.isSafeInteger(123) //true
Number.isSafeInteger(-123) //true
Number.isSafeInteger(5-2) //true
Number.isSafeInteger(0) //true
Number.isSafeInteger(0.5) //false
Number.isSafeInteger(Math.pow(2, 53)) //false
Number.isSafeInteger(Math.pow(2, 53) - 1) //true
Number.isSafeInteger('123') //false
Number.isSafeInteger(false) //false
Number.isSafeInteger(Infinity) //false
Number.isSafeInteger(-Infinity) //false
Number.isSafeInteger(0 / 0) //false

var num = 5.56789;
var n = num.toExponential(); //5.56789e+0

var num2 = 52.56789;
var n2= num2.toExponential(); //5.256789e+1

var x = 9.656;
x.toExponential(2);     // returns 9.66e+0
x.toExponential(4);     // returns 9.6560e+0
x.toExponential(6);     // returns 9.656000e+0

var x = 9.656;
x.toFixed(0);           // returns 10
x.toFixed(2);           // returns 9.66
x.toFixed(4);           // returns 9.6560
x.toFixed(6);           // returns 9.656000

var x = 9.656;
x.toPrecision();        // returns 9.656
x.toPrecision(2);       // returns 9.7
x.toPrecision(4);       // returns 9.656
x.toPrecision(6);       // returns 9.65600

var num = 15;
var n = num.toString(); //15 string

var x = 123;
x.valueOf();            // returns 123 from variable x
(123).valueOf();        // returns 123 from literal 123
(100 + 23).valueOf();   // returns 123 from expression 100 + 23

```

#### 将变量转换成数值
有3个JavaScript方法可以用来将变量转换成数值, 这个3个方法是的JavaScript的全局方法(Global Methods)
- Number(x) Returns a number, converted from its argument.
- parseInt(x) Parses its argument and returns an integer
- parseFloat(x) Parses its argument and returns a floating point number


**Number(x)方法**
```
x = true;
Number(x);        // returns 1
x = false;     
Number(x);        // returns 0
x = new Date();
Number(x);        // returns 1404568027739
x = "10"
Number(x);        // returns 10
x = "10 20"
Number(x);        // returns NaN
```

**parseInt(x)方法**
parseInt() parses a string and returns a whole number. Spaces are allowed. Only the first number is returned.
If the number cannot be converted, NaN (Not a Number) is returned.
```
parseInt(10);           // returns 10
parseInt(10.99);        // returns 10
parseInt("10");         // returns 10
parseInt("10.33");      // returns 10
parseInt("10 20 30");   // returns 10
parseInt("10 years");   // returns 10
parseInt("years 10");   // returns NaN 
parseInt(true);         // returns NaN 
parseInt(false);         // returns NaN 

```
**parseFloat(x)方法**
parseFloat() parses a string and returns a number. Spaces are allowed. Only the first number is returned.
If the number cannot be converted, NaN (Not a Number) is returned.
```
parseFloat(10);          // returns 10
parseFloat(10.33);       // returns 10.33
parseFloat("10");        // returns 10
parseFloat("10.33");     // returns 10.33
parseFloat("10 20 30");  // returns 10
parseFloat("10 years");  // returns 10
parseFloat("years 10");  // returns NaN
parseFloat(true);        // returns NaN
parseFloat(false);       // returns NaN
```

### 15. String(字符串)
JavaScript的字符串用于存储和操纵文本, 使用单引号或双引号包围。
```
var carname = "Volvo XC60";
var carname = 'Volvo XC60';
var answer = "It's alright";
var answer = "He is called 'Johnny'";
var answer = 'He is called "Johnny"';
```

#### 特殊字符进行转义: \escape character
```
var x = 'It\'s alright';
var y = "We are the so-called \"Vikings\" from the north."
```

| Code  | Outputs  |
| :---- | :--------|
| \'  | single quote  |
| \"  | double quote  |
| \\  | backslash  |
| \b  | Backspace  |
| \r  | Carriage Return  |
| \t  | Horizontal Tabulator  |
| \v  | Vertical Tabulator  |

#### 长字符串断行
```
var longText = 'Hello \
World!';

//A safer way to break up a string, is to use string addition:
var longText = 'Hello '+ 
               'World!';
```

#### 字符串对象
通常从字面值创建字符串的是原始类型，但同样可以用new关键字创建字符串对象。但是请不要创建字符串对象，它将降低执行速度，new关键字使得代码变复杂，且会产生一些不可预期的结果。
```
var x = 'John';
var y = new String('John');
var y2 = new String('John');
console.log(x == y);//(x == y) is true because x and y have equal values
console.log(x === y);// (x === y) is false because x and y have different types (string and object)
console.log(y == y2);//(y == y2) is false because y and y2 are different objects

```

> Primitive values, like "John Doe", cannot have properties or methods (because they are not objects).
> But with JavaScript, methods and properties are also available to primitive values, because JavaScript treats primitive values as objects when executing methods and properties.

#### String的属性列表
| Property | Description |
| :------- | :---------- |
| constructor | Returns the string's constructor function |
| (\_\_proto\_\_)prototype | Allows you to add properties and methods to the Boolean prototype |
|length | Returns the length of a string|
```
var str = 'Mr. Wei';
console.log(str.constructor); // ƒ String() { [native code] }
console.log(str.__proto__);   // tring {length: 0, constructor: ƒ, charAt: ƒ, charCodeAt: ƒ, concat: ƒ, …}
console.log(str.length);      // 7
```

#### 字符串的方法列表
| Method | Description |
| :------- | :---------- |
| charAt() | Returns the character at the specified index (position) |
| charCodeAt() | Returns the Unicode of the character at the specified index |
| concat() | Joins two or more strings, and returns a new joined strings |
| endsWith() | Checks whether a string ends with specified string/characters |
| fromCharCode() | Converts Unicode values to characters |
| includes() | Checks whether a string contains the specified string/characters |
| indexOf() | Returns the position of the first found occurrence of a specified value in a string |
| lastIndexOf() | Returns the position of the last found occurrence of a specified value in a string |
| localeCompare() | Compares two strings in the current locale |
| match() | Searches a string for a match against a regular expression, and returns the matches |
| repeat() | Returns a new string with a specified number of copies of an existing string |
| replace() | Searches a string for a specified value, or a regular expression, and returns a new string where the specified values are replaced |
| search() | Searches a string for a specified value, or regular expression, and returns the position of the match |
| slice() | Extracts a part of a string and returns a new string |
| split() | Splits a string into an array of substrings |
| startsWith() | Checks whether a string begins with specified characters |
| substr() | Extracts the characters from a string, beginning at a specified start position, and through the specified number of character |
| substring() | Extracts the characters from a string, between two specified indices |
| toLocaleLowerCase() | Converts a string to lowercase letters, according to the host's locale |
| toLocaleUpperCase() | Converts a string to uppercase letters, according to the host's locale |
| toLowerCase() | Converts a string to lowercase letters |
| toString() | Returns the value of a String object |
| toUpperCase() | Converts a string to uppercase letters |
| trim() | Removes whitespace from both ends of a string |
| valueOf() | Returns the primitive value of a String object |
> All string methods return a new value. They do not change the original variable.

##### length: 字符串长度
```
var txt = "ABCDEFGHIJKLMNOPQRSTUVWXYZ";
var sln = txt.length;
```

- indexOf(x)/indexOf(x, startPosition)
The indexOf() method returns the index of (the position of) the first occurrence of a specified text in a string
startPosition是可缺省的，缺省时startPosition默认值是0
```
var str = 'bcc1123'
console.log(str.indexOf(1)); //3
console.log(str.indexOf('c')); //1
console.log(str.indexOf('c', 2)); //2 包含起始位置
console.log(str.indexOf('c', 3)); //-1
```
##### lastIndexOf(x)/lastIndexOf(x, startPosition)
The lastIndexOf() method returns the index of the last occurrence of a specified text in a string
注意lastIndexOf是从后往前找的，startPosition缺省时默认值是字符串的长度
```
var str2 = 'bcc1123'
console.log(str2.lastIndexOf(1)); //4
console.log(str2.lastIndexOf('c')); //2
console.log(str2.lastIndexOf('c', 0)); //-1

```
> Both the indexOf(), and the lastIndexOf() methods return -1 if the text is not found.
> JavaScript counts positions from zero. 0 is the first position in a string, 1 is the second, 2 is the third ...

##### search(x)
The search(x) method searches a string for a specified value and returns the position of the match. 
The search(x) methods return -1 if the text is not found.
```
var str = "Please locate where 'locate' occurs!";
console.log(str.search("locate"));
```
indexOf()和search()的区别
1. search()没有起始位置参数
2. search()支持正则表达式

> 能提取字符串的函数
1. slice(start, end)
2. substring(start, end)
3. substr(start, length)

##### slice(start, end) 裁切字符串
***注意包含start但不包含end***
slice() extracts a part of a string and returns the extracted part in a new string.
The method takes 2 parameters: the starting index (position), and the ending index (position).
This example slices out a portion of a string from position 7 to position 13:
```
var str = "0123456789";
var res = str.slice(0, 4);
console.log(res); // 0123
```
如果position是负数则表示从后往前数的位置
```
var str = "0123456789";
var res = str.slice(-3, -1);
console.log(res); // 78
```
如果省略第二个参数(end), 则表示从开始位置一直到字符串的结尾
```
var str = "0123456789";
var res = str.slice(2);
console.log(res); // 23456789
```

##### substring(start, end)
***注意包含start但不包含end***
substring(start, end)不支持负数的位置
```
var str = "0123456789";
var res = str.substring(0, 4);
console.log(res); // 0123
```
如果省略第二个参数(end), 则表示从开始位置一直到字符串的结尾
```
var str = "0123456789";
var res = str.substring(2);
console.log(res); // 23456789
```

##### substr(start, length)
```
var str = "0123456789";
var res = str.substr(2, 3);
console.log(res); // 234
```
start可以是负数，表示从后往前数的位置, length不能为负数.
如果省略第二个参数(length), 则表示从开始位置一直到字符串的结尾
```
var str = "0123456789";
var res = str.substr(2);
console.log(res); // 23456789
```

##### replace(currentString, targetString)字符串替换
```
var str = "Microsoft Please visit Microsoft!";
console.log(str.replace("Microsoft", "W3Schools")); //W3Schools Please visit Microsoft!
```

默认情况下，replace函数只替换第一个匹配的字符串，如果想要替换所有匹配的字符串可以使用带/g的正则表达式
```
var str = "Microsoft Please visit Microsoft!";
console.log(str.replace(/Microsoft/g, "W3Schools")); //W3Schools Please visit W3Schools!
```
默认情况下，replace函数是大小写敏感，如果想要大小写不敏感可以使用带/i的正则表达式
```
var str = "Please visit MicroSOFT!";
console.log(str.replace(/Microsoft/i, "W3Schools")); //Please visit W3Schools!
```

##### toUpperCase() 转换成大写
```
var name = 'JavaScript';
console.log(name.toUpperCase()); //JAVASCRIPT
```

##### toLowerCase() 转换成小写
```
var name = 'JavaScript';
console.log(name.toLowerCase()); //javascript
```

##### concat(x, ...) 连接字符串
```
var text1 = "Hello";
var text2 = "World";
console.log(text1.concat(text2)); //HelloWorld
console.log(text1.concat(" ", text2)); //Hello World
console.log(text1.concat(" ", text2, 12, '*****', false)); //Hello World12*****false

// 可以使用加号替换
console.log(text1 + text2); //HelloWorld
console.log(text1 + ' ' + text2); //Hello World
console.log(text1 + ' ' + text2 + 12 + '*****' + false); //Hello World********
```

##### charAt(position) 返回指定位置的字符，未找到则返回空字符串
```
var str = "HELLO WORLD";
console.log(str.charAt(0)); // H
console.log(str.charAt(2)); // L

var char = str.charAt(50);
//如果位置不合法则返回空字符串 
console.log(char.length + ' ' + (typeof char) + ' ' + (char == '')); //0 string true

```

##### charCodeAt(position) 返回指定位置字符对应的unicode的数值，未找到则返回NaN
```
var str = "HELLO WORLD";
console.log(str.charCodeAt(0)); // 72
console.log(str.charCodeAt(2)); // 76

var char = str.charCodeAt(50);
//如果位置不合法则返回空字符串 
console.log(char  + ' ' + (typeof char) + ' ' + isNaN(NaN)); //NaN number true

```

##### split(separator) 字符串转成数组
```
var txt = "a,b,c,d,e";   // String
var array1 = txt.split(","); 
var array2 = txt.split(" ");
var array3 = txt.split("|");
var array4 = txt.split();

console.log(array1); // ['a', 'b', 'c', 'd', 'e'] 包含5个元素的数组
console.log(array2); // ['a,b,c,d,e']  仅包含一个元素的数组
console.log(array3); // ['a,b,c,d,e']  仅包含一个元素的数组
console.log(array4); // ['a,b,c,d,e']  仅包含一个元素的数组

```

### 16. Array(数组)
#### Array Object
The Array object is used to store multiple values in a single variable:
```
语法
var array_name = [item1, item2, ...]; //推荐这种
var array_name = new Array(item1, item2, ...); //避免使用

```

访问数组内元素：数组是通过下标来访问数组内元素的，数组下标是从0开始的，第一个元素的的下标是0，第二个元素的下标是1，以此类推.
```
var cars2 = new Array("Saab", "Volvo", "BMW");
var cars = ["Saab", "Volvo", "BMW"];
var emptyArray = [];
console.log(cars[0]);
```

#### 数组都是对象
数组是特殊类型的对象, 执行typeof会返回object,  数组是使用数字下标，对象使用名字下标
```
//Array
var person = ['John', 'Doe', 46];
var firstName = person[0];

//Object
var person = {firstName:'John', lastName:'Doe', age:46}
var firstName = person['firstName'];
var firstName = person.firstName;
```

数组的元素可以是数值类型、布尔类型、字符串类型、对象类型(对象、函数、数组、日期等对象), 数组内的元素之间可以是不同的数据类型.
```
var array = ['Jiandong', 20, false, {age:'20'}, new Date()]; //["Jiandong", 20, false, {…}, Tue Sep 12 2017 20:09:09 GMT+0800 (CST)]

function sum(num1, num2) {
    return num1 + num2;
}

var array2 = [];
array2[0] = true;//元素是布尔类型
array2[1] = 12;//元素是数值类型
array2[2] = 'JS';//元素是字符串类型
array2[3] = sum;//元素是函数
array2[4] = {name:'JS', sex:'male'};//元素是对象
array2[5] = new Date();//元素是日期
array2[6] = [1, 2, 3];//元素是数组
console.log(array);//["Jiandong", 20, false, {…}, Tue Sep 12 2017 21:52:05 GMT+0800 (CST)]
console.log(array2);//[true, 12, "JS", ƒ, {…}, Tue Sep 12 2017 21:52:05 GMT+0800 (CST), Array(3)]

```

#### 数组的length属性, 返回数组的长度
```
var fruits = ["Banana", "Orange", "Apple", "Mango"];
console.log(fruits.length);// the length of fruits is 4
```

#### 使用for循环遍历数组
```
var fruits = ['Banana', 'Orange', 'Apple', 'Mango'];
var length = fruits.length;
var text = '';
var i;
for (i = 0; i < length; i++) {
    text += ' ' + fruits[i];
}
console.log(text);//Banana Orange Apple Mango

```

#### 添加数组元素到数组末尾push(x)或使用下标
```

// 使用push(x)方法添加给数组末尾添加元素
var fruits = ["Banana", "Orange", "Apple", "Mango"];
fruits.push("Lemon"); // adds a new element (Lemon) to fruits
console.log(fruits);//["Banana", "Orange", "Apple", "Mango", "Lemon"]

// 使用下标添加数组元素
var fruits = ["Banana", "Orange", "Apple", "Mango"];
fruits[4] = "Lemon"; // adds a new element (Lemon) to fruits
console.log(fruits);//["Banana", "Orange", "Apple", "Mango", "Lemon"]

// 请注意用较大的下标给数组添加元素会导致创建占位的undefined元素
fruits[7] = "Pear";
console.log(fruits[5]); //undefined
console.log(fruits[6]); //undefined
console.log(fruits[7]); //Pear

// If you use named indexes, JavaScript will redefine the array to a standard object.
// After that, some array methods and properties will produce incorrect results.
var person = [];
person["firstName"] = "John";
person["lastName"] = "Doe";
person["age"] = 46;
var x = person.length;         // person.length will return 0
var y = person[0];             // person[0] will return undefined

```

#### 添加数组元素到数组头部unshift(x)
```
var fruits = ["Banana", "Orange", "Apple", "Mango"];
fruits.unshift("Lemon"); //添加数组元素到数组头部
console.log(fruits); //["Lemon", "Banana", "Orange", "Apple", "Mango"]
```

#### 移除数组末尾元素pop()
```
var fruits = ["Banana", "Orange", "Apple", "Mango"];
console.log(fruits.toString()); //Banana,Orange,Apple,Mango
fruits.pop();
console.log(fruits.toString()); //Banana,Orange,Apple

var array = [];
array.pop();//对空数组执行pop是无害的
console.log(array.toString());
```

#### 移除数组的第一个元素shift()
```
var fruits = ["Banana", "Orange", "Apple", "Mango"];
console.log(fruits.toString()); //Banana,Orange,Apple,Mango
fruits.shift();
console.log(fruits.toString()); //Orange,Apple,Mango

var array = [];
array.shift();//对空数组执行shift是无害的
console.log(array.toString());
```

#### 使用数组下标改变数组元素或添加数组元素
```
var fruits = ["Banana", "Orange", "Apple", "Mango"];
fruits[0] = 'BananaChanged'; //改变下标为0的元素
fruits[fruits.length] = 'EndElement';//使用length可以方便在数组末尾添加元素
console.log(fruits.toString()); //BananaChanged,Orange,Apple,Mango,EndElement
```

#### 使用delete操作符删除数组元素:元素值变成undefined,扔占位(不推荐)
```
var fruits = ["Banana", "Orange", "Apple", "Mango"];
delete fruits[0]; // Changes the first element in fruits to undefined
console.log(fruits.toString()); //

```

#### splice()添加或删除数组元素

使用splice()函数添加数组元素
```
var fruits = ["Banana", "Orange", "Apple", "Mango"];
fruits.splice(2, 0, "Lemon", "Kiwi");
console.log(fruits.toString()); //Banana,Orange,Lemon,Kiwi,Apple,Mango
```

> The first parameter (2) defines the position where new elements should be added (spliced in).
> The second parameter (0) defines how many elements should be removed.
> The rest of the parameters ("Lemon" , "Kiwi") define the new elements to be added.

使用splice()函数删除数组元素
```
var fruits = ["Banana", "Orange", "Apple", "Mango"];
fruits.splice(1, 1); // Removes the second element of fruits
console.log(fruits.toString()); //Banana,Apple,Mango

```

> The first parameter (0) defines the position where new elements should be added (spliced in).
> The second parameter (1) defines how many elements should be removed.
> The rest of the parameters are omitted. No new elements will be added.

#### concat(array1, array2, ...)合并数组然后返回合并后的新数组
```
var myGirls = ["Cecilie", "Lone"];
var myBoys = ["Emil", "Tobias","Linus"];
var myGirls2 = myGirls.concat();//复制数组
var myChildren = myGirls.concat(myBoys); // 两个数组进行合并
console.log(myChildren.toString()); // Cecilie,Lone,Emil,Tobias,Linus

var arr1 = ["Cecilie", "Lone"];
var arr2 = ["Emil", "Tobias","Linus"];
var arr3 = ["Robin", "Morgan"];
var myChildren2 = arr1.concat(arr2, arr3); // 三个数组进行合并
console.log(myChildren2.toString()); // Cecilie,Lone,Emil,Tobias,Linus,Robin,Morgan

```

#### slice(startIndex, endIndex)从数组中截取指定元素生成新的数组且不改变原数组， 其中包含startIndex, 不包含endIndex
```
var fruits = ["Banana", "Orange", "Lemon", "Apple", "Mango"];
var citrus = fruits.slice(1); //省略第二个参数代表一直截取到数组的末尾
console.log(citrus.toString());//Orange,Lemon,Apple,Mango

var citrus2 = fruits.slice(3); //省略第二个参数代表一直截取到数组的末尾
console.log(citrus2.toString());//Apple,Mango

var citrus3 = fruits.slice(1, 3); //包含1，但不包含3
console.log(citrus3.toString());//Orange,Lemon

```

#### sort()/sort(compareFunction)按照字母顺序(alphabetically)进行排序或使用比较函数进行排序
```
var fruits = ["Banana", "Orange", "Apple", "Mango", 'banana', 'apple'];
fruits.sort(); 
console.log(fruits.toString()); // Apple,Banana,Mango,Orange,apple,banana

```

在上面的例子中，元素都是字母时排序是对的，但如果元素是数字字符串，'20'和'100'，按照sort排序，'20'>'100', 因为2比1大，这时可以在sort函数中传入比较函数来解决
```
var fruits = ["300", "20", "100"];
fruits.sort(); 
console.log(fruits.toString()); // 100,20,300 排序结果不是所期望的

fruits.sort(function (a, b) { return a - b; });// 升序
console.log(fruits.toString()); // 20,100,300

fruits.sort(function (a, b) { return b - a; });// 降序
console.log(fruits.toString()); // 300,100,20

```

- 数组随机排序
```
var points = [40, 100, 1, 5, 25, 10];
points.sort(function(a, b){return 0.5 - Math.random()});
console.log(points.toString()); 

```

- reverse()数组逆序
```
var fruits = ["Banana", "Orange", "Apple", "Mango"];
fruits.sort();
console.log(fruits.toString());// Apple,Banana,Mango,Orange

fruits.reverse();
console.log(fruits.toString()); // Orange,Mango,Banana,Apple

```

- 查找数组内的最大值和最小值

JavaScript没有提供查找数组内最大值最小值的函数，但可以通过以下方法：
**方法一：**通过对数组进行升序或降序后得到最大值和最小值。但是如果只是为了得到最大值或最小值就对数组进行升序或降序排序是低效的（inefficient)
```
var points = [40, 100, 1, 5, 25, 10];
points.sort(function(a, b){return a - b});
var min = points[0];
var max = points[points.length-1];
console.log(min); // 1
console.log(max); // 100

```

**方法二：**使用Math.max()和Math.min()
```
function myArrayMax(arr) {
    return Math.max.apply(null, arr);
}

function myArrayMin(arr) {
    return Math.min.apply(null, arr);
}

var arr = [100, 30, 90, 5, 300];
var min = myArrayMin(arr);
var max = myArrayMax(arr);

console.log(min); // 5
console.log(max); // 300

```

**方法三：**使用循环遍历数组来查找最大值最小值
```
function myArrayMax(arr) {

    var length = arr.length;
    var max = -Infinity;

    while (length--) {
        if (arr[length] > max) {
            max = arr[length];
        }
    }

    return max;
}

function myArrayMin(arr) {

    var length = arr.length;
    var min = Infinity;

    while (length--) {
        if (arr[length] < min) {
            min = arr[length];
        }
    }

    return min;
}

var arr = [100, 30, 90, 5, 300];
var min = myArrayMin(arr);
var max = myArrayMax(arr);

console.log(min); // 5
console.log(max); // 300
```

- 对象数组进行排序
```
var cars = [{type:"Volvo", year:2016},  {type:"Saab", year:2001}, {type:"BMW", year:2010}];
cars.sort(function(a, b){return a.year - b.year});//使用年份属性进行排序
console.log(cars[0].year + ' ' + cars[1].year + ' ' + cars[2].year); //2001 2010 2016

cars.sort(function(a, b){
    var aType = a.type.toLowerCase();
    var bType = b.type.toLowerCase();
    if (aType < bType) {return -1;}
    if (aType > bType) {return 1;}
    return 0;
}); //使用type属性进行排序
console.log(cars[0].type + ' ' + cars[1].type + ' ' + cars[2].type); //BMW Saab Volvo

```

- 数组的复制：(深复制，浅复制)

**浅复制**: 只是复制了内存地址，修改复制对象时原对象也修改
```
// 数组对象内存地址复制
var array = ['a', 'b', 'c'];
var array2 = array;
array2[1] = 'BB'; //改变array2时，array也改变了
console.log(array.toString());  //a,BB,c
console.log(array2.toString()); //a,BB,c

// contcat()或arr1.slice(0)
// 情况1：数组元素是非对象类型时，复制对象不影响原对象的元素
var arr1 = [1, 2, 3, 4],
arr2 = arr1.slice(0),
arr3 = arr1.concat();
console.log(arr1, arr2, arr3);//[1, 2, 3, 4] [1, 2, 3, 4] [1, 2, 3, 4],
arr2[2] = 10;
arr3[2] = 11;
console.log(arr1, arr2, arr3); //[1, 2, 3, 4] [1, 2, 10, 4] [1, 2, 11, 4],

// 情况2：数组元素是对象类型时，复制对象会影响原对象的对象型元素
var fun = function() {},
arr1 = [1, 2, [3, 4], {a: 5, b: 6}, fun],
arr2 = arr1.slice(0),
arr3 = arr1.concat();

arr1[0] = 10;
arr2[3].a = 100;
arr3[2][1] = 5;

console.log(arr1, arr2, arr3);//出了arr1[0] = 10;对简单值的修改，其他对对象型元素的修改对三个对象都生效了

```

**深复制**
1、对原型进行扩展
```
Object.prototype.clone = function() {
    var obj = {};

    for(var i in this) {
        obj[i] = this[i];
    }

    return obj;
}

Array.prototype.clone = function() {
    var len = this.length;
    var arr = [];

    for(var i = 0;i < len;i++) {
        if(typeof this[i] !== 'object') {
            arr.push(this[i]);
        } else {
            arr.push(this[i].clone());
        }
    }

    return arr;
}

//测试Object
var obj1 = {
    name: 'Rattz',
    age: 20,
    hello: function () {
        return "I'm " + name;
    }
};
var obj2 = obj1.clone();
obj2.age++;
console.log(obj1.age);//20
console.log(obj2.age);//21

//测试Array
var fun = function() {};
var fun2 = function(a, b) {return a+b};
arr1 = [1, 2, [3, 4], {a: 5, b: 6}, fun],
arr2 = arr1.clone();
arr2[0] = 1000;
(arr2[2])[1] = 3333;
(arr2[3]).a = 5555;
arr2[4] = fun2;
console.log(arr1);
console.log(arr2);

```

2、使用JSON方法
```
var arr1 = [1, 2, [3, 4], {a: 5, b: 6}, 7];
var arr2 = JSON.parse(JSON.stringify(arr1));

console.log(arr1, arr2);//[1, 2, [3, 4], {a: 5, b: 6}, 7] [1, 2, [3, 4], {a: 5, b: 6}, 7],
arr2[1] = 10;
arr2[3].a = 20;
console.log(arr1[1], arr2[1]);//2 10
console.log(arr1[3], arr2[3]);//{a: 5, b: 6} {a:20,b:6}
```


#### toString()将数组转换成字符串，数组元素之间用逗号分隔
```
var fruits = ["Banana", "Orange", "Apple", "Mango"];
console.log(fruits.toString()); //Banana,Orange,Apple,Mango
```

#### join(separator)将数组转换成字符串，数组元素之间使用separator分隔
```
var fruits = ["Banana", "Orange", "Apple", "Mango"];
console.log(fruits.join('####')); //Banana####Orange####Apple####Mango
```

#### 如何判断是否是数组
方法1：使用ECMAScript5提供的Array.isArray(x)方法
```
var array = [];
var isArray = Array.isArray(array);
console.log(isArray);
```

方法2：使用自己创建的isArray(x)函数
```
function isArray(x) {
    return x.constructor.toString().indexOf("Array") > -1;
}
```

方法3：使用instanceof操作符
```
var array = [];
var isArray = array instanceof Array;
console.log(isArray);
```

#### 数组的属性列表
| Property | Description |
| :------- | :---------- |
| constructor | Returns the function that created the Array object's prototype |
| (\_\_proto\_\_)prototype | Allows you to add properties and methods to an Array object |
|length | Sets or returns the number of elements in an array |

```
var array = ['Jiandong', 20, false, {age:'20'}];

console.log(array.constructor); //ƒ Array() { [native code] }
console.log(array.__proto__); //[constructor: ƒ, concat: ƒ, pop: ƒ, push: ƒ, shift: ƒ, …]
console.log(array.length); //4
console.log(array[0]); // Jiandong
console.log(array[1]); // 20 
console.log(array[2]); // false
console.log(array[3]); // {age: "20"}
```

#### 数组的方法列表
| Method | Description |
| :------- | :---------- |
| concat() | Joins two or more arrays, and returns a copy of the joined arrays |
| copyWithin() | Copies array elements within the array, to and from specified positions |
| every() | Checks if every element in an array pass a test |
| fill() | Fill the elements in an array with a static value |
| filter() | Creates a new array with every element in an array that pass a test |
| find() | Returns the value of the first element in an array that pass a test |
| findIndex() | Returns the index of the first element in an array that pass a test |
| forEach() | Calls a function for each array element |
| indexOf() | Search the array for an element and returns its position |
| isArray() | Checks whether an object is an array |
| join() | Joins all elements of an array into a string |
| lastIndexOf() | Search the array for an element, starting at the end, and returns its position |
| map() | Creates a new array with the result of calling a function for each array element |
| pop() | Removes the last element of an array, and returns that element |
| push() | Adds new elements to the end of an array, and returns the new length |
| reduce() | Reduce the values of an array to a single value (going left-to-right) |
| reduceRight() | Reduce the values of an array to a single value (going right-to-left) |
| reverse() | Reverses the order of the elements in an array |
| shift() | Removes the first element of an array, and returns that element |
| slice() | Selects a part of an array, and returns the new array |
| some() | Checks if any of the elements in an array pass a test |
| sort() | Sorts the elements of an array |
| splice() | Adds/Removes elements from an array |
| toString() | Converts an array to a string, and returns the result |
| unshift() | Adds new elements to the beginning of an array, and returns the new length |
| valueOf() | Returns the primitive value of an array |


### 17. Date日期类型
The Date object lets you work with dates (years, months, days, hours, minutes, seconds, and milliseconds)
#### JavaScript的日期格式
字符串：Wed Sep 13 2017 15:10:37 GMT+0800 (CST)
距离1970年1月1日00:00:00的毫秒数: 1505286637514

创建日期对象
```
语法:
new Date()
new Date(milliseconds)
new Date(dateString)
new Date(year, month, day, hours, minutes, seconds, milliseconds)
//请注意这里的month是0~11，0就是1月份，11就是12月份
```

示例
```
var currentDate = new Date();
var dateFromString = new Date('October 13, 2014 11:13:00');
var dateFromMilliseconds = new Date(86400000);
var date = new Date(2014, 10, 10, 13, 30, 21, 5); //请注意这里的month是0~11，0就是1月份，11就是12月份

console.log(currentDate); // Wed Sep 13 2017 15:17:28 GMT+0800 (CST)
console.log(dateFromString); // Mon Oct 13 2014 11:13:00 GMT+0800 (CST)
console.log(dateFromMilliseconds); //Fri Jan 02 1970 08:00:00 GMT+0800 (CST)
console.log(date); //Mon Nov 10 2014 13:30:21 GMT+0800 (CST)
```

#### toString()/toUTCString()
```
var currentDate = new Date();

console.log(currentDate.toString()); //Wed Sep 13 2017 15:24:53 GMT+0800 (CST)
console.log(currentDate.toUTCString()); //Wed, 13 Sep 2017 07:24:53 GMT

```

#### 时区(Time Zones)
When setting a date, without specifying the time zone, JavaScript will use the browser's time zone.

When getting a date, without specifying the time zone, the result is converted to the browser's time zone.

In other words: If a date/time is created in GMT (Greenwich Mean Time), the date/time will be converted to CDT (Central US Daylight Time) if a user browses from central US.


#### 日期输出格式
日期输出格式与日期的输入格式无关，JavaScript默认输出日期的是输出全格式的文本
```
var currentDate = new Date();
console.log(currentDate); //Wed Sep 13 2017 15:31:50 GMT+0800 (CST)

```

#### 日期输入格式(4种)
| Type | Example |
| :--- | :-------|
| ISO Date | "2015-03-25" (The International Standard) |
| Short Date | "03/25/2015" |
| Long Date | "Mar 25 2015" or "25 Mar 2015" |
| Full Date | "Wednesday March 25 2015" |

##### ISO Dates:
1. YYYY-MM-DD
```
var date = new Date("2015-03-25");
console.log(date); //Wed Mar 25 2015 08:00:00 GMT+0800 (CST)
```

2. YYYY-MM
```
var date = new Date("2015-03");
console.log(date); //Sun Mar 01 2015 08:00:00 GMT+0800 (CST)
```

3. YYYY
```
var date = new Date("2015");
Thu Jan 01 2015 08:00:00 GMT+0800 (CST)
```

4. Date-Time: YYYY-MM-DDTHH:MM:SSZ
Date and time is separated with a capital T.
UTC time is defined with a capital letter Z.
If you want to modify the time relative to UTC, remove the Z and add +HH:MM or -HH:MM instead:
Omitting T or Z in a date-time string can give different result in different browser.
```
var date = new Date("2015-03-25T12:00:00Z");
console.log(date.toUTCString()); //Wed, 25 Mar 2015 12:00:00 GMT


var date2 = new Date("2015-03-25T12:00:00-06:30");
console.log(date2.toUTCString()); //Wed, 25 Mar 2015 18:30:00 GMT
```

##### Short Dates:MM/DD/YYYY
```
var d = new Date("03/25/2015");
console.log(d);//Wed Mar 25 2015 00:00:00 GMT+0800 (CST)
```

##### Long Dates: MMM DD YYYY
```
var d1 = new Date("Mar 25 2015");
var d2 = new Date("25 Mar 2015"); //月份跟日期可以互换位置
var d3 = new Date("January 25 2015"); //月份可以不简写
var d4 = new Date("Jan 25 2015");
console.log(d1);//Wed Mar 25 2015 00:00:00 GMT+0800 (CST)
console.log(d2);//Wed Mar 25 2015 00:00:00 GMT+0800 (CST)
console.log(d3);//Sun Jan 25 2015 00:00:00 GMT+0800 (CST)
console.log(d4);//Sun Jan 25 2015 00:00:00 GMT+0800 (CST)
```

##### Full Date: full JavaScript format
```
var d = new Date("Wed Mar 25 2015 09:56:24 GMT+0100 (W. Europe Standard Time)");
console.log(d.toUTCString());//Wed Mar 25 2015 16:56:24 GMT+0800 (CST)
```


#### Date Get Methods
Get methods are used for getting a part of a date. Here are the most common :
| Method | Description |
| :------- | :---------- |
| getFullYear() | Get the four digit year (yyyy) |
| getMonth() | Get the month (0-11) |
| getDate() | Get the day as a number (1-31) |
| getDay() | Get the weekday as a number (0-6) |
| getHours() | Get the hour (0-23) |
| getMinutes() | Get the minutes (0-59) |
| getSeconds() | Get the seconds (0-59) | 
| getMilliseconds() | Get the milliseconds (0-999) |
| getTime() | Get the time (milliseconds since January 1, 1970) |

> getDay()返回 0-6, 请注意：在JavaScript中0代表星期日,就从星期日开始

```
var date = new Date(2014, 11, 25, 12, 32, 20, 888);
console.log(date.getFullYear()); // 2014
console.log(date.getMonth()); // 11
console.log(date.getDate()); // 25
console.log(date.getDay()); // 4
console.log(date.getHours()); // 12
console.log(date.getMinutes()); // 32
console.log(date.getSeconds()); // 20
console.log(date.getMilliseconds()); // 888
console.log(date.getTime()); // 1419481940888
```

#### Date Set Methods
Set methods are used for setting a part of a date. Here are the most common :
| Method | Description |
| :------- | :---------- |
| setFullYear(year, month, date) | Set the year (optionally month and day) |
| setMonth() | Set the month (0-11) |
| setDate() | Set the day as a number (1-31) |
| setHours() | Set the hour (0-23) |
| setMinutes() | Set the minutes (0-59) |
| setSeconds() | Set the seconds (0-59) | 
| setMilliseconds() | set the milliseconds (0-999) |
| setTime() | Set the time (milliseconds since January 1, 1970) |

```
var date = new Date();
date.setFullYear(2014);
//date.setFullYear(2014,11, 25);
date.setMonth(11);
date.setDate(25);
date.setHours(12);
date.setMinutes(32);
date.setSeconds(20);
date.setMilliseconds(888);
date.setTime(date.getTime());
console.log(date.getFullYear()); // 2014
console.log(date.getMonth()); // 11
console.log(date.getDate()); // 25
console.log(date.getDay()); // 4
console.log(date.getHours()); // 12
console.log(date.getMinutes()); // 32
console.log(date.getSeconds()); // 20
console.log(date.getMilliseconds()); // 888
console.log(date.getTime()); // 1419481940888

```

#### Add days
```
var d = new Date();
d.setDate(20);
console.log(d); //Wed Sep 20 2017 16:27:56 GMT+0800 (CST)
d.setDate(d.getDate() + 30); //Fri Oct 20 2017 16:27:56 GMT+0800 (CST)
console.log(d);

```

> If adding days, shifts the month or year, the changes are handled automatically by the Date object.

#### 日期字符串转成日期对象

Parsing Dates: Date.parse(validDateStr)

Date.parse(validDateStr)将一个合法的日期字符串转换成距离1970的毫秒数
```
var milliseconds = Date.parse('2017-07-22');
console.log(milliseconds); // 1500681600000

var date = new Date(milliseconds);
console.log(date.getFullYear() + '-' + (date.getMonth()+1) + '-' + date.getDate()); // 2017-7-22

```

#### 日期对象转成日期字符串
```

function convertDateToString(dateObj, formatStr) {

    var dateStr = '';
    if (typeof(dateObj) == 'object' && dateObj instanceof Date) {

        if (typeof(formatStr) == 'string') {

            if (formatStr.toUpperCase() == 'YYYY') {
                dateStr = String(dateObj.getFullYear());

            } else if (formatStr.toUpperCase() == 'YYYY-MM') {
                dateStr = dateObj.getFullYear() + '-' + (dateObj.getMonth() + 1);

            } else if (formatStr.toUpperCase() == 'YYYY-MM-DD') {
                dateStr = dateObj.getFullYear() + '-' + (dateObj.getMonth() + 1) + '-' + dateObj.getDate();
                
            } else if (formatStr.toUpperCase() == 'YYYY-MM-DD HH:MM') {
                dateStr = dateObj.getFullYear() + '-' + (dateObj.getMonth() + 1) + '-' + dateObj.getDate() + ' ' + dateObj.getHours() + ':' + dateObj.getMinutes();
                
            } else if (formatStr.toUpperCase() == 'YYYY-MM-DD HH:MM:SS') {
                dateStr = dateObj.getFullYear() + '-' + (dateObj.getMonth() + 1) + '-' + dateObj.getDate() + ' ' + dateObj.getHours() + ':' + dateObj.getMinutes() + ':' + dateObj.getSeconds();
                
            }
        }
    }

    return dateStr;
}

var dateObj = new Date(2017, 9, 11, 14, 33, 25, 777);
console.log(convertDateToString(dateObj, 'YYYY'));                 //2017
console.log(convertDateToString(dateObj, 'YYYY-MM'));              //2017-10
console.log(convertDateToString(dateObj, 'YYYY-MM-DD'));           //2017-10-11
console.log(convertDateToString(dateObj, 'YYYY-MM-DD HH:MM'));     //2017-10-11 14:33
console.log(convertDateToString(dateObj, 'YYYY-MM-DD HH:MM:SS'));  //2017-10-11 14:33:25

```

#### Date日期比较
```
var today, someday, text;
today = new Date();
someday = new Date();
someday.setFullYear(2100, 0, 14);

if (someday > today) {
    text = "Today is before January 14, 2100.";
} else {
    text = "Today is after January 14, 2100.";
}
console.log(text); //Today is before January 14, 2100.

```

#### Date对象的属性列表
| Property | Description |
| :------- | :---------- |
| constructor | Returns the function that created the Date object's prototype |
| prototype/\_\_proto\_\_ | Allows you to add properties and methods to an object |
详见:https://www.w3schools.com/jsref/jsref_obj_date.asp

#### Date对象的方法列表
| Method | Description |
| :------- | :---------- |
| abs(x) | Returns the absolute value of x |
| getDate() | Returns the day of the month (from 1-31) |
| getDay() | Returns the day of the week (from 0-6) |
| getFullYear() | Returns the year |
| getHours() | Returns the hour (from 0-23) |
| getMilliseconds() | Returns the milliseconds (from 0-999) |
| getMinutes() | Returns the minutes (from 0-59) |
| getMonth() | Returns the month (from 0-11) |
| getSeconds() | Returns the seconds (from 0-59) |
| getTime() | Returns the number of milliseconds since midnight Jan 1 1970, and a specified date |
| getTimezoneOffset() | Returns the time difference between UTC time and local time, in minutes |
| getUTCDate() | Returns the day of the month, according to universal time (from 1-31) |
| getUTCDay() | Returns the day of the week, according to universal time (from 0-6) |
| getUTCFullYear() | Returns the year, according to universal time |
| getUTCHours() | Returns the hour, according to universal time (from 0-23) |
| getUTCMilliseconds() | Returns the milliseconds, according to universal time (from 0-999) |
| getUTCMinutes() | Returns the minutes, according to universal time (from 0-59) |
| getUTCMonth() | Returns the month, according to universal time (from 0-11) |
| getUTCSeconds() | Returns the seconds, according to universal time (from 0-59) |
| getYear() | Deprecated. Use the getFullYear() method instead |
| now() | Returns the number of milliseconds since midnight Jan 1, 1970 |
| parse() | Parses a date string and returns the number of milliseconds since January 1, 1970 |
| setDate() | Sets the day of the month of a date object |
| setFullYear() | Sets the year of a date object |
| setHours() | Sets the hour of a date object |
| setMilliseconds() | Sets the milliseconds of a date object |
| setMinutes() | Set the minutes of a date object |
| setMonth() | Sets the month of a date object|
| setSeconds() | Sets the seconds of a date object |
| setTime() | Sets a date to a specified number of milliseconds after/before January 1, 1970 |
| setUTCDate()| Sets the day of the month of a date object, according to universal time |
| setUTCFullYear() | Sets the year of a date object, according to universal time |
| setUTCHours()| Sets the hour of a date object, according to universal time |
| setUTCMilliseconds() | Sets the milliseconds of a date object, according to universal time |
| setUTCMinutes() | Set the minutes of a date object, according to universal time |
| setUTCMonth() | Sets the month of a date object, according to universal time |
| setUTCSeconds() | Set the seconds of a date object, according to universal time |
| setYear() | Deprecated. Use the setFullYear() method instead |
| toDateString() | Converts the date portion of a Date object into a readable string |
| toGMTString() | Deprecated. Use the toUTCString() method instead |
| toISOString() | Returns the date as a string, using the ISO standard |
| toJSON() | Returns the date as a string, formatted as a JSON date |
| toLocaleDateString() | Returns the date portion of a Date object as a string, using locale conventions |
| toLocaleTimeString() | Returns the time portion of a Date object as a string, using locale conventions |
| toLocaleString() | Converts a Date object to a string, using locale conventions |
| toString() | Converts a Date object to a string |
| toTimeString() | Converts the time portion of a Date object to a string |
| toUTCString() | Converts a Date object to a string, according to universal time | 
| UTC() | Returns the number of milliseconds in a date since midnight of January 1, 1970, according to UTC time |
| valueOf() | Returns the primitive value of a Date object |
详见:https://www.w3schools.com/jsref/jsref_obj_date.asp

### 18. Math(数学对象)
#### Math是JavaScript的全局对象, 提供数学相关的属性和方法

```
console.log(Math); //Math {abs: ƒ, acos: ƒ, acosh: ƒ, asin: ƒ, asinh: ƒ, …}
console.log(typeof Math); //object
console.log(Math.constructor); //ƒ Object() { [native code] }
console.log(Math.__proto__); //{constructor: ƒ, __defineGetter__: ƒ, __defineSetter__: ƒ, hasOwnProperty: ƒ, __lookupGetter__: ƒ, …}
```

#### Math对象的属性列表
| Property | Description |
| :------- | :---------- |
| E | Returns Euler's number (approx. 2.718) |
| LN2 | Returns the natural logarithm of 2 (approx. 0.693) |
| LN10 | Returns the natural logarithm of 10 (approx. 2.302) |
| LOG2E | Returns the base-2 logarithm of E (approx. 1.442) |
| LOG10E | Returns the base-10 logarithm of E (approx. 0.434) |
| PI | Returns PI (approx. 3.14) |
| SQRT1_2 | Returns the square root of 1/2 (approx. 0.707) |
| SQRT2 | Returns the square root of 2 (approx. 1.414) |

#### Math对象的方法列表
| Method | Description |
| :------- | :---------- |
| abs(x) | Returns the absolute value of x |
| acos(x) | Returns the arccosine of x, in radians |
| asin(x) | Returns the arcsine of x, in radians |
| atan2(y, x) | Returns the arctangent of the quotient of its arguments |
| ceil(x) | Returns x, rounded upwards to the nearest integer |
| cos(x) | Returns the cosine of x (x is in radians) |
| exp(x) | Returns the value of Ex |
| floor(x) | Returns x, rounded downwards to the nearest integer |
| log(x) | Returns the natural logarithm (base E) of x |
| max(x, y, z, ..., n)  | Returns the number with the highest value |
| min(x, y, z, ..., n) | Returns the number with the lowest value |
| pow(x, y) | Returns the value of x to the power of y |
| random() | Returns a random number between 0 and 1 |
| round(x) | Rounds x to the nearest integer |
| sin(x) | Returns the sine of x (x is in radians) |
| sqrt(x) | Returns the square root of x |
| tan(x) | Returns the tangent of an angle |

##### Math.PI
```
console.log(Math.PI); //3.141592653589793
```

##### Math.abs(x) 求绝对值
```
console.log(Math.abs(-4.7)); //4.7
console.log(Math.abs(0)); //0
```

##### Math.round(x) 四舍五入
```
console.log(Math.round(4.7)); //5
console.log(Math.round(4.5)); //5
console.log(Math.round(4.499999)); //4
```

##### Math.ceil(x) 向上取整
```
console.log(Math.ceil(4.1));//5
console.log(Math.ceil(4.8));//5
console.log(Math.ceil(0));//0
console.log(Math.ceil(-4.3));//-4
```

##### Math.floor(x) 向下取整
```
console.log(Math.floor(4.1));//4
console.log(Math.floor(4.8));//4
console.log(Math.floor(0));//0
console.log(Math.floor(-4.3));//-5
```

##### Math.pow(x, y) 求幂: x的y次方
```
console.log(Math.pow(8, 2)); //64
console.log(Math.pow(8, 3)); //512
```

##### Math.sqrt(x) 开平方
```
console.log(Math.sqrt(64)); //8

```

##### Math.max(x, y, z, ..., n) 求最大值
```
console.log(Math.max(0, 150, 30, 20, -8, -200));  //150
```

##### Math.min(x, y, z, ..., n) 求最小值
```
console.log(Math.min(0, 150, 30, 20, -8, -200));  //-200
```

##### Math.random() 生成0(包含)到1(不包含)之间的随机数
```
console.log(Math.random());  //随机生成0.2948454498504711

```

### 19. Random(随机数)
#### Math.random()随机数函数
Math.random()函数返回0(包含)到1(不包含)之间的随机数, 所以Math.random()返回随机数总是小于1
```
console.log(Math.random()); //随机生成的 0.9575246787376859

```

#### 随机整数
通过Math.random()和Math.floor()来返回随机整数
```
// 0到10，但不包含10
console.log(Math.floor(Math.random() * 10)) //随机生成的 9

// 0到11，但不包含11
console.log(Math.floor(Math.random() * 11)) //随机生成的 10

// 0到100，但不包含100
console.log(Math.floor(Math.random() * 100)) //随机生成的 99

// 0到101，但不包含101
console.log(Math.floor(Math.random() * 101)) //随机生成的 100

// 1到100，但不包含100
console.log(Math.floor(Math.random() * 100) + 1)  // 1

```

> This JavaScript function always returns a random number between min (included) and max (excluded):
```
function getRandomInteger(minIncluded, maxExcluded) {
    return Math.floor(Math.random() * (maxExcluded - minIncluded) ) + minIncluded;
}
```
> This JavaScript function always returns a random number between min and max (both included):
```
function getRandomInteger(minIncluded, maxIncluded {
    return Math.floor(Math.random() * (maxIncluded - minIncluded + 1) ) + minIncluded;
}
```

### 20. RegExp(Regular Expressions正则表达式)

正则表达式是由字符序列构成的搜索模式(search pattern), 可以用来执行文本搜索和文本替换
#### 正则表达式语法
```
语法
/pattern/modifiers;

pattern匹配模式
modifiers匹配修饰符

示例:
var patt = /w3schools/i;
var regexp = new RegExp(/w3schools/i);

/w3schools/i  是一个正则表达式.
w3schools  是匹配模式
i  是修饰符，代表大小写不敏感
```

#### 正则表达式在字符串的方法中使用: search() and replace()
The search() method uses an expression to search for a match, and returns the position of the match.
The replace() method returns a modified string where the pattern is replaced.
- Using String search() With a Regular Expression
```
var str = "Visit W3Schools";
var n = str.search(/w3schools/i);
console.log(n); // 6
```

- Using String search() With String
The search method will also accept a string as search argument. The string argument will be converted to a regular expression:
```
var str = "Visit W3Schools!";
var n = str.search("W3Schools");
console.log(n); // 6
```

- Use String replace() With a Regular Expression
```
var str = "Visit Microsoft!";
var res = str.replace(/microsoft/i, "W3Schools");
console.log(res); // Visit W3Schools!
```

- Using String replace() With a String
```
var str = "Visit Microsoft!";
var res = str.replace("Microsoft", "W3Schools");
console.log(res); // Visit W3Schools!
```

#### 正则表达式的修饰符
| Modifier | Description |
| :--- | :--- |
| i    | 大小写不敏感 |
| g    | 执行全局匹配:将所有匹配的都找出来) |
| m    | 执行多行匹配 |

#### 正则表达式的匹配模式
- Brackets are used to find a range of characters:
| Expression | Description |
| :--- | :--- |
| [abc]    | 匹配中括号内的任意字符 |
| [^abc]   | 匹配非括号内的任意字符 |
| [0-9]    | 匹配0至9的数字 |
| [^0-9]   | 匹配非数字 |
| [a-z]    | 匹配a至z的字母 |
| (x&#124;y)    | 匹配x或y |

- Metacharacters are characters with a special meaning:
| Metacharacter | Description |
| :--- | :--- |
| .     | 匹配除“\r\n”之外的任何单个字符。要匹配包括“\r\n”在内的任何字符，请使用像“[\s\S]”的模式 |
| \w    | Find a word character |
| \W    | Find a non-word character |
| \d    | Find a digit |
| \D    | Find a non-digit character |
| \s    | Find a whitespace character |
| \S    | Find a non-whitespace character |
| \b    | Find a match at the beginning or at the end of a word |
| \B    | Find a match not at the beginning/end of a word |
| \0    | Find a NUL character |
| \n    | Find a new line character |
| \f    | Find a form feed character |
| \r    | Find a carriage return character |
| \t    | Find a tab character | 
| \v    | Find a vertical tab character |
| \xxx  | Find the character specified by an octal number xxx |
| \xdd  | Find the character specified by a hexadecimal number dd |
| \uxxxx    | Find the Unicode character specified by the hexadecimal number xxxx |

- Quantifiers define quantities:
| Quantifier | Description |
| :--- | :--- |
| X+    | 匹配1个或多个的X: Matches any string that contains at least one X |
| X*    | 匹配0个或多个的X: Matches any string that contains zero or more occurrences of X |
| X?    | 匹配0个或1个的X: Matches any string that contains zero or one occurrences of X |
| X{n}  | 匹配n个X: Matches any string that contains a sequence of n X's |
| X{n,} | 匹配至少n个X: Matches any string that contains a sequence of at least n X's |
| X{n, m} | 匹配n至m个X: atches any string that contains a sequence of n to m X's|
| ^X    | 匹配以X开始的: Matches any string with X at the beginning of it |
| $X    | 匹配以X结束的: Matches any string with X at the end of it|
| ?=X   | Matches any string that is followed by a specific string X |
| ?!n   | Matches any string that is not followed by a specific string X |

更多请参考：https://baike.baidu.com/item/正则表达式/1700215?fr=aladdin

#### 使用正则表达式对象
In JavaScript, the RegExp object is a regular expression object with predefined properties and methods.

- 使用test(x)函数: 返回是否能找到匹配, 能找到匹配返回true, 找不到匹配返回false
```
var regExp = /e/;
var testResult = regExp.test('The best things in life are free!');
console.log(typeof(regExp)); //object
console.log(testResult); // true

var regExp2 = new RegExp(/e/);
var testResult2 = regExp.test('The best things in life are free!');
console.log(testResult2); // true

```

- 使用exec(x)函数: 找不到匹配返回null, 找到匹配返回"一个又像数组又像对象的东西"
```
var regExp = /FREE/i;
var foundText = regExp.exec('The best things in life are free!');
console.log(foundText); // ["free", index: 28, input: "The best things in life are free!"] 返回的是一个又像数组又像对象的东西，"好奇怪的家伙""
console.log(foundText[0]); // free
console.log(foundText.index); // 28
console.log(foundText.input); // The best things in life are free!

var regExp2 = /GOOD/i;
var foundText2 = regExp2.exec('The best things in life are free!');
console.log(foundText2); // 无匹配时返回null
```


#### RegExp对象的属性列表
| Property | Description |
| :------- | :---------- |
| constructor | Returns the function that created the RegExp object's prototype |
| global | Checks whether the "g" modifier is set |
| ignoreCase | Checks whether the "i" modifier is set |
| multiline | Checks whether the "m" modifier is set |
| lastIndex | Specifies the index at which to start the next match |
| source | Returns the text of the RegExp pattern |

```
var regExp = /^Good$/i;
console.log(regExp.ignoreCase); //true

regExp = /^Good$/g;
console.log(regExp.global); //true

regExp = /^Good$/m;
console.log(regExp.multiline); //true

console.log(regExp.source); // ^Good$
console.log(regExp.lastIndex); //0

```

***正则表达式的使用示例***
```

// 判断都是都是否数字
function isDigit(str) {
    var regExp = /^[0-9]+$/;
    var result = regExp.test(str);
    return result;
}

// 判断是否都是字母
function isEnglishLetter(str) {

    var regExp = /^[a-zA-Z]+$/;
    var result = regExp.test(str);
    return result;
}

console.log(isDigit('134321'));  // true
console.log(isDigit('a34321'));  // false
console.log(isDigit('34321b'));  // false
console.log(isDigit('34321中')); // false

console.log(isEnglishLetter('abcddABCD')); // true
console.log(isEnglishLetter('134321'));    // false
console.log(isEnglishLetter('abcdd123'));  // false
console.log(isEnglishLetter('abcdd中'));   // false

```

#### RegExp对象的方法列表
| Method | Description |
| :------- | :---------- |
| exec(x) | Tests for a match in a string. Returns the first match |
| test(x) | Tests for a match in a string. Returns true or false |
| toString() | Returns the string value of the regular expression |
| compile() | 1.5版本已经废弃!!!!Deprecated in version 1.5. Compiles a regular expression |

```
var regExp = /Best/i;
var testResult = regExp.test('My best friend.');
var foundResult = regExp.exec('My Best Friend');
var toString = regExp.toString();

console.log(testResult);

console.log(foundResult); // ["Best", index: 3, input: "My Best Friend"]
console.log(foundResult[0]); // Best
console.log(foundResult.index); // 3
console.log(foundResult.input); // My Best Friend

console.log(toString); // /Best/i

```

### 21. JSON
#### 为什么用JSON?
- JSON是JavaScript Object Notation的简写
- JSON是轻量级的数据交换格式
- JSON是独立与编程语言的
- JSON是自描述的且易理解

JSON是使用名值(name:value)对的书写方式，且name必须为双引号包围的字符串. 
跟JavaScript对象不一样的是, JSON的name需要双引号包围，JavaScript对象的name不要双引号包围
```
语法
{"name":value, "name2", value2, ....}
```

name必须是字符串, value可以是数值、字符串、布尔值、对象、数组
```
{
    "age":12, //value是数值
    "name":"JS", //value是字符串
    "isPretty":true, //value是布尔值
    "school" : {"schoolName":"北京大学", "schoolNo":0001}, //value是对象
    "employees":[
        {"firstName":"John", "lastName":"Doe"}, 
        {"firstName":"Anna", "lastName":"Smith"},
        {"firstName":"Peter", "lastName":"Jones"}
    ] //value是数组
}
```

#### JSON文本转换成JavaScript对象：JSON.parse(jsonText)
> JSON是一个全局对象
```
var jsonText = '{"age":12, "name":"JS", "isPretty":true}';

var jsonObj = JSON.parse(jsonText);
console.log(jsonObj.name + ' ' + jsonObj.age + ' ' + jsonObj.isPretty); // JS 12 true

```

#### JavaScript对象转换成JSON文本：JSON.stringify(jsonObj);

```
var obj = {name:'JS', age:12, isPretty:true};
var jsonText = JSON.stringify(obj);
console.log(jsonText); // {"name":"JS","age":12,"isPretty":true}
```

### 22. Global全局属性和函数
#### Global全局属性

| Property | Description |
| :------- | :---------- |
| Infinity | A numeric value that represents positive/negative infinity |
| NaN | "Not-a-Number" value |
| undefined | "Indicates that a variable has not been assigned a value |

#### Global全局函数
| Function | Description |
| :------- | :---------- |
| decodeURI(uri) | Decodes a URI |
| decodeURIComponent(uri) | Decodes a URI component |
| encodeURI(uri) | Encodes a URI |
| encodeURIComponent(uri) | Encodes a URI component |
| parseFloat(str) | Parses a string and returns a floating point number |
| parseInt(str) | Parses a string and returns an integer |
| Number(x) | Converts an object's value to a number |
| String(x) | Converts an object's value to a string |
| isFinite(x) | Determines whether a value is a finite, legal number |
| isNaN(x) | Determines whether a value is an illegal number |
| eval(x) | Evaluates a string and executes it as if it was script code |
| escape(x) | Deprecated in version 1.5. Use encodeURI() or encodeURIComponent() instead |
| unescape(x) | Deprecated in version 1.5. Use decodeURI() or decodeURIComponent() instead |

- encodeURI(uri)/decodeURI(uri)
The encodeURI() function is used to encode a URI.
This function encodes special characters, except: , / ? : @ & = + $ # (Use encodeURIComponent() to encode these characters).

```
var uri = "my test.asp?name=ståle&car=saab";
var enc = encodeURI(uri);
var dec = decodeURI(enc);
console.log(enc); // my%20test.asp?name=st%C3%A5le&car=saab
console.log(dec); // my test.asp?name=ståle&car=saab
```

- encodeURIComponent(uri)/decodeURIComponent(uri)
The encodeURIComponent() function encodes a URI component.
This function encodes special characters. In addition, it encodes the following characters: , / ? : @ & = + $ #

```
var uri = "https://w3schools.com/my test.asp?name=ståle&car=china中国";
var enc = encodeURIComponent(uri);
var dec = decodeURIComponent(enc);
console.log(enc); // https%3A%2F%2Fw3schools.com%2Fmy%20test.asp%3Fname%3Dst%C3%A5le%26car%3Dchina%E4%B8%AD%E5%9B%BD
console.log(dec); // https://w3schools.com/my test.asp?name=ståle&car=china中国

```

### 23. JavaScript的版本

| Year  | Name     | Description |
| :---- | :--------| :-----------|
|1997   |ECMAScript 1  |First Edition.|
|1998   |ECMAScript 2  |Editorial changes only.|
|1999   |ECMAScript 3  |Added Regular Expressions. Added try/catch.|
|       |ECMAScript 4  |Was never released.|
|2009   |ECMAScript 5  |Added "strict mode". Added JSON support.|
|2011   |ECMAScript 5.1|Editorial changes.|
|2015   |ECMAScript 6  |Added classes and modules.|
|2016   |ECMAScript 7  |Added exponential operator (**).Added Array.prototype.includes.|
> **ECMAScript 6** is also called **ECMAScript 2015**.
> **ECMAScript 7** is also called **ECMAScript 2016**.

[相关版本在浏览器兼容性见JavaScript Versions](https://www.w3schools.com/js/js_versions.asp)

### 24. 参考资料

https://www.w3schools.com
