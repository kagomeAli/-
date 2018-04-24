
# web安全    - > XSS攻防

#

# 1.XSS的定义
**跨站脚本攻击（cross site scripting**，恶意攻击者往Web页面里插入恶意Script代码，当用户浏览该页之时，嵌入里面的script代码会被执行，从而到达恶意攻击用户的目的

#2.XSS的原理

a.攻击者对含有漏洞的服务器发起XSS攻击（注入JS代码）

b.诱导受害者打开受到攻击的服务器URL

c.受害者在web浏览器中打开URL，恶意脚本执行

# 3. XSS的攻击方式

a.反射型：发出请求时，XSS出现在URL中，作为输入提交到服务器端，服务器端解析后响应，XSS随响应内容一起返回给浏览器，最后浏览器解析执行CSS代码，这个过程就像一次发射，所以叫做反射性XSS。

b.存储型：存储型XSS和反射性的XSS的区别就在于，存储型的XSS会存储在服务器端，下次请求目标页面时不再提交XSS代码

# 4.XSS的防御措施
a.编码：对用户输入的疏忽进行HTML Entity编码
![image](http://img.blog.csdn.net/20170418160547231?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvZ2FueWluZ3hpZTEyMzQ1Ng==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

b.过滤：移除用户上传的DOM属性，如onerror等，移除用户上传的style节点，script节点，iframe节点等

c.校正：避免直接对HTML Entity编码，使用DOM Prase转换，校正不配对的Dom标签