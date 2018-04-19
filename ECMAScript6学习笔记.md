[TOC]

## ECMAScript6学习笔记

### Variables变量
#### let: 定义具有块作用域的变量
我们之前通常使用var声明定义变量。现在可以使用let声明定义变量，let与var的区别在于作用域不同，let定义的变量具有块(block)作用域
```
function test() {
    
    if (true) {
        var varX = 100;
        let letX = 30;
    }

    console.log(varX); // 100
    console.log(letX); // ReferenceError: letX is not defined.
}

test();

```
let定义的变量不存在变量提升
```
varX = 30;
console.log(varX); // 30

letX = 20;
console.log(letX); // ReferenceError: letX is not defined.

var varX;
let letX;

```

#### const: 定义常量
const声明定义的变量具有跟let一样的块作用域，必须声明后立即赋值，之后不能改变
```
const myConst = 3;//声明后立即赋值
myConst = 4; //Uncaught TypeError: Assignment to constant variable.

const myConst2;
myConst2 = 5; //Uncaught SyntaxError: Missing initializer in const declaration

```

> 请注意：如果const用在对象类型，只是变量不能再赋值, 但是对象内部仍然可改变

```
const myConstObj = {name:'ES6', age:2};
myConstObj.name = 'ES7'; //对象内部可以改变
console.log(myConstObj.name); //ES7
myConstObj = {age:30}; //Uncaught TypeError: Assignment to constant variable.

```

### Arrow Functions箭头函数

http://qnimate.com/javascript-arrow-function/

```
() => FunctionExpression
(args) => { FunctionExpression }
```

```
let books = [{title: 'X', price: 10}, {title: 'Y', price: 15}];

let titles = books.map( (item) => item.title );
console.log(titles); // ["X", "Y"]

// ES5 equivalent:
var titles2 = books.map(function(item) {
   return item.title;
});
console.log(titles2); // ["X", "Y"]

```

箭头函数没有function关键字，包含0个或多个参数、箭头=>、函数表达式

```
// 没有参数的情况
let books = [{title: 'X', price: 10}, {title: 'Y', price: 15}];
let titles = books.map( () => 1 );
console.log(titles); // [1, 1]

// 多个参数的情况
let result = [1,2].map( (n, index) => n * index ); // [0, 2]
console.log(result); // [0, 2]

```

```
// 1. One parameter 

// in ES6
let sum = (a, b) => a + b;
 
// in ES5
var sum = function(a, b) {
    return a + b; 
};

 
// 2. Without parameters 
// in ES6
let randomNum = () => Math.random();
 
// in ES5
var randomNum = function() {
    return Math.random(); 
};
 

// 3. Without return 
//in ES6
let message = (name) => alert("Hi " + name + "!"); 
 
// in ES5
var message = function(yourName) {
    alert("Hi " + yourName + "!");  
};
```

如果函数表达式比较复杂可以用{}包着
```
let result = [1, 2, 3, 4, 5].map( n => {
   n = n % 3;
   return n;
});
console.log(result); // [1, 2, 0, 1, 2]
```

There’s an important difference between regular and arrow functions, that is arrow functions don’t receive a this value automatically like functions defined with the function keyword do. Arrow functions lexically bind the this value to the current scope. This means that we can easily reuse the this keyword in an inner function. In ES5 it is only possible with the following hack:
```
// ES5 Hack to use the "this" keyword in an inner function
{
  ...
  addAll: function addAll(pieces) {
    var self = this;
    _.each(pieces, function (piece) {
      self.add(piece);
    });
  },
  ...
}
 
// ES6 the same inner function now can use its own "this"
{
  ...
  addAll: function addAll(pieces) {
    _.each(pieces, piece => this.add(piece));
  },
  ...
}
```

```
function Person() {

    this.name = 'name',
    this.func1 =  function (a) {
        console.log('111');
        console.log(this);
        
        this.func2(function() {console.log('222');console.log(this);});
        this.func2(()=> {console.log('333');console.log(this);});
        a();
    },
    this.func2 = function (b) {
        console.log('444');
        console.log(this);
        b();
    }
}

var person = new Person();
person.func1(() => {
    console.log('555');
    console.log(this);
});
```

### … spread Operator 展开操作符
```
let myArray = [1, 2, 3];
 
let newArray = [...myArray, 4, 5, 6];//展开数组
 
console.log(newArray); // 1, 2, 3, 4, 5, 6
```

We can also take leverage of the spread operator in function calls in which we want to pass in arguments from an array:
```
let myArray = [1, 2, 3];
 
function sum(a, b, c) {
  return a + b + c;
}
 
console.log(sum(...myArray));
```


### Default Values for Parameters 函数参数设置默认值
```
function sum(a = 2, b = 4) {
  return a + b;
}
 
console.log( sum() ); // 6
console.log( sum(3, 6) ); // 9
```

### Rest Parameters 可变参数
ES6 also introduces a new kind of parameter, the rest parameters. They look and work similarly to spread operators. They come handy if we don’t know how many arguments will be passed in later in the function call. We can use the properties and methods of the Array object on rest parameters:
```
function putInAlphabet(...args) {
   
    // 可变参数当做数组使用, 可以调用数组的属性和方法
    console.log(args.length); // 10
    console.log(args.concat()); // ["e", "c", "m", "a", "s", "c", "r", "i", "p", "t"]

    let sorted = args.sort();
    return sorted;
}
 
console.log( putInAlphabet("e","c","m","a","s","c","r","i","p","t") ); // a,c,c,e,i,m,p,r,s,t
```


### for...of遍历语句
for...of遍历语句可以用来遍历Array、Map、Set

```
//遍历数组
let myArray = [1, 2, 3, 4, 5];
let sum = 0;
for (let i of myArray) {
  sum += i;
}
console.log(sum); // 15 (= 1 + 2 + 3 + 4 + 5)

let myArray2 = [{'name':'JS', desc:'Good'}, {'name':'JS2', desc:'Good2'}];
let names = '';
for (let item of myArray2) {
  names += item.name + ' ';
}
console.log(names); // JS JS2 

```

### Template Literals
ECMAScript 6提供了另一种拼接字符串的方式: 模板字符串
语法: ${...}
```
let customer = { title: 'Ms', firstname: 'Jane', surname: 'Doe', age: 34 };
 
let template = `${customer.age}${customer.age} Dear ${customer.title} `; //使用模板字符串实现字符串拼接
let normalStr = customer.age + customer.age + ' Dear ' + customer.title + ' ' ; //使用+拼接字符串
 
console.log(template); // 3434 Dear Ms 注意：模板字符串始终当字符串出来再拼接
console.log(normalStr); // 68 Dear Ms       这里的+拼接遇到+左右都是数字时发现数学加法运算而不是单纯在字符串拼接

```

### Class 类
ES6引入了class关键字定义类，并且引入了默认的构造函数constructor()

class定义类

```
class Polygon {
  constructor(height, width) { //class constructor
    this.name = 'Polygon';
    this.height = height;
    this.width = width;
  }
 
  sayName() { //class method
    console.log('Hi, I am a', this.name + '.', this.height, this.width);
  }
}
 
let myPolygon = new Polygon(5, 6);
myPolygon.sayName(); //Hi, I am a Polygon.

let myPolygon2 = new Polygon();
myPolygon2.sayName(); //Hi, I am a Polygon. undefined undefined

```

extends继承
```
class Student {

    //constructor of the class
    constructor(name, age) {
        //"this" points to the current object
        this.name = name;
        this._age = age;
    }

    //member function
    getName() {
        return this.name;
    }

    setName(name) {
        this.name = name;
    }

    //getters and setters make a function accessible like a variable. They are used as wrappers around other variables.
    set age(value) {
        this._age = value;
    }

    get age() {
        return this._age;
    }
}

//class person inherits student class
class Person extends Student {

    constructor(name, age, citizen) {
        //this points to the person class
        this.citizen = citizen;

        //call constructor of super class. "super" is an pointer to the super class object
        super(name, age);
    }

    getCitizen() {
        return this.citizen;
    }

    //overriding
    getName() {
        //we are calling the super class getName function
        return super.getName();
    }
}

//instance of student class
var stud = new Student("Narayan", 21);

//instance of person class
var p = new Person("Narayan Prusty", 21, "India");

stud.age = 12; //executes setter
console.log(stud.age); //executes getter
```

### Module 模块

We need to define each module in its own file, then use the export keyword to export variables and functions to other files, and the import keyword to import them from other files, according to the following syntax:

```
// functions.js
 
  function cube(a) {
    return a * a * a;
  }
 
  function cubeRoot(a) {
    return Math.cbrt(a);
  }
 
  export { cube, cubeRoot}
  // or: export { cube as cb, cubeRoot as cr }
 
// app.js
 
  import { cube, cubeRoot } from 'functions';
 
  console.log(cube(4)); // 64
 
  console.log(cubeRoot(125)); // 5
```

```
math.js
export class Math {

    constructor() {
        this.sum = function(x, y){
            return x + y;
        }

        this.sub = function(x, y){
            return x - y;
        }
    }

    findSum(a, b) {
        return this.sum(a, b);
    }

    findSub(a, b) {
        return this.sub(a, b);
    }
}

app.js

import {Math} from 'math';

var math = new Math();

console.log(math.findSum(1, 2)); //3
console.log(math.findSub(1, 2)); //-1

```

### Function Return Multiple Values
```
function function_name() {
    return [1, 6, 7, 4, 8, 0]; //here we are storing variables in an array and returning the array
}

var q, w, e, r, t, y;

//Here we are using ES6's array destructuring feature to assign the returned values to variables.
//Here we are ignoring 2 and 4 array indexes
[q, w, , r, , y] = function_name();

alert(y);//y is 0
```

ES6 provides a array like syntax to assign multiple variables to values of array indexes. It also lets you ignore some array indexes.

### Set
JavaScript “Set” object is a collection of unique keys. Keys are object references or primitive types.
与数组不同，Set集合内元素不能重复

```
//create a set
var set = new Set();

//add three keys to the set
set.add({x: 12});
set.add(44);
set.add("text");

//check if a provided key is present
console.log(set.has("text"));

//delete a key
set.delete(44);

//loop through the keys in an set
for(var i of set) {
    console.log(i);
}

//create a set from array values
var set_1 = new Set([1, 2, 3, 4, 5]); 

//size of set
console.log(set_1.size); //5

//create a clone of another set
var set_2 = new Set(set.values());
```

### Weak Set
JavaScript Set and WeakSet objects allows you to store collection of unique keys. But there are some key differences between them. Here are the differences:

- They both behave differently when a object referenced by their keys gets deleted. Lets take the below example code:
```
var set = new Set();
var weakset = new WeakSet();

(function(){
    var a = {x: 12};
    var b = {y: 12};

    set.add(a);
    weakset.add(b);
})()
```

One the above self invoked function is executed there is no way we can reference {x: 12} and {y: 12} anymore. Garbage collector goes ahead and deletes the key b pointer from “WeakSet” and also removes {y: 12} from memory. But in case of “Set”, the garbage collector doesn’t remove a pointer from “Set” and also doesn’t remove {x: 12} from memory.

So “Set” can cause more garbages in memory. We can say that “Set” references are strong pointer whereas “WeakSet” references are weak pointers.

- “WeakSet” keys cannot be primitive types. Nor they can be created by an array or another set.
```
var set = new Set([1,2,3,4]);

//cannot be created from array or another set
var weakset = new WeakSet();
weakset.add({a: 1}); //object reference must
```

- “WeakSet” doesn’t provide any methods or functions to work with the whole set of keys. For example: size, looping etc.
```
var set = new Set([1,2,3,4]);

//cannot be created from array
var weakset = new WeakSet();
weakset.add({a: 1}); //object reference must

console.log(set.size);//4
console.log(weakset.size);//undefined

for(var i of set) {
    console.log(i); //1,2.3.4
}

//doesn't execute throws error
for(var i of weakset) {
    console.log(i);
}

set.clear();
weakset.clear(); //This works
```

### Map
JavaScript “Map” object is a collection of unique keys and corresponding values. Keys and Values can be object references or primitive types.
2D Arrays can store duplicate values but Maps don’t store duplicate keys, this is what makes it different from 2D arrays.
A JavaScript “Set” object can store only keys but “Map” can store key and value pairs.

```
//create a map
var map = new Map();

//add three keys & values to the map
map.set({x: 12}, 12);

//same key is overwritten
map.set(44, 13);
map.set(44, 12);

//check if a provided key is present
console.log(map.has(44)); //true

//retrieve key
console.log(map.get(44)); //12

//delete a key
map.delete(44);

//loop through the keys in an map
for(var i of map) {
    console.log(i);
}

//delete all keys
map.clear();

//create a map from arrays
var map_1 = new Map([[1, 2], [4, 5]]); 

//size of map
console.log(map_1.size); //2
```

### Weak Map
JavaScript “Map” and “WeakMap” objects allows you to store collection of unique keys and their corresponding values. But there are some key differences between them. Here are the differences:

- They both behave differently when a object referenced by their keys/values gets deleted.
```
var map = new Map();
var weakmap = new WeakMap();

(function(){
    var a = {x: 12};
    var b = {y: 12};

    map.set(a, 1);
    weakmap.set(b, 2);
})()
```

One the above self invoked function is executed there is no way we can reference {x: 12} and {y: 12} anymore. Garbage collector goes ahead and deletes the key b pointer from “WeakMap” and also removes {y: 12} from memory. But in case of “Map”, the garbage collector doesn’t remove a pointer from “Map” and also doesn’t remove {x: 12} from memory.

So “Map” can cause more garbages in memory. We can say that “Map” references are strong pointer whereas “WeakMap” references are weak pointers.

- “WeakMap” keys cannot be primitive types. Nor they can be created by an 2D array.
```
map.set(44, 12);

//throws invalid type error
weakmap.set(44, 13);

//doesn't work. throws errors
var map_1 = new WeakMap([[1, 2], [4, 5]]);
```

- “WeakMap” doesn’t provide any methods or functions to work with the whole set of keys. For example: size, looping etc.
```
console.log(weakmap.size); //undefined


//loop through the keys in an map
for(var i of map) {
    console.log(i);
}

//loop through the keys in an weakmap doesn't work
for(var i of weakmap) {
    console.log(i);
}

//delete all keys
map.clear();
weakmap.clear(); //but this works
```

<!-- ### Loads of New Methods
function isPrime(element, index, array) {
  var start = 2;
  while (start <= Math.sqrt(element)) {
    if (element % start++ < 1) {
      return false;
    }
  }
  return element > 1;
}
 
console.log([4, 6, 8, 12].find(isPrime)); 
// undefined, not found
 
console.log([4, 5, 8, 12].find(isPrime)); 
// 5



http://www.hongkiat.com/blog/ecmascript-6/
http://qnimate.com/post-series/ecmascript-6-complete-tutorial/

Variables and Parameters
Classes
Proxies
Build-in Objects and Prototype based features
Promises
Reflect API
Modules
Iterators and Generators
 -->
