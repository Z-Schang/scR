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

6. **数组、对象、字符串的方法和各之间的转换**

   类数组转为数组：

   ~~~javascript
   [].slice.call(document.getElementsByTagName("li"));
   ~~~

   数组的方法：

   ~~~javascript
   var personArr = [
       {name: 'ZSC', src: 'www.sc.com', des: 'The School', sex: 'male', age: 23},
       {name: 'ZYY', src: 'www.yy.com', des: 'The School', sex: 'female', age: 23},
       {name: 'LYF', src: 'www.ss.com', des: 'The School', sex: 'male', age: 22}
   ];
   
   // forEach：为一个数组集每一项操作【循环遍历作用】
   var obj = {name: 'specil'}
   personArr.forEach(function(ele, index, self){
       li[index].innerText = ele.name;//li中被赋予ZSC、ZYY、SS
       li2[index].innerText = this.name;//li中被赋予specil * 3
   }, obj);
   
   // filter：数组过滤
   var obj1 = {name : 'zsc', sex : 'male'};
   function deal2(ele, index, self){
       return ele.sex == 'male'
   }
   var newArr = personArr.filter(deal2, obj1);
   console.log(newArr);//personArr中sex为male的被筛选出来
   
   // map：映射作用，返回新数组
   var newArr = personArr.map(function(ele,index,self){
       ele.age += 20;
       return ele;
   }, obj2);//返回一个数组，和原来数组区别在于age +20
   
   // every: 判断元素是否都符合条件
   var flag = personArr.every(function(ele, index, self){
       return (ele.age > 18) ? true : false;
   },{name: 'zsc'})
   console.log(flag);//true
   
   // some: 判断是否有元素符合条件
   var flag = personArr.every(function(ele, index, self){
       return (ele.sex == "male") ? true : false;
   },{name: 'zsc'})
   console.log(flag);//true
   
   // reduce: 累加器，数组中的每个值（从左到右）开始缩减，最终计算为一个值。
   // total 初始值/上次计算结束后的返回值；currentValue 当前元素
   let arr = [1,2,3,4];
   var arr2 = arr.reduce((total, currentValue) => {
       return total + currentValue;
   }); //10
   var arr3 = arr.reduce((total, currentValue) => {
       return total + currentValue;
   }, 10);//20
   // 高级用法：
   var cookieStr = 'aa=123;bb=456;cc=789';
   function parseCookieStr(str){
   	var obj = {};
   	var cookieArr = str.split(';');//["aa=123", "bb=456", "cc=789"]
   	return cookieArr.reduce(function(prevValue, icurValue, index, self){
   		var arr = icurValue.split('=');
   		prevValue[arr[0]] = arr[1];
   		return prevValue;
   	}, obj);
   }
   console.log(parseCookieStr(cookieStr));//{aa:123, bb:456, cc:789}
   ~~~
