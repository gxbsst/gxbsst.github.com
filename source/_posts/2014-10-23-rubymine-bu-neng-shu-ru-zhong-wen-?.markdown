---
layout: post
title: "rubymine 不能输入中文？"
date: 2014-10-23 10:14:26 +0800
comments: true
categories: rubymine ide
---

如果你的rubymine 不能输入中文，请做这样的修改:

``` bash
 vim /Applications/RubyMine.app/bin/idea.vmoptions
```

加入下面一行：
``` java
-J-Djava.awt.im.style=on-the-spot
```
所以长得这样子:

``` java
-Xms128m
-Xmx512m
-XX:MaxPermSize=250m
-XX:+UseCompressedOops
-J-Djava.awt.im.style=on-the-spot
```

–EOF–