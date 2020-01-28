# number

在 JavaScript 中, Number是一种定义为[64位双精度浮点型（double-precision 64-bit floating point format） (IEEE 754)的数字数据类型](https://en.wikipedia.org/wiki/Double-precision_floating-point_format)

## 格式/精度

![pic](https://tva1.sinaimg.cn/large/006tNbRwly1gb0pqdx0adj30gi02ogld.jpg)

* 第1位：符号位，`0`正数，`1`负数
* 第2 ~ 11位 (共11位): 指数
* 第13 ~ 64位 (共52位): 小数部分(有效数字)

```sh
// 如果指数部分的值在0~2047之间，第一位的有效数子总是1，并且不保存在64位浮点数之中。
// .xx...xx最长可能是52位，因此，js中的有效数字长度最长为53个进制

(-1)^符号位 * 1.xx...xx * 2^指数部分
```

##### Js可以精确表示[-2^53 ~ 2^53]这个范围的数字，由于2的53次方是一个16进制数值，所以简单的法则就是，JavaScript对于15位的十进制都可以精确处理

## 范围

由于指数部分的长度是11个二进制位，所以指数部分的最大值是2047(2^11 - 1)。

##### JavaScript 能够表示的数值范围是 (-2^1024, 2^1024)，超出这个范围的数字就无法表示

```js
// 正向溢出，会返回 Infinity
Math.pow(2, 1024) // Infinity

// 负向溢出，会返回 0
Math.pow(2, -1075) // 0

// 最大值
Number.MAX_VALUE // 1.7976931348623157e+308
// 最小值
Number.MIN_VALUE // 5e-324
```

## 表示方法

* 多种进制
* 十进制
* 十六进制
* 科学计数法

有两种情况，js会将数值转为科学计数法表示，其他情况都采用字面形式直接表示。

* 小数点前的数字多于21位

```sh
1234567890123456789012
// 1.2345678901234568e+21

123456789012345678901
// 123456789012345680000
```

* 小数点后的零多于5位

```sh
// 小数点后紧跟5个以上的零，
// 就自动转为科学计数法
0.0000003 // 3e-7

// 否则，就保持原来的字面形式
0.000003 // 0.000003
```

## 进制

对于整数提供4种进制的表示方法：

* 十进制: 没有前导`0`的数值
* 八进制：有前缀`0O`或`0o`的数值，或者有前导`0`,且只用到0-7的阿拉伯数字的值
* 十六进制：有前缀`0x`或`0X`的数值
* 二进制：有前缀`0b`或`0B`的数值

但是在默认情况下，js内部会自动将八、十六、二进制转为十进制。**使用前导0的数值表示八进制，在es5的严格模式和es6已经废除**

## 特殊数值

#### +0 / -0

js的64位浮点数之中，有一个二进制是符号位，所以每一个数都有正负值。

有关于 +0/-0之间唯一有区别的是当作分母时返回的值是不相等的。一个返回`Infinity`，一个返回`-Infinity`

## NaN

`NaN`是一个**特殊的数值**,`typeof NaN === 'number'`, 表示 Not a Number (非数字)。

###### 运算规则

```js
// NaN不等一任何值，包括它本身
NaN === NaN // false

// 数组的indexof方法对于NaN不成立
[NaN].indexof(NaN) // -1

// 在布尔运算中会被当成 false
Boolean(NaN) // false

// 它与任何数(包括自己)进行运算，返回值都是NaN
NaN - 0 // NaN
```

## infinity

* `+Infinity` 表示正无穷
* `-Infinity` 表示负无穷

###### 运算规则_

`Infinity`大于一切数值，`-Infinity`小于一切数值。(除了`NaN`)

```js
Infinity > NaN // false
-Infinity > NaN // false

Infinity < NaN // false
-Infinity < NaN // false
```

`Infinity`的四则运算符合无穷的数学计算规则

## 与数值有关的全局方法

###### 1. `parseInt()` [Standard build-in Objects]

* 这个`parseInt()`与`Number.parseInt()`有区别


