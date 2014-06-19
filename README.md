
##ECMAScript 知识点整理##

----

**数据类型**

----


ECMAScript中有5种基本数据类型：`Undefined` `Null` `Boolean` `Number` `String` 和1种复杂数据类型`Object`

**Undefined类型**

value:`undefined`使用var声明一个变量未初始化时，这个变量的值就是undefined，例如：
		
	var message;
	
	alert(message == undefined); // true

`typeof undefined` ==> 'undefined'


**Null类型**

value: `null`表示一个空对象的指针

undefined == null // true

undefined === null // false

`typeof null` ==> 'object'

**Boolean类型**

true | fase

要将一个值转换为Boolean可以调用转型函数Boolean()例如：

	var message = 'hello world';
	
	var messageAsBoolean = Boolean(message);
	
可以对任何数据类型的值调用Boolean()函数，而且总会返回一个Boolean值，至于返回的是true还是false则取决于要转换值的数据类型及其实际值。

**数据类型** **转换为true的值** **转换为false的值**

Boolean true false

String 任何非空字符串 ‘’空字符串

Number 任何非零数字值（包括无穷大） 0和NaN

Object 任何对象 0和null

Undefined 不适用 undefined


**面向对象（OOP）**

----


**函数**

----





**BOM**

----



**DOM**

----



**事件**

----


**AJAX&JSON**

----
