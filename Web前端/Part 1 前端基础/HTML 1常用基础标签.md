### HTML基础标签

****

#### **字体标签**

~~~html
<pre></pre>
预格式化标签，可直接使用空格、换行符。

<i></i><em></em>
斜体文字

<b></b>
文字加粗

<ins></ins>
下划线

<del></del>
 删除线

<sup></sup>
上标

<sub></sub>
下标

&lt;(<)		&gt;(>)		&copy;(@c)		&trade;(™)
特殊符号
~~~



#### **列表标签**

~~~html
<ul>
	<li></li>
	<li></li>
</ul>
无序列表
list-style:	disc圆, square 方, circle 空心

<ol>
	<li></li>
	<li></li>
</ol>
有序列表
list-style：	1 数字, a,A 字母, i,I 罗马数字

<dl>
	<dt></dt>
	<dd></dd>
</dl>
定义列表
dt 项目, dd 说明 
(dt, dd是同级关系，不相互包括)
~~~



#### **图像、超链接**

~~~html
<img src=”路径” alt=”文字说明” name=”加载失败代替文字”/>
图像标签

<a href=”路径” target=”打开方式” title=”文字说明”>点击这里</a>
超链接
target：_self 直接刷新；_black 打开新网页

制锚：<a href=”路径#锚名” target=”_blank”>跳转</a>	路径举例:  index.html#锚名
抛锚：<a name=”锚名”></a>
锚链接
注：必须通过 name 属性来取得猫名，id虽然也ok，但id不能滥用

<a href=”mailto:894241445@qq.com”>反馈意见</a>
电子邮件
mailto 不用驼峰命名喔！

<a href=”ftp/ftp.rar”>文件下载</a>
文件下载
ftp协议，即文件传输协议
~~~



#### **表格**

~~~html
caption：定义标题，居中
th：表头，居中、加粗
tr：行，属性：
align：水平对齐left、center
valign：垂直对齐 top、middle、bottom
bgcolor：行的背景色
td：单元格，属性同行，bgcolor单元格背景色
table：表格，

属性：
bgcolor：表格背景色；
border：边框；
cellspacing：格间隔；
cellpadding:文本和边框距；
frame:外边框，void, box
rules:内测线条 none, rows行，cols列，all全

表格demo：
<table border=”1”>
	<caption>标题说明</caption>
	<thead>
		<tr>
			<th>表头</th>
			<td>单元格内容1</td>
			<td>单元格内容2</td>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td>属性</td>
			<td>值1</td>
			<td>值2</td>
		</tr>
		<tr>
			<td>属性</td>
			<td>值1</td>
			<td>值2</td>
		</tr>
	</tbody>
	<tfoot>
		<tr>
			<td>属性</td>
			<td>值1</td>
			<td>值2</td>
		</tr>
	</tfoot>
</table>

高级使用：
跨行属性：rowspan
跨列属性：colspan
【垂R水C】
都加在td里面，注意数量关系
格式：<td rowspan=”2”>内容</td>
~~~



#### **表单**

~~~html
<form action=”ftp.php” method=”post” target=”_blank”>
	<input type=”类型” name=”名称” value=”默认文字” placeholder=”空段输入的默认文段”>
</form>

action：向何处发送表单数据，是URL(如php后台处理文件)

method 如何发送：get暴露信息，信息数量由url栏限制，一般用于获取信息
 			   post掩盖信息，作为http请求体一部分，一般用于安全类(如密码更改)操作

target 如何打开：_blank 新页面，_self 本页打开。

type的属性：
password	密码  
text 账号/用户名	maxlength最大字符
file 上传文件
radio 单选框，同级要求name相同，checked默认选中
<input type=”radio” name=”xx” value=”男” checked/>
<input type=”radio” name=”xx” value=”女” checked/>
checkbox 复选框，同级要求name相同，checked默认选中
select 下拉列表，格式：
<select name=”city”>
	<option value=”choose” selected>--请选择--</option>
	<optgroup lable=”一线”>
		<option value=”bj”>北京</option>
		<option value=”sh”>上海</option>
		<option value=”gz”>广州</option>
	</optgroup>
	<optgroup lable=”二线”>
		<option value=”st”>汕头</option>
	</optgroup>
</select>
submit 上交按钮，value置名
reset  重置按钮，value置名
image  图片按钮，src定图
button 按钮，value置名
textarea 多行文本域，格式：
<textarea name=”自我介绍” rows=”5” cols=”20” placeholder=”请介绍你自己”></textarea>
~~~