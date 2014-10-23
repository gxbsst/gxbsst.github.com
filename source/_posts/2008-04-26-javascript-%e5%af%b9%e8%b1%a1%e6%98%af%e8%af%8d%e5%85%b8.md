---
title: JavaScript 对象是词典
author: gxbsst
layout: post
permalink: /archives/74
post_views_count:
  - 106
views:
  - 50
categories:
  - Javascript
---
引用：link  
记住文章的题目：JavaScript 对象是词典“.才会有下面的方法

<pre lang="javascript">function sayHi(x) {
alert(”Hi, “ + x + ”!“);
}
sayHi.text = ”Hello World!“;
sayHi[”text2“] = ”Hello World... again.“;

alert(sayHi[”text“]); // displays ”Hello World!“
alert(sayHi.text2); // displays ”Hello World... again.“
</pre>

看到有什么分别么？sayHi[”text2“]＝sayHi.text，sayHi[”text2“]感觉想一个数组中的值，这和JavaScript 对象是词典的描述是吻合的

作为对象，函数还可以赋给变量、作为参数传递给其他函数、作为其他函数的值返回，并可以作为对象的属性或数组的元素进行存储等等  
在 C# 中，我们使用类来实例化对象实例。但 JavaScript 与此不同，因为它没有类。您将在下一节中看到，您可以充分利用这一情况：函数在与”new“运算符一起使用时，函数将充当构造函数。  
构造函数而不是类

前面提到过，有关 JavaScript OOP 的最奇怪的事情是，JavaScript 不像 C# 或 C++ 那样，它没有类。在 C# 中，在执行类似下面的操作时：

Dog spot = new Dog();

将返回一个对象，该对象是 Dog 类的实例。但在 JavaScript 中，本来就没有类。与访问类最近似的方法是定义构造函数，如下所示：

<pre lang="javascript">function DogConstructor(name) {
this.name = name;
this.respondTo = function(name) {
if(this.name == name) {
alert(”Woof“); 
}
};
}

var spot = new DogConstructor(”Spot“);
spot.respondTo(”Rover“); // nope
spot.respondTo(”Spot“); // yeah!
</pre>

那么，结果会怎样呢？暂时忽略 DogConstructor 函数定义，看一看这一行：

<pre lang="javasript">var spot = new DogConstructor(”Spot“);
</pre>

”new“运算符执行的操作很简单。首先，它创建一个新的空对象。然后执行紧随其后的函数调用，将新的空对象设置为该函数中”this“的值。换句话说，可以认为上面这行包含”new“运算符的代码与下面两行代码的功能相当：

<pre lang="javascript">// create an empty object
var spot = {}; 
// call the function as a method of the empty object
DogConstructor.call(spot, ”Spot“);
</pre>

正如在 DogConstructor 主体中看到的那样，调用此函数将初始化对象，在调用期间关键字”this“将引用此对象。这样，就可以为对象创建模板！只要需要创建类似的对象，就可以与构造函数一起调用”new“，返回的结果将是一个完全初始化的对象。这与类非常相似，不是吗？实际上，在 JavaScript 中构造函数的名称通常就是所模拟的类的名称，因此在上面的示例中，可以直接命名构造函数 Dog：

<pre lang="javascript">// Think of this as class Dog
function Dog(name) {
// instance variable 
this.name = name;
// instance method? Hmmm...
this.respondTo = function(name) {
if(this.name == name) {
alert(”Woof“); 
}
};
}

var spot = new Dog(”Spot“);
</pre>

在上面的 Dog 定义中，我定义了名为 name 的实例变量。使用 Dog 作为其构造函数所创建的每个对象都有它自己的实例变量名称副本（前面提到过，它就是对象词典的条目）。这就是希望的结果。毕竟，每个对象都需要它自己的实例变量副本来表示其状态。但如果看看下一行，就会发现每个 Dog 实例也都有它自己的 respondTo 方法副本，这是个浪费；您只需要一个可供各个 Dog 实例共享的 respondTo 实例！通过在 Dog 以外定义 respondTo，可以避免此问题，如下所示：

<pre lang="javascript">function respondTo() {
// respondTo definition
}

function Dog(name) {
this.name = name;
// attached this function as a method of the object
this.respondTo = respondTo;
}

</pre>

这样，所有 Dog 实例（即用构造函数 Dog 创建的所有实例）都可以共享 respondTo 方法的一个实例。但随着方法数的增加，维护工作将越来越难。最后，基本代码中将有很多全局函数，而且随着”类“的增加，事情只会变得更加糟糕（如果它们的方法具有相似的名称，则尤甚）。但使用原型对象可以更好地解决这个问题，这是下一节的主题。

但 JavaScript 本身并不支持私有成员（同样，也不支持受保护成员）。任何人都可以访问对象的所有属性和方法。但我们有办法让类中包含私有成员，但在此之前，您首先需要理解闭包。

转载请注明：[韦旭红的点点滴滴][1] &raquo; [JavaScript 对象是词典][2]

 [1]: http://www.weixuhong.com
 [2]: http://www.weixuhong.com/archives/74