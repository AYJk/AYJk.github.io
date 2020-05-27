---
layout:     post
title:      "Flutter 解决键盘遮挡Dialog输入框问题"
subtitle:   " \"初学Flutter\""
date:       2020-05-27 10:47:00
author:     "香蕉Dark"
header-img: "img/home-bg-o.jpg"
catalog: true
tags:
    - Flutter
---


# 正文

很多需求中会出现点击按钮之后，弹出一个带TextField的Dialog，一般情况下我们的Dialog位置都是固定的，所以当键盘弹出的时候就可能遮挡到Dialog的部分内容。

解决方案就是在Dialog这个Widget外面套一层`AnimatedContainer`，当键盘弹出的时候通过动画进行位移。

位移的距离可以通过如下代码获得：

``` dart
var mediaQuery = MediaQuery.of(context);
var insetBottom = mediaQuery.viewInsets.bottom
```

当然，我们需要往y轴负方向位移，对应的值就需要`* -1`。

主要代码如下：

``` dart
AnimatedContainer(
    duration: Duration(milliseconds: 250),
    curve: Curves.easeInOut,
    transform: Matrix4.translationValues(
                    0,
                    mediaQuery.viewInsets.bottom * -1,
                    0,
                ),
    child:...,
)
```

# 最终实现效果

![效果图](/img/in-post/Flutter解决键盘遮挡Dialog输入框问题/Xnip2020-05-27_10-01-57.png)