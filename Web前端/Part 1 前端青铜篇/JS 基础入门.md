#### JS 七种数据类型

- 基本类
  - Undefined
  - Null
  - Boolean
  - Number
  - String
  - Symbol 【 ES6 新增的一种原始数据类型，它的字面意思是：符号、标记。代表独一无二的值 】
- 引用类
  - Object 【本质：一组无序的名值对组成的】

衍生：typeof 返回值

- string、number、boolean、undefined、object、function

- null 是 object “空对象”

  null==undefined   true

  null===undefined  false



#### 数据类型转换

- 将字符转为数值：

  var X=parseInt(“28px”);	//必须以数字开头

  console.log(X)	==> 28	

  var Y=parseFloat(“58.6.3px”)		//必须以数字开头

  console.log(Y) ==> 58.6

- 将str转化为字符串

  str.toString()

  var b=ids.toString();

  var a=89;

  console.log(String(a)); ==> string

- 数字转布尔值

  除空格,0,null,未定义以外数字字符的boolean都为true

  NaN 与其他数值进行比较的结果总是不相等的，包括它自身在内。因此，不能用 Number.NaN 比较来检测一个值是不是数字，而只能调用 isNaN() 来比较。while(k!=NaN) 判断是否为数字



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

var today=new Date(),				//当前时间

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