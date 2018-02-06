## 1. CSS属性是否区分大小写？
不区分。（HTML, CSS都不区分，但为了更好的可读性和团队协作，一般都小写，而在XHTML 中元素名称和属性是必须小写的。）

#

## 2.如果设置<p>的font-size: 10rem;那么当用户重置或拖拽浏览器窗口时，它的文本会不会受到影响？
不会，rem是css3新增的一个相对单位（root em）；这个单位引起了广度关注，使用rem为元素设定字体大小时，仍然是相对大小，单相对的只是html根元素



**rem 跟 em 的区别**


> EM 是字体排印的一个单位，等同于当前指定的point-size
意思是如果存在一个选择器font-size属性的值为20px，那么1em=20px

```
h1 { 
   font-size: 2em; /* 1em = 16px */ 
    margin-bottom: 1em; /* 1em = 32px */
 }

p { 
    font-size: 1em; /* 1em = 16px */ 
    margin-bottom: 1em; /* 1em = 16px */
 }

```
很吃惊两种状况下的margin-bottom的1em值不同？

这种现象的发生在于1em等同于它当前的font-size。因为<h1>中的font-size被设置为了2em。其他用在<h1>内的em来计算的属性，就为1em = 32px。


> 什么是rem
rem是指**根em**，而不是当前的font-size大小。产生是为了帮助解决em所带来的计算问题

                


## 3. 

伪类选择器:checked将作用与input类型为radio或者checkbox, 不会作用于option？

答：不对。

可以作用于option，试了下感觉并没有什么用，虽然能选中，但是这个不能改变其中的属性。对option有效，对input无效

```
<style>  
    option:checked {
      color: red;
    }
    input:checked {
      background: red;
    }
  </style> 

<div>
  <select>
    <option>Volvo</option>
    <option selected="selected">Saab</option>
    <option>Mercedes</option>
    <option>Audi</option>
  </select>
  <br>
  <br>
  <input type="radio" name="sex" value="male" checked>Male
  <br>
  <input type="radio" name="sex" value="female">Female
</div>
```
![image](https://user-images.githubusercontent.com/20856598/35787742-6fcbbdca-0a6b-11e8-9793-dc653452bd2f.png)

#

## 4. screen关键词是指设备的物理屏幕大小还是指浏览器的视窗。

答：浏览器的视窗。

# 

## 5.overfloa:hidden 是否形成新的块级格式化上下文？

答：会
**形成 BFC 的条件** 
1、浮动元素，float 除 none 以外的值； 
2、绝对定位元素，position（absolute，fixed）； 
3、display 为以下其中之一的值 inline-blocks，table-cells，table-captions； 
4、overflow 除了 visible 以外的值（hidden，auto，scroll）
**它决定了其子元素将如何定位，以及和其他元素的关系和相互作用。**

## 5.1 清除浮动
1. 父级div定义height
原理：父级div手动定义height，就解决了父级div无法自动获取到高度的问题。 
优点：简单、代码少、容易掌握 
缺点：只适合高度固定的布局，要给出精确的高度，如果高度和父级div不一样时，会产生问题 

2.结尾处添加空div标签 clear：both
原理：添加一个空div，利用css提供的clear:both清除浮动，让父级div能自动获取到高度 
优点：简单、代码少、浏览器支持好、不容易出现怪问题 
缺点：不少初学者不理解原理；如果页面浮动布局多，就要增加很多空div，让人感觉很不好 

3.父级div定义伪类：after和zoom
.clearfloat:after{
   display:block;
   clear:both;
   content:"";
   visibility:hidden;
   height:0
} 
.clearfloat{
     zoom:1
} 
原理：IE8以上和非IE浏览器才支持:after，原理和方法2有点类似，zoom(IE转有属性)可解决ie6,ie7浮动问题 
优点：浏览器支持好、不容易出现怪问题（目前：大型网站都有使用，如：腾迅，网易，新浪等等） 
缺点：代码多、不少初学者不理解原理，要两句代码结合使用才能让主流浏览器都支持。

4.父级div定义overflow：hidden，定义width或zoom:1
原理：必须定义width或zoom:1，同时不能定义height，使用overflow:hidden时，浏览器会自动检查浮动区域的高度 
优点：简单、代码少、浏览器支持好 
缺点：不能和position配合使用，因为超出的尺寸的会被隐藏。 
建议：只推荐没有使用position或对overflow:hidden理解比较深的朋友使用。 

5.父级div定义overflow：auto，定义width或zoom:1
原理：必须定义width或zoom:1，同时不能定义height，使用overflow:auto时，浏览器会自动检查浮动区域的高度 
优点：简单、代码少、浏览器支持好 
缺点：内部宽高超过父级div时，会出现滚动条。 

6.父级一起浮动
原理：所有代码一起浮动，就变成了一个整体 
优点：没有优点 
缺点：会产生新的浮动问题。 

#

## 6.渐进增强和优雅降级之间的不同
渐进增强：针对低版本浏览器进行构建页面，保证最基本的功能，再增对高版本浏览器进行效果、交互等改进和追加功能达到更好的用户体验
优雅降级：一开始就构建完整的功能，然后在针对低版本浏览器进行兼容

区别：优雅降级是从复杂的现状开始，并试图减少用户体验的供给，而渐进增强则是从一个非常基础的，能够起作用的版本开始，不断扩充，以适应未来环境的需要


## 7.知道css有个content属性吗？有什么作用？有什么应用？
能够实现页面中的内容插入。用来和:after及:before伪元素一起使用，在对象前或后显示内容。

1.生成内容
2.使用计数器创建号码内容


## 8.伪类和微元素的区别
伪类还是伪元素都属于CSS选择器的范畴，
根本区别：是否创造了新元素 
如果需要添加新元素加以标识的，就是伪元素，反之，如果只需要在既有元素上添加类别的，就是伪类。而这也是为什么，标准精确地使用 “create” 一词来解释伪元素，而使用 “classify” 一词来解释伪类的原因。一个描述的是新创建出来的“幽灵”元素，另一个则是描述已经存在的符合“幽灵”类别的元素

## 9.css 的引入方式

- [ ] 外部样式表
- [ ] 内部样式表
- [ ] 内联样式
- [ ] 导入样式

link跟@import的区别
@import只能加载css，link还可以定义rel连接属性
link引入的css会跟页面一起加载，import引入的css要等页面全部下载完成后加载
@import只有ie5以上才能识别，link没限制
js控制dom修改样式只能使用link标签
import可以在css中再次引用

**不要使用@import**
影响浏览器的并行下载
多个@import导致下载顺序紊乱





