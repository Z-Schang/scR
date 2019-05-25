### 理论篇

****

#### CSS的构成

选择器 + 声明

~~~css
.a{
    color:orange
}
~~~



#### CSS双特性

继承性【家族继承王位】

层叠性【权力决定地位】



#### CSS使用方法

- 行内样式  <p style="color:red">  置于行间
- 内联样式  <style  type="text/css">...</style>  置于 head 标签中
- 外联样式  <link rel="stylesheet" href="css.css">  置于 head 标签中



#### CSS继承

子元素继承父元素计算后的值，不包括 em 和 %



#### CSS优先级

行内 > (内联 >= 外联) 理论上取决于引入顺序，但实际中 style 一般置于 link 后面

最高级：@import url("index.css");   置于内部样式 style 的第一行中

​		p{color:black !important;}



#### CSS样式权值

class：1

伪类：10

id：100

行内：1000



#### CSS选择器

- 全局【全家福】 *{}
- 群组【各个家庭】 a,b,c{}
- 后代【家有子孙】 a ason{}
- 伪类【家中宠物】 a:link{};  a:visit{};  a:hover{}  a:active{}
- 子代【所有儿子】M>N{}
- 兄弟【后面所有同级兄弟】M~N{}
- 相邻【后面某个相邻兄弟】M+N{}   （导航中 li + li 实现效果：    首页💗我们💗更多💗）
- 排斥【黑名单】input:not(#badman){}



#### CSS常用属性

**字体和文本**

~~~css
    font-family    			字体类型(微软雅黑，宋体，黑体...)
	font-size	   			字体大小(px, em)
    font-color/color     	字体颜色
	font-weight  			粗细(bold, bolder, 100~900)
	font-style	    		样式(normal, italic, oblique斜体)
	font-variant			变形(small-caps小型大写字母)
	vertical-align  		对行内元素垂直对齐起作用
		【值：top, baseline, textTop, middle, textBottom, bottom, +-(15px)/+-(xx%)】
	line-height				设置行高
	word-spacing 			单词间隙(空格判断)
	letter-spacing 			字母间隙
	text-transform			文本变化: capitalize(首字母大写) uppercase/lowercase(大小写)
	text-decoration			文本装饰:underline下划线 overline上划线 line-through删除线 										blink闪烁  none 全无
	text-indent				缩进文字
~~~

**列表和背景**

~~~css
背景系列：
background-color  	背景色
border:				边框 合并写法: 1px solid/dashed black;
background:			背景图片 #000 合并写法: url(img/pic.jpg) no-repeat fixed;	
		     repeat 重复，分为no-repeat不重复；repeat-x水平重复；repeat-y垂直重复
			 fixed滚动设置，分为fixed不滚动；scroll滚动(background-attachment的属性)

background-position:背景定位 center top bottom left right;	
opacity:			透明度设置 0 ~ 1;		
列表系列：
list-style-type:	列表项的样式选择
	无序列表值：disc实心圆	circle空心圆	square实心方块
	有序列表值：decimal数字	upper/lower-alpha	英文	upper/lower-roman罗马数字

list-style-image:	植入图片图标
list-style-position:定位图标位置 outside/inside
~~~

**常用系列**

~~~css
布局属性：display、position、float、clear
自身盒模型：width、height、padding、margin、border、overflow
文本属性：font、line-height、text-align、text-indent(缩进em)、vertical-align
装饰属性：color、background-color、opacity、cursor(pointer...)
~~~



#### CSS注释

~~~css
顶部注释
/*
*@description：说明
*@author：作者
*@update：更新时间
*/
模块注释
/*导航部分，开始*/
/*导航部分，结束*/
~~~



#### CSS盒子模型

~~~
H5的 !doctype 采用标准盒子模型(含外边距)
margin外填充
border边框，[width][color][style]	style分为solid\dotted\dashed
padding内填充	
	两值：上下，左右
	三值：上，左右，下
	四值：上，右，下，左 (顺时针)
width内容宽度
height内容高度
display：inline;(块级元素行内化) 
		 block;(行内元素块级化)
		 inline-block;(行内块元素)
行内元素没有上下外边距。
还有混杂盒模型，将在黄金段位揭晓

💗 inline-block 元素间默认有边距，去除方法是在父级添加 font-size:0
	几个 img 一起时同理，用font-size:0 去除制表符
~~~



#### CSS定位

~~~
position:
	static 自然定位：免疫top/bottm控制
	relative相对定位：不离开常规流，可使浮动元素发生偏移
	absolute绝对定位：离开常规流。
	fixed固定定位：不随窗口移动而移动
浮动处理：
.cont{		【置于父元素！】
	overflow:hidden;
	zoom:1;
}
.clear{		【置于与后面元素之间】
	clear:both;
}
~~~



#### 几个重要概念

~~~css
1）包含块
	父于子是相对的，儿子不是所有人的儿子，相对他亲生父亲才是儿子
2）层叠上下文	
	背景边框是装饰属性，层叠级别低；	【就像店门口玻璃的贴纸】
	浮动块用于布局，层叠级别中；		 【店内各产品货架的布局】
	行内元素为内容，层叠级别最高。		【重要商品在货架上的布局】
3）BFC/IFC		
	格式上下文(FC)，分为块级BFC和行级LFC。
	一个HTML元素要创建BFC，则满足下列的任意一个或多个条件即可：
		1、float的值不是none。
		2、position的值不是static或者relative。
		3、display的值是inline-block、table-cell、flex、table-caption或者inline-flex
		4、overflow的值不是visible
		* 块级概念：display为block\table\list-item的元素

	BFC特点：
		相邻块盒子垂直边距叠加
		左边界紧贴容器左边
		内部新BFC不会与float元素区域重叠
		内部子元素不影响外面。
	BFC用途：
		创建BFC避免垂直外边距叠加
		清除浮动
		实现自适应

	overflow:hidden;原理：
		如果一元素为BFC,则浮动子元素高度也算入该元素高度。

4）display:table-cell;使元素具有td元素特点。应用于：
	图片垂直居中于元素
		使用display:table-cell;vertical-align:middle;实现大小不固定图片的垂直居中效果
		父元素{display:table-cell;vertical-align:middle;}
		子元素{vertical-align:middle;}
	等高布局
		父元素{display:table-row;}
		子元素{display:table-cell;vertical-align:middle;text-align:center;}
	自动平均划分元素，在一行显示
		可应用于导航。当给父元素宽度时，父元素宽度会根据子元素个数进行自动平均划分
		父元素{display:table;width:300px}
		子元素{display:table-cell;}
~~~





### 技巧篇

****

以下技巧在实际开发中运用频繁！**纯干货(初级)**！



块元素转行内元素

display:inline;

display:inline-block【行内块，常用】



行内元素转块元素

display:block;



有关**display**

~~~css
display:table-cell;使元素具有td元素特点。应用于：
图片垂直居中于元素
	使用display:table-cell;vertical-align:middle;实现大小不固定图片的垂直居中效果
	父元素{display:table-cell;vertical-align:middle;}
	子元素{vertical-align:middle;}
等高布局
	父元素{display:table-row;}
	子元素{display:table-cell;vertical-align:middle;text-align:center;}
自动平均划分元素，在一行显示
	可应用于导航。当给父元素宽度时，父元素宽度会根据子元素个数进行自动平均划分
	父元素{display:table;width:300px}
	子元素{display:table-cell;}
去除inline-block(img)元素间距：
	父元素{font-size:0;}	子元素{display:inline-block;}

display:none;	隐藏后不占位置
visibility:hidden;隐藏后还是占位置
~~~



文本效果

~~~css
在背景为 logo 的 h1 标签中置入文字后设置 text-indent:-9999px; 可隐藏文字内容，有利于SEO。
text-align 对文字、行内元素、inline-block元素起作用，但对块元素不起作用。
text-align:center;	实现文字、行内元素以及inline-block元素的水平居中，在父元素定义。
margin:0 auto;		实现块元素的水平居中，在当前元素中定义。
line-height是两行文字 基线之间 的距离。
可以定义height和line-height属性值相等，实现 单行文字 的垂直居中。
vertical-align:middle;	实现文字、行内元素以及inline-block元素的垂直居中，块无效。
~~~



表单效果

~~~css
单选框问题：
文字与单选框对齐：通过vertical-align:-..px方式对齐
文字为12px	-->	vertical-align:-3px;
文字为14px	-->	vertical-align:-2px;

textarea文本域	
固定大小，禁用拖动	用width、height、resize:none;来固定禁拖。
相同外观，滚条适应	用width、height、overflow:auto;定义滚条自适应。
总结:	
textarea{
	width:100px;
	height:80px;
	overflow:auto;
	resize:none;
}
~~~



有关**浮动**

~~~css
对自身影响：转化为块元素，即display:block;
对父元素的影响：如果浮动元素高度大于父元素或者父元素无高度，发生塌陷(无高)。
对子元素的影响：如果一个元素是浮动元素(无height),子元素也是浮动元素，则自适应。

清除浮动：
1)overflow:hidden;	应用于浮动元素的父元素
2)clear:both;	添加了多余的div标签
3)::after	实际开发中，用::after伪元素结合clear:both; 来实现
.clearfix{*zoom:1;}
clearfix:after
{
	clear:both;
	content:””;
	display:block;
	height:0;
	visibility:hidden;
}
~~~



有关**定位**

~~~css
position:absolute;	会将元素转换为块元素。实现子元素相对父元素定位，给父元素定义position:relative; 子元素定义position:absolute;配合top,bottom,left,right来定位。
绝对定位元素是相对于第一个设置了position:relative;position:absolute;position:fixed;的祖先元素进行定位的。
z-index只有在元素定义position:relative;position:absolute;position:fixed;才会被激活。
~~~

