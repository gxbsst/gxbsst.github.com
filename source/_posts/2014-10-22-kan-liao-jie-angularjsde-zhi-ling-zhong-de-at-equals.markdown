---
layout: post
title: "看了解AngularJs的指令中的@,="
date: 2014-10-22 18:08:15 +0800
comments: true
categories: angularjs directive
---

###Attribute Isolated Scope
Defined with an @ symbolBinds a local scope property to the value of a DOM attribute The binding is uni-directional from parent to directiveThe result is always a string because DOM attributes are strings

{% img  /images/directive_1.png  600 'image' 'images' %}

###Binding Isolated Scope
Defined with an = symbolBi-directional binding between parent and directive You can define the binding as optional via =? Optimal for dealing with objects and collections

{% img  /images/directive_2.png  600 'image' 'images' %}
###Expression Isolated Scope
Defined using an & symbolAllows you to execute an expression on the parent scope To pass variables from child to parent expressions you must use an object map{% img  /images/directive_3.png  600 'image' 'images' %}