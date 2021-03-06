---
title: "css文档流和盒模型"
date: 2020-01-21T20:13:11+08:00
draft: false
---

# 一、文档流

## （一）知识准备

1. 最新的 HTML5 已经不把元素一棒子打死的分为行内元素和块级元素了。因为任何元素都可以修改变成行内元素或者块级元素。当 display：inline 时，为行内元素；当 display：block 时，为块级元素。当 display：inline-block 时，为 inline-block 元素
2. 把纯文本文字当成一个行内元素
3. 别在 inline 元素中加 block 元素，不然你会晕倒。

## （二）流动方向

1. inline 元素从左到右，到达最右边才会换行，可能把一个元素从中间断开。

- 如果存在横滚动条，inline 元素只在在第一屏显示，拉动横滚动条会看见第一屏之外为空白

2. block 元素从上到下，每一个都另起一行。
3. inline-block 元素从左到右，但不会把一个元素从中间断开。

![图1](https://user-gold-cdn.xitu.io/2020/1/27/16fe5f339503de77?w=716&h=563&f=png&s=124381)

![图2](https://user-gold-cdn.xitu.io/2020/1/27/16fe6031550d684b?w=1916&h=593&f=png&s=192568)

## （三）宽度

1. inline 元素宽度为内部 inline 元素之和，不可用 width 指定。
2. block 元素默认自动计算宽度，**注意不是 100%**，而是能有多宽有多宽。可以用 width 指定（比如在标签里加上属性`sytle="width: 100px;"`）

- 注：只有极少数情况才可以吧 width 指定为 100%，所以一般别乱用 100%

3. inline-block 元素宽度为内部 inline 元素之和，可以用 width 指定。

![图3](https://user-gold-cdn.xitu.io/2020/1/27/16fe614c9086121f?w=1920&h=622&f=png&s=208334)

## （四）高度

1. inline 元素的（实际）高度由 line-height（行高）间接确定，不能用 height 指定。

- 用了间接是因为有时候改变了字体会把设置好的行高改变一点，具体参考[文章](https://zhuanlan.zhihu.com/p/25808995)。
- 如果给 inline 元素加上了内边距 padding，改变的只是可视高度，不是这个 inline 元素的实际高度。
- 如图 4

2. block 元素的高度由内部文档流元素决定，可以用 height 指定.如图 5
3. inline-block 元素的高度由内部文档流元素决定，可以用 height 指定

![图4](https://user-gold-cdn.xitu.io/2020/1/27/16fe6267b55604b6?w=1920&h=601&f=png&s=114207)
图 4

![图5](https://user-gold-cdn.xitu.io/2020/1/27/16fe638ab2b11b18?w=1920&h=732&f=png&s=241526)
图 5

## （五）overflow 溢出

### 1.定义

当内容的高度或宽度大于容器的高度或宽度，内容就会溢出。如图 6

![图6](https://user-gold-cdn.xitu.io/2020/1/27/16fe6450b1020da1?w=1920&h=614&f=png&s=102605)
图 6

### 2.用 overflow 来设置是否显示滚动条

（1） auto：灵活设置，超过才有滚动条

（2） scroll：一直显示滚动条

（3）hidden：直接隐藏溢出部分

（4）overflow：直接显示溢出部分
![](https://user-gold-cdn.xitu.io/2020/1/27/16fe64f8c067a07a?w=1920&h=869&f=png&s=188846)

## （六）脱离文档流

### 1.概念

有些元素可以不在文档流中，这时 block 元素高度就不会把这些元素计入其中。

### 2. 脱离文档流的方法

- 方法一：`position: absolute`
- 方法二：`float:left or right or both`

![](https://user-gold-cdn.xitu.io/2020/1/27/16fe6aee165a1d71?w=1920&h=443&f=png&s=110999)

![](https://user-gold-cdn.xitu.io/2020/1/27/16fe6aa074671305?w=1920&h=443&f=png&s=112499)

# 二、盒模型

## （一）定义

### 1.元素

- margin：外边距
- border：边框
- padding：内边距
- content：内容
- width：宽度

### 2.盒模型共分两种

#### （1）content-box（内容盒）

- 内容就是盒子的边界
- content-box width=内容宽度

#### （2）border-box (边框盒)

- 边框才是盒子的边界
- border-box width=内容宽度+padding+border
- border-box 更好用
  ![](https://user-gold-cdn.xitu.io/2020/1/27/16fe6e1fb1641c48?w=1242&h=704&f=png&s=313222)

![](https://user-gold-cdn.xitu.io/2020/1/27/16fe6e9a7263e1de?w=1920&h=503&f=png&s=110168)

### 3.可从开发者工具中看到盒模型的尺寸

打开开发者工具 → 点击左上角的指针 → 点击要查看的盒模型 → 在 Style 中即可看见

![](https://user-gold-cdn.xitu.io/2020/1/27/16fe6e834a85584e?w=1920&h=863&f=png&s=177168)

## （二）margin 合并(只有上下合并)

### 1.兄弟 margin 合并

#### （1）举例

将第一个子 div 的下外边距设为 30 像素，第二个子 div 的上外边距设为 30 像素，而最终两个子 div 之间只有 30px 的外边距，如下图，这种情况就为**兄弟合并**。**这是个好现象！**
![](https://user-gold-cdn.xitu.io/2020/1/27/16fe701e1e6cdbd5?w=1901&h=779&f=jpeg&s=230663)
![](https://user-gold-cdn.xitu.io/2020/1/27/16fe701f14bb438d?w=1919&h=795&f=jpeg&s=243374)

#### （2）消除兄弟合并现象

在兄弟元素中添加以下代码

```
width: 100%;  #可有可不有，不有时需要多写几个兄弟
display: inline-block； #把兄弟元素设为inline-block元素
```

![](https://user-gold-cdn.xitu.io/2020/1/27/16fe70e0aea9b24a?w=1919&h=854&f=jpeg&s=242110)
![](https://user-gold-cdn.xitu.io/2020/1/27/16fe70e1f28bc584?w=1919&h=831&f=jpeg&s=237598)

### 2.父子 margin 合并

#### （1）举例

第一个子元素和最后一个子元素的 margin 会和父元素的 margin 合并

![](https://user-gold-cdn.xitu.io/2020/1/27/16fe71efd11d9499?w=1874&h=796&f=jpeg&s=228491)
![](https://user-gold-cdn.xitu.io/2020/1/27/16fe71f0a92fa7a9?w=1901&h=836&f=jpeg&s=248915)
![](https://user-gold-cdn.xitu.io/2020/1/27/16fe71f13f30597b?w=1920&h=795&f=jpeg&s=250042)

##### （2）消除父子合并的方法

在父级元素中加上

- 方法一：`border: 2px solid blue;`
  ![](https://user-gold-cdn.xitu.io/2020/1/27/16fe72e93fa34dff?w=1919&h=659&f=png&s=142745)
- 方法二：`padding-top: 1px;`
  ![](https://user-gold-cdn.xitu.io/2020/1/27/16fe72eae1946c4a?w=1920&h=626&f=png&s=139433)
- 方法三：`overflow: hidden;`
  ![](https://user-gold-cdn.xitu.io/2020/1/27/16fe72ebb490e020?w=1920&h=639&f=png&s=139677)

# 三、基本单位

## 1.长度单位

（1）px：像素

（2）em：相对于自身 font-size 的倍数

（3）百分数

（4）整数

（5）rem

（6）vw 和 vh

- 具体哪个元素可以使用哪些长度单位，需要使用 MDN 搜索
