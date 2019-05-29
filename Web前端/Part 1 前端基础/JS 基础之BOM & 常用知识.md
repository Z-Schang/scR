### BOM

****

- BOM的核心是window
- 组成：
  - Window浏览器窗口【JS的顶层对象】
  - Navigator浏览器信息
  - History 浏览器访问过的URL
  - Location 当前URL信息
  - Screen 客户端显示屏



### JS常用知识点

****

1. **浏览网页发生的事：**

   1. 输入网站，DNS解析IP地址
   2. DNS查看浏览器缓存、系统缓存路由器缓存，有无此IP
   3. 没有缓存则查询DNS服务器，返回IP地址
   4. 建立TCP连接，发送HTTP请求
   5. 接到响应后，下载html
   6. JS解析，即JS时间线过程
   7. 渲染到浏览器
   8. 关闭TCP连接

2. **浏览器的基本组成**

   1. 用户界面

   2. 浏览器引擎

   3. JS引擎

   4. 渲染引擎

   5. UI后端

   6. 数据存储

   7. 网络


3. **渲染过程(Model 渲染出图像)**

   1. 解析html构建DOM树
   2. CSS Rule树
   3. Render树

   渲染模式：

   1. 怪异模式

   2. 标准模式

   检测方法：document.compatMode();

   ​	BackCompat(混杂)		CSS1Compat(标准)


4. **特性/属性**

   - 属性包含特性和自定义属性

   - 特性是本来就存在的，无需定义

   - 特性与DOM对象一一映射关系

   - 属性与DOM对象无映射关系，设置不了DOM中自定义的属性，但可通过setAttribute()来设置

5. **图片预加载**

   ~~~javascript
   function prevLoad(dom, url){
       var yimg = new Image();
       yimg.onload = function(dom){
       	dom.appendChild(this);
   	}
   	yimg.src = url;
   }
   // 先使用懒加载，再使用预加载
   ~~~
