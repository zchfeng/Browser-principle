## JS 执行顺序：先编译后执行

### 源码

```
showName();
console.log(myname);
var myname = '2222';
function showName(){
  console.log('1111');
}

```

先编译：编译的时候会把一些变量进行变量提示

```
var myname = undefined;
function showName(){
  console.log('1111');
}
showName();
console.log(myname);
myname = '2222'

```

再执行

```
showName();
console.log(myname);
myname = '2222'''

```

输出结果：'1111', undefined.

### 解析源码

```
showName();
console.log(myname);
var myname = '2222';
function showName(){
  console.log('1111');
}

```

- 第一行和第二行，由于两行不是声明操作，所以 JavaScript 引擎不会做任何处理。
- 第三行，由于这行是经过 var 声明的，因此 JavaScript 引擎将在环境对象中创建一个名为 myname 的属性，并使用 undefined 对其初始化；
- 第四行，JavaScript 引擎发现一个通过 function 定义的函数，所以它将函数定义储存到堆中，并在环境对象中创建一个 showName 的属性，这个属性值指向堆中函数的位置。
