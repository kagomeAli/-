# 带你理解BFC原理

## 常见定位方案
在讲BFC之前，我们先了解一下常见的定位，定位方案是控制元素的布局，有三种常见的方案：

1. 普通流

> 在普通流中，元素按照其在HTML中的先后位置至上而下布局，在这个过程中，行内元素水平排列，直到当行被占满然后换行，块级元素则会被渲染为完整的一个新行，除非另外指定，否则所有元素默认普通流定位，也可以说，普通流中元素的位置由该元素在HTML文档中的位置决定。

 2. 浮动
> 在浮动布局中，元素首先按照普通流的位置出现，然后根据浮动的方向尽可能的向左边或右边偏移。

 3. 绝对定位
> 在绝对定位布局中，元素会整体脱离普通流，因此绝对定位元素不会对其兄弟元素造成影响，而元素具体的位置由绝对定位的坐标决定

## 二、BFC慨念
**Formatting context（格式化上下文）**是CSS2.1规范中的一个概念，它是页面中的一块渲染区域，并且有一套渲染规则，它决定了其子元素将如何定位，以及和其他元素的关系和相互作用。

那么BFC？？？？？

BFC（Block Formatting Contexts）块级格式上下文，输入上述定位方案的普通流。

**具有BFC特性的元素可以看作是隔离了的独立容器，容器里面的元素不会在布局上影响到外面的元素，并且BFC具有普通容器所没有的一些特性**

可以把BFC理解为一个封闭的大箱子，箱子内部的元素无论如何如何翻江倒海，都不会影响到外部。

## 三、触发BFC
只要元素满足下面任一条件即可触发BFC特性

1. body根元素
2. 浮动元素：float除none以外的值
3. 绝对定位元素：position（absolute、fixed）
4. display为inline-block、table-cells、flex
5. overflow除了visible以外的值（hidden、auto、scroll）

## 四、BFC特性及应用
### 1、同一个BFC下外边距会发生折叠

```
<head>
    <meta charset="UTF-8">
    <title>BFC</title>
    <style>
        .foldMargin{
            width: 100px;
            height: 100px;
            background: lightcyan;
            margin: 100px;
        }
    </style>
</head>
<body>
    <div class="foldMargin"></div>
    <div class="foldMargin"></div>
</body>
```
![image](https://user-images.githubusercontent.com/20856598/39188314-14c5f484-4802-11e8-9aa9-413c3eec93bd.png)

从效果上看，因为两个div元素都处于同一个BFC容器下（这里指body元素）所以第一个div的下边距和第二个div的上边距发生了重叠，所以两个盒子之间距离只有100px，而不是200px

首先这不是css的bug，我们可以理解为一种规范，如果想要避免外边距的重叠，可以将其放放在不同的BFC容器中。

首先这不是CSS的bug，我们可以理解一种规范，如果想要避免外边距的重叠，可以将其放在不同的BFC容器中。。


### 2. BFC可以包含浮动的元素（清楚浮动）
我们都知道，浮动的元素会脱离普通文档流，来看下面一个例子
```
<div style="border: 1px solid #000;">
    <div style="width: 100px;height: 100px;background: #eee;float: left;"></div>
</div>

```
![image](https://pic2.zhimg.com/80/v2-371eb702274af831df909b2c55d6a14b_hd.jpg)

由于容器内元素浮动，脱离了文档流，所以容器只剩下 2px 的边距高度。如果使触发容器的 BFC，那么容器将会包裹着浮动元素。
```
<div style="border: 1px solid #000;overflow: hidden">
    <div style="width: 100px;height: 100px;background: #eee;float: left;"></div>
</div>
```
效果如图：
![image](https://pic2.zhimg.com/80/v2-cc8365db5c9cc5ca003ce9afe88592e7_hd.jpg)

### 3.  BFC 可以阻止元素被浮动元素覆盖

![image](https://user-images.githubusercontent.com/20856598/39192048-e7567178-480a-11e8-857c-bd62d1522538.png)


```
 .borderLine{
            border: 1px solid #000;
        }
        .floatBox{
            width:100px;
            height: 100px;
            background: deepskyblue;
            float: left;
        }
```

```
        .overflowHidden{
            overflow: hidden;
        }
```

![image](https://user-images.githubusercontent.com/20856598/39190563-6fadf112-4807-11e8-8088-018b716548fd.png)

 这时候其实第二个元素有部分被浮动元素所覆盖（但文本信息不回被浮动元素所覆盖）如果想避免元素被覆盖，可触发第二个元素的BFC特性，在第二个元素中加入overflow：hidden，就会变成

```
    <div class="borderLine overflowHidden">
        <div class="floatBox">
            我是一个浮动元素
        </div>
        <div class="overflowHidden">
            我是浮动元素的父级父级的给子集的你，你到底懂不懂父爱如山，给爸爸妈妈打个电话吧孩子
        </div>
    </div>
```
![image](https://user-images.githubusercontent.com/20856598/39196505-e2c200be-4814-11e8-8982-f98e10783c6f.png)


这样的方法可以用来实现两列自适应布局



