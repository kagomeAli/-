# wepy  的深入理解

[小程序的概述](https://mp.weixin.qq.com/s/9PID6UJsQyB06xdyOkEVOA)
#


# 预先加载
 原理：传统的H5中也可以通过预加载来提升用户体验，但在小程序中做到这一点会更加容易一点

传统的H5在启动时，page1.html只会加载page1.html的页面个逻辑代码，当page1.html跳转到page2.html时，page1.html的javascript数据将会从内存中消失。page1.html与page2.html之间的数据通信只能通过URL参数传递或者浏览器的cookie，localStorage存储处理。


小程序在启动时，会直接加载所有页面逻辑代码进内存，即便page2可能不会被使用。在page1.html跳转至page2.html时，page1所有的javascript数据也不会从内存中消失，page2甚至可以直接访问page1中的数据

针对传统H5，小程序的优化：
 1.预加载数据
preload

2.预查询数据
 page1.html 页面的跳转到page2.html的方式改为：wepy.redirect（url）
page2.html在加载页面的时候会调用页面中的一个生命周期函数 onPrefetch（）

预查询数据示例：

```
// page1.wpy 使用封装的 redirect 方法跳转时，会调用 page2 的 onPrefetch 方法
methods: {
  tap () {
    this.$redirect('./page2');
  }
}

// page2.wpy 直接从参数中拿到 onPrefetch 中返回的数据
onPrefetch () {
  return api.getBigList();
}
onLoad (params, data) {
  data.prefetch.then((list) => render(list));
}
```


# 数据绑定

原理;

在针对数据绑定做优化时，需要先了解小程序的运行机制。因为视图层与逻辑层的完全分离，所以通信完全依赖于WeixinJSBridge。

setData操作时机就是js逻辑层与页面渲染之间的通信，
运行的流程如下
![image](https://user-images.githubusercontent.com/20856598/36659455-7eb793d6-1b0f-11e8-9f0f-f39be00fb4fb.png)

当一个数据变化时，小程序不单单只处理传递的数据，而是处理当前页面的所有data数据，所以setData的开销是非常大的，以及减少setData

**最优绑定**：在内存中添加完毕后最后执行setData操作。
**最差绑定**：在添加一条记录执行一次setData操作。
**最智能绑定**：不管中间进行了什么操作，在运行结束时执行一次脏检查，对需要设置的数据进行setData操作。

## 优化：
WePY选择使用脏检查去做数据优化，只会在流程最后做一次脏检查，并且按需执行setData



#  wepy如何实现单文件组件wepy组件.wpy编译
wepy框架通过wepy-cli对.wpy编译，拆解为style、script、template，再分别处理，生成到dist文件对应的xxx.wxss、xxx.wxml......

# 如何隔离组件作用域
通过组件在不同page的命名作为前缀，并以父级为起点，依次为$child，再子寄就是$child$child，依次类推。
不同组件在不同的component实例下，data set到page就是带上前缀，同样的method也是加上前缀在Page（{}）中

# 如何实现组件通信
 通过编译获取component的路径注入代码，在小程序运行时，根据逐层require获取对应的new component 并记下父级$parent ，构建组件树。

如何向子组件传递props和events？
编译时就会手机在template中传入的props和events注入到代码中的$props和$events，然后子组件init的时候获取父级$parent的$props并加入前缀$prefix去setData（_子组件的在page中的元素表现已经在编译的时候被替换成了$prefix$data的样子_），这样实现了传值，调用$emit触发父组件event，直接寻找福建的$parent apply调用相应的方法


# 如何实现加载外部npm包
wepy-cli在处理script部分，根据require的内容判断是否是npm内容或者带有npm标识，如果是require('xxx') require('xxx/yyy')的形式获取package.json中的main部分找到引用文件，就去compile该文件（带上npm标识继续去resolveDeps），如果判断不是npm内容修正require即可，带有npm标识最后会打包到npm文件夹。













