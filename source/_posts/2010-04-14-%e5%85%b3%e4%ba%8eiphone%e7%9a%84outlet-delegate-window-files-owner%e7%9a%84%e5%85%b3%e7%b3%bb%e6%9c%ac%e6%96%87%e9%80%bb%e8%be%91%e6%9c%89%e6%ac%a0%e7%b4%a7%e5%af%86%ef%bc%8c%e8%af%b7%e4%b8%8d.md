---
title: '关于iPhone的outlet, delegate, window, file&#8217;s Owner的关系(本文逻辑有欠紧密，请不要随便转载，以免误人子弟)'
author: gxbsst
layout: post
permalink: /archives/476
aktt_notify_twitter:
  - no
qzone:
  - 'true'
post_views_count:
  - 274
views:
  - 129
categories:
  - IOS
  - 心情随写
---
*本文仅供参考，不是权威教程，欢迎讨论

<div style="text-align:center;">
  <img src="http://blog.hellojessica.info/wp-content/uploads/2010/04/Screen-shot-2010-04-14-at-10.51.18-PM.png" alt="Screen shot 2010-04-14 at 10.51.18 PM.png" border="0" width="816" height="703" />
</div>

一个iPhone程序 启动的时候估计有UIApplication, Delegate, Controller, 还有UI(xib文件), 但是他们是如何工作的呢？

为什么要用Outlet?  
我的想法:  
比如ROR程序中，要使用Views，views中要使用某个实例变量（当然这样比喻估计不是准确), 那在iPhone程序怎么实现呢？ 那就用outlet， 比如window &#8212;> Window， 图中表示 Delegate 的outlet window 引用了 Window， 那么Delegate实例就可以使用Window实例的方法：

delegate.m 文件中有这样一个例子

- (void)applicationDidFinishLaunching:(UIApplication *)application {  
[window addSubview:switchViewController.view];

// Configure and show the window  
[window makeKeyAndVisible];

}

假想:

**UIApplication**

UIApplication 是这个核心，它调度controller等的工作，我就把它想象成ROR的一个Application，那为什么UIApplication会有一个Outlets delegate==> Delegate呢？ 这个意味着UIApplication实例可以调用Delegate实例， 但是delegate这个outlet在哪里定义呢？ 这个是我比较迷惑的地方? 或许 UIApplication 类就有这样一个outlet.

<div style="text-align:center;">
  <img src="http://blog.hellojessica.info/wp-content/uploads/2010/04/Screen-shot-2010-04-14-at-10.57.30-PM.png" alt="Screen shot 2010-04-14 at 10.57.30 PM.png" border="0" width="816" height="706" />
</div>

**Delegate**

Delegate是一个Protocol，其实我可以想象成一个虚拟类（只定义方法，不实现), 在这里delegate.h 遵守了UIApplicationDelegate

@interface iPhoneRadioAppDelegate : NSObject <UIApplicationDelegate> {  
UIWindow *window;  
SwitchViewController *switchViewController;  
}

这意味着delegate.m 可以实现UIApplicationDelegate的方法

delegate.m 中的代码

- (void)applicationDidFinishLaunching:(UIApplication *)application {  
[window addSubview:switchViewController.view];

// Configure and show the window  
[window makeKeyAndVisible];  
}

那applicationDidFinishLaunching顾名思义，就是application完成lanche之后， 我是否可以想象成UIApplication的一个Callback呢？

第一张图中，delegate的outlet了Window, Controller， File&#8217;s Owner, 那表示，Delegate实例可以引用这几个实例, 这行代码可以证明:

[window addSubview:switchViewController.view];

**Controller**

controller就是控制输出，当然包括对views的控制： 数据的处理（比如处理views中post【暂且理解用web app的方式理解】）数据，或者views如何controller要在views显示数据等等&#8230;

Tips: 

因为有些时候，需要自己定义controller或者delegate实例到MainWindow.xib中，但是

<div style="text-align:center;">
  <img src="http://blog.hellojessica.info/wp-content/uploads/2010/04/Screen-shot-2010-04-14-at-11.24.09-PM.png" alt="Screen shot 2010-04-14 at 11.24.09 PM.png" border="0" width="487" height="610" />
</div>

图中的outlet不会自动出现Delegate出现定义的outlet，那只能手动添加了，添加好之后，就可以在inspetor中看到这几个outlet， 然后手动点击圆圈拉到要链接的对象就可以了

<div style="text-align:center;">
  <img src="http://blog.hellojessica.info/wp-content/uploads/2010/04/Screen-shot-2010-04-14-at-11.26.45-PM.png" alt="Screen shot 2010-04-14 at 11.26.45 PM.png" border="0" width="289" height="159" />
</div>

* 文章比较混乱，只是为了理清自己的思绪，请不要转载，以免误认子弟

&#8211;EOF&#8211;

转载请注明：[韦旭红的点点滴滴][1] &raquo; [关于iPhone的outlet, delegate, window, file&#8217;s Owner的关系(本文逻辑有欠紧密，请不要随便转载，以免误人子弟)][2]

 [1]: http://www.weixuhong.com
 [2]: http://www.weixuhong.com/archives/476