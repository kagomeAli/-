# Flex的相关属性

## 1、简介
Flex是Flexible Box的缩写，意为“弹性布局”，用来为盒子模型提供最大灵活性。
Flex是它可以简单、完整、响应式的实现各种网页布局，目前已经得到大多数主流浏览器的支持。

##/2、基本概念

- flex container：采用Flex布局的元素，即父元素，称为**Flex容器**，简称容器。
- flex item：父元素内包含的子元素，称为**flex项目**。
- Flex是没有方向之分的，在Flex容器中默认存在两根轴，水平的**轴为主轴（main axis）**，垂直的轴为**侧轴（cross axis）**。
- 主轴的开始位置叫做main start，结束位置叫做main end。
- 侧轴的开始位置叫做cross start，结束位置叫做cross end。
- 项目默许沿主轴方向排列，单个项目占的主轴空间叫做main size，侧轴叫做cross size。

概念的图片解析：
![image](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071004.png)

**注意：设为flex布局后，子元素的float、clear、vertical-align属性将失效**

#

##/3、容器(父元素)的属性

容器共有六个属性：

- flex-direction
- flex-wrap
- flex-flow
- justify-content
- align-items
- align-content

### 3.1 flex-direction属性
flex-direction属性决定主轴的方向，它可能有四个值

- row：默认值，主轴为水平方向，起点在左端
- row-reverse：主轴为水平方向，起点在右端
- column：主轴为垂直方向，起点在上端
- column-reverse：主轴在垂直方向，起点在下端

四个值对应如图：

![image](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071005.png)

### 3.2 flex-wrap属性
flex-wrap属性决定项目在一行排不了的情况下是否换行。

nowrap：默认值，不换行
![image](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071007.png)

wrap：换行，第一行在主轴**开始方向**，一次往主轴结束方向布置。
![image](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071008.jpg)

wrap-reverse：换行，第一行在主轴**结束方向**，依次往主轴结束方向布置
![image](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071009.jpg)

#

### 3.3 flex-flow
属性是flex-direction和flex-wrap的简写形式，默认值为row nowrap

### 3.4 justify-content属性
justify-content属性定义了项目在主轴上的对齐方式

- flex-start：默认值，主轴开始方向对齐，
- flex-end：主轴结束方向对齐
- center：主轴居中对齐
- space-between：两端对齐，项目之间的间隔相等
- space-around：每个项目两侧的间隔相等，所以项目之间间隔是项目与边框间隔的两倍

![image](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071010.png)

### 3.5 align-items属性
align-items属性定义了每个行项目上在侧轴的对齐方式

- flex-start：侧轴的开始方向对齐。
- flex-end：侧轴的结束方向对齐
- center：侧轴居中对齐
- baseline：项目的第一行文字的基线对齐。
- strecth：默认值，如果项目未设置高度或高度设为auto，将占满整个容器

![image](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071011.png)

### 3.6 align-content属性定义了在容器侧轴上还有额外空间时，如何排布每一行（当容器只有一行时，他不起作用）

- flex-start：侧轴开始方向对齐。
- flex-end：侧轴结束方向对齐
- center：侧轴中心对齐
- space-between：与侧轴两端对齐，每行轴线间隔平均
- space-around：每根轴两侧间隔相等
- strecth：默认值，占满整个侧轴

![image](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071012.png)

#

## 4、项目（子元素）的属性
项目共有6个属性

- order
- flex-grow
- flex-shrink
- flex-basis
- flex
- align-self

### 4.1 order属性
order属性定义项目的排列顺序，数值越小排列越靠前，默认值为0，可以是任意整数

![image](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071013.png)


### 4.2 flex-grow
flex-grow属性定义项目的放大比例，默认为0，即如果存在剩余空间也不放大。

如果所有的项目的flex-grow属性都为1，则它们将等分剩余空间，如果有一个项目的flex-grow属性为2，其他项目都为1，则前者占据的剩余空间比其他的空间多一倍
![image](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071014.png)

### 4.3 flex-shrink
flex-shrink属性定义了项目的缩小比例，默认为1，即如果空间不足时，该项目将缩小。

负值对该属性无效，即该属性可能的值为0或正整数。

如果所有项目的flex-shrink属性都为1，当空间不足时，都将等比例缩小。
**如果一个项目的flex-shrink属性为0**，其他项目都为1，则空间不足时，前者不缩小

![image](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071015.jpg)

### 4.4 flex-basis
flex-basis属性定义了在分配多余空间之前，项目占据的主轴空间的大小。浏览器根据这个属性，计算主轴是否有多余的空间。它的默认值为auto，即项目的本来大小。
它可以设为跟width或height属性一样的值（比如350px），则项目将占据固定空间。

### 4.5 flex属性
flex属性是flex-grow、flex-shrink、flex-basis的简写。
默认值：0 1 auto。后面两个属性可选

该属性有两个快捷值: auto （1,1，auto）和 none （0,0 ，auto）

建议优先使用这个属性，而不是单独写三个分离的属性，因为浏览器会推算相关值。

### 4.6 align-self属性
align-self属性允许单个项目有与其他项目不一样的侧轴对齐方式，可覆盖align-items属性。
默认值为auto，表示继承父元素的align-items属性，如果没有父元素，则等同于strecth

