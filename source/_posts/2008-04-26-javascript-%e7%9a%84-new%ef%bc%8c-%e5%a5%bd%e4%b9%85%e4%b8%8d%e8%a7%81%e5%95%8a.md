---
title: JavaScript 的 new， 好久不见啊
author: gxbsst
layout: post
permalink: /archives/113
post_views_count:
  - 136
views:
  - 32
categories:
  - Javascript
---
原文： JavaScript, We Hardly new Ya －－Douglas Crockford。

JavaScript是一门基于原型的语言，但它却拥有一个 new 操作符使得其看起来象一门经典的面对对象语言。那样也迷惑了程序员们，导致一些有问题的编程模式。

其实你永远不需要在JavaScript使用 new Object()。用字面量的形式{}去取代吧。

同理，不要使用 new Array() ，而代之以字面量[]。JavaScript中的数组并不象Java中的数组那样工作的，使用类似Java的语法只会让你糊涂。

同理不用使用 new Number, new String, 或者 new Boolean。这些的用法只会产生无用的类型封装对象。就直接使用简单的字面量吧。

不要使用 new Function 去创建函数对象。用函数表达式更好。比如：

frames[0].onfocus = new Function(”document.bgColor=’antiquewhite’”)

更好的写法是：

frames[0].onfocus = function () {document.bgColor = ‘antiquewhite’;};

第二种形式让脚本编译器更快的看到函数主体，于是其中的语法错误也会更快被检测出来。有时候程序员使用 new Function 是因为他们没有理解内部函数是如何工作的。

selObj.onchange = new Function(”dynamicOptionListObjects[”+  
dol.index+”].change(this)”);

如果我们让用字符串做函数体，编译器不能看到它们。如果我们用字符串表达式做函数体，我们同样也看不到它们。更好的方式就是不要盲目编程。通过制造一个返回值为函数的函数调用，我们可以明确的按值传递我们想要绑定的值。这允许我们在循环中初始化一系列 selObj 对象。

selObj.onchange = function (i) {  
return function () {  
dynamicOptionListObjects[i].change(this);

};  
}(dol.index);

直接对一个函数使用new永远不是一个好主意。比如， new function 对构造新对象没有提供什么优势。

myObj = new function () {  
this.type = ‘core’;  
};

更好的方式是使用对象字面量，它更轻巧，更快捷。

myObj = {  
type: ‘core’  
};

假如我们需要创建的对象包含的方法需要访问私有变量或者函数，更好的方式仍然是避免使用new.var foo = new function() {  
function processMessages(message) {  
alert(”Message: ” + message.content);  
}  
this.init = function() {  
subscribe(”/mytopic”, this, processMessages);  
}  
}通过使用 new 去调用函数，对象会持有一个无意义的原型对象。这只会浪费内存而不会带来任何好处。如果我们不使用new，我们就不用在对象链维护一个无用的prototype对象。所以我们可以用（）来正确的调用工厂函数。var foo = function () {  
function processMessages(message) {  
alert(”Message: ” + message.content);  
}  
return {  
init: function () {  
subscribe(”/mytopic”, this, processMessages);  
}  
};  
}();所以原则很简单： 唯一应该要用到new操作符的地方就是调用一个古老的构造器函数的时候。当调用一个构造器函数的时候，是强制要求使用new的。有时候可以来new一下, 有的时候还是不要了吧。

转载请注明：[韦旭红的点点滴滴][1] &raquo; [JavaScript 的 new， 好久不见啊][2]

 [1]: http://www.weixuhong.com
 [2]: http://www.weixuhong.com/archives/113