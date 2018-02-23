# web语义化，有什么好处
根据内容的结构化，选择合适的标签，便于开发者阅读和写出更优雅的代码，让浏览器的爬虫和机器更好的解析

好处：
1.有利于SEO，有助于爬虫抓取更多的有效信息，爬虫是依赖于标签来确定上下文和各个关键字的权重
2.语义化的HTML在没有css的情况下也能很好的呈现内容结构和代码结构
3.方便其他设备解析
4.便于团队开发和维护

# display：none 和visibility：hidden 的区别
联系：都让元素不可见

区别：
1.display：none 会让元素从渲染树中消失，渲染的时候不占任何空间，visibility：hidden不会让元素从渲染树种消失，元素继续占据空间，只是内容不可见
2.display：none是非继承属性，子孙节点消失由于元素从渲染树消失造成的，同过修改子孙节点属性无法显示；visibility：hidden；是继承属性，子孙节点消失是由于继承了hidden，通过设置visibility：visible可以显示
3.修改常规流元素的display通常会造成文档重排，修改visibility只会造成文本重绘
4.读屏器不会读取display：none元素内容；会读取visibility：hidden；元素内容

# css hack原理以及常用hack
原理：利用不同浏览器对css的支持与解析不一样而编写针对特定浏览器的样式。
常见的hack：
1.属性hack
2.选择器hack
3.IE条件注释
