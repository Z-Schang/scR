#### Math

var min=Math.min(1,2,3,4);

var max=Math.max(1,2,23,44);

var num=Math.ceil(89.99);		//90，向上取整

var num=Math.floor(89.99);	//89，向下取整

var num=Math.round(89.45);	//89，四舍五入

var num=Math.abs(-55);		//55，绝对值

var ran = Math.random();		//随机数生成 [0，1）

应用：

1. 生成n~m的随机数

   function get(n,m){

   ​	var c = m - n + 1;

   ​	return Math.floor(Math.random() * c + n)

   }

2. 随机生成十个数，放入数组

   var Arr=[];	//定义数组

   for(var i=0;i<10;i++)

   {

   ​	Arr[i]=Math.round(Math.random()*101);

   }

3. 生成1~9随机数

   var j=Math.floor(Math.random()*9+1);



#### Date

​	var today=new Date(),				//当前时间

  	 year=today.getFullYear(),			//年份  

​	month=today.getMonth()+1,		//月份(必须加一)

​	date=today.getDate(),				//日期

​	week=today.getDay(),				//星期X (0~6，用weeks[week] 可以完成大写操作)

​	hour=today.getHours(),			//小时

  	min=today.getMinutes(),			//分钟

  	sec=today.getSeconds();			//毫秒

50天后星期几？

today.setDate(today.getDate()+50);

document.write(today.getDay());