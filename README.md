#技术详述
一开始大家都会觉得做一个Android外挂会汲取很多东西或者底层的东西,但当发现Android里有一个叫AccessibilityService的服务时，一切都变得很简单。

关于AccessibilityService

先看看官网的介绍Accessibility
Many Android users have different abilities that require them to interact with their Android devices in different ways. These include users who have visual, physical or age-related limitations that prevent them from fully seeing or using a touchscreen, and users with hearing loss who may not be able to perceive audible information and alerts...

Android官网详解accessibility

上面大概的意思就是Accessibility是一个辅助服务，主要是面向一些使用Android手机的用户有相关障碍(年龄、视觉、听力、身体等)，这个功能可以更容易使用手机，可以帮用户在点击屏幕或者显示方面得到帮助等等。接下来就是查找相关API，看能做到哪个地步。

Accessibility相关API描述

当然accessibility除了可以辅助点击界面的事件外，还可以用作自动化测试，或者一键返回，是一个非常强大与实用的功能，具体实例可以看我另一个App虚拟按键助手 请往下载 GooglePlay市场 或 应用宝。

关于抢红包的流程

在有以上的一些关于辅助服务的基础知识后，我们就可以分析怎样自动化抢红包。 大家使用过微信都知道，如果不是在微信的可见界面范围（在桌面或者在使用其它应用时），在收到新的消息，就会在通知栏提醒用户。而在微信的消息列表界面，就不会弹出通知栏，所以可以区分这两种情况。然后抓取相关关键字作进一步处理。

1、在非微信消息列表界面，收到通知消息的事件，判断通知栏里的文本是否有[微信红包]的关键字，有则可以判断为用户收到红包的消息(当然，你可以故意发一条包括这个关键字的文本消息去整蛊你的朋友)。然后，我们就自动化触发这个消息的意图事件(Intent);

2、在通知栏跳进微信界面后，是去到com.tencent.mm.ui.LauncherUI这个Activity界面。我们知道，红包的消息上，包括了关键字领取红包或者View的id，那我们就根据这个关键字找到相应的View，然后再触发ACTION_CLICK(点击事件);

3、在点击红包后，会跳到com.tencent.mm.plugin.luckymoney.ui.LuckyMoneyReceiveUI这个拆红包的Activity,当然老方法，找关键字拆红包或id,然后触发自动化点击事件。

这样就可以完成整个自动化完成抢红包的流程了,所以核心就是找关键字，然后模拟用户点击事件，就这么简单
