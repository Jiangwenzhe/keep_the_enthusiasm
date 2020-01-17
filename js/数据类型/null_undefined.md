# null 、 undefined

## null

值`null`特别指对象的值未设置，属于js的基本类型之一，在布尔运算中被认为是[falsy](https://developer.mozilla.org/zh-CN/docs/Glossary/Falsy)

## undefined

用于表示一个声明未定义的变量的初始值或者是没有实际参数的形参

```js
// 一个声明未定义的变量的初始值
let i;
i;        // undefined

// 没有实际参数的形参
function f(x) {
  console.log(x);
  return 1;
}
f();      // undefined 1

// 对象没有赋值的属性
const obj = new Object();
obj.a     // undefined

// 函数没有返回值，默认返回undefined
function f() {}
f() // undefined
```

## null vs undefined

```js
typeof null        // "object" (因为一些以前的原因而不是'null')
typeof undefined   // "undefined"
null === undefined // false
null  == undefined // true
null === null // true
null == null // true
undefined === undefined // true
undefined == undefined // true
!null //true
isNaN(1 + null) // false
isNaN(1 + undefined) // true 啥数和undefined碰一起都是 NaN
```
