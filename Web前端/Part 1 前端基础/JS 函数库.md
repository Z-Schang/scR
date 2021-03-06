****

#### Math

~~~javascript
var min=Math.min(1,2,3,4);
var max=Math.max(1,2,23,44);
var num=Math.ceil(89.99);//90，向上取整
var num=Math.floor(89.99);//89，向下取整
var num=Math.round(89.45);//89，四舍五入
var num=Math.abs(-55);//55，绝对值
var ran = Math.random();//随机数生成 [0，1）

//应用：
//1. 生成n~m的随机数
   function get(n,m){
   	var c = m - n + 1;
   	return Math.floor(Math.random() * c + n)
   }
//2. 随机生成十个数，放入数组
   var Arr=[];	//定义数组
   for(var i=0;i<10;i++)
   {
   	Arr[i]=Math.round(Math.random()*101);
   }
//3. 生成1~9随机数
   var j=Math.floor(Math.random()*9+1);

~~~

****

#### Date

~~~javascript
var today=new Date(),			//当前时间
    year=today.getFullYear(),	//年份  
	month=today.getMonth()+1,	//月份(必须加一)
	date=today.getDate(),	//日期
	week=today.getDay(),	//星期X (0~6，用weeks[week] 可以完成大写操作)
	hour=today.getHours(),			//小时
  	min=today.getMinutes(),			//分钟
  	sec=today.getSeconds();			//毫秒

// 50天后星期几？
today.setDate(today.getDate()+50);
document.write(today.getDay());
~~~

****

#### 定时器

- setInterval 是 window 上的方法
- 若 2000 改为自定义time，只识别一次，不可改变
- 每次 setInterval 都新建一个定时器，唯一标识
- 内存状态会影响定时器

~~~
setInterval(function(){}, 1000);
setTimeout(function(){}, 1000);
clearInterval()
clearTimeout()
~~~

~~~javascript
// 10分钟闹钟
var date = new Date();
date.setMinutes(10);
setInterval(function(){
    if(new Date().getTime() - date.getTime() > 1000)
        console.log("10分钟过去了");
}, 1000);
~~~

****

#### 正则表达式

- 正则表达式是匹配特殊字符串或有特殊搭配原则字符的最佳选择

~~~javascript
语句：
reg.text(str);//str字符串是否满足reg正则的规则
str.match(reg);//找出str中满足reg正则的集合类数组

创建：
var reg = new RegExp("abc", "i");
// 或：
var reg = new RegExp(/abc/i);

大规则：
/i：忽略大小写属性(ignore)
/g：全局匹配(global)
/m：多行匹配(mult)
实例：
var reg = /[0-9A-z]/g;//任选1位
var reg = /(abc|def)[0-9]/g;//全局匹配以 abc/def 开头拼接数字的串

小规则：
\w：[0-9A-z]word
\d：[0-9]dig
\s：[\t\n\r\v\f] 空格 space
实例：
var reg = new RegExp(/\bcde/g);	
var str = "abc cde fgh";
str.match(reg);

~~~

