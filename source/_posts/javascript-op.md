title: JavaScript操作符使用注意事项
id: 54
categories:
  - 前端开发
date: 2015-03-11 00:00:00
tags:
---

javascript 的操作符运算中有很多是可以适用于不同类型的值，这是因为javascript本身是一门变量类型松散型的语言，在使用运算符的时候有很多容易出错的地方。加法和减法这两个运算符是各种开发语言中用得最多的运算符了，但是在ECMAScript中，这两个操作符却有一系列特殊行为。
<!--more-->
1、加法：
如果+号的两个操作数有一个是字符串，那么就有下面的规则：
两个操作数都是字符串的时候，那么结果就是两个字符串拼接；
只有一个是字符串，那么将另外一个操作数转化为字符串，然后两个字符串拼接
如果有一个操作数是对象、数值或者布尔值，则调用它们的toString()方法取得相应的字符串值，再按照上面的规则。

比如:

```
var res = 5+5; //两个数值相加，结果为10
var res2 = 5+“5”; //一个数值和一个字符串相加，结果为"55"
```

编程中常犯的一个错误就是当我们想要得到相加结果，我们很容易这么写：

```
var num1 = 5;
var num2 = 10;
var msg = "The sum of 5 and 10 is " + num1 +num2; //错误结果
```

这样我们得到的结果竟然是“The sum of 5 and 10 is 510”。出现这样的情况就是因为运算规则是从左到右，前面一个加号是字符串和数值相加，根据上面的规则，结果为字符串，然后再进行下一步加法时，还是字符串和数值的相加，结果就会出现上面的错误，正确的写法是将后两个数值相加就和之后再与字符串合并，即：

```
var num1 = 5;
var num2 = 10;
var msg = "The sum of 5 and 10 is " +（ num1 +num2）; // The sum of 5 and 10 is 15
```
2、减法：
减法和加法类似，但是参数转换略有不同，减法的两个操作数其中一个是字符串、布尔值或者对象的时候，后台调用Number() 函数将其转换为数值再进行减法运算。比如：

```
var res1 = 5 - true; //4，因为true被转换成1
var res2 = 5 - ""; //5，因为""被转化成0
var res3 = 5 - "2"; //3，因为"2"被转化成数值2
```

3、相等操作符：
javascript中==和===不一样。前一个是相等操作符，在比较之前会进行类型强制转换，也就是说true==1、null==undefined是成立的。但是后一个操作符是全等操作符，比较之前不会进行类型转换，所以全等的前提是类型和值都相等，关系才成立。

还有很多类似的小细节，使用者在开发过程中一定要注意这些可能造成致命错误的细节。