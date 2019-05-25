##### CSS实现三角形

~~~html
html:
<div class="sjx"></div>

css:
<style>
    .sjx{
        width:0;
        height:0;
        border-width:15px;
        border-style:solid;
        border-color:transparent black transparent transparent;
    }
</style>
~~~

#### 

##### CSS实现椭圆

border-radius: x/y;		x：圆角水平半径；y：圆角垂直半径

~~~html
html:
<div class="ty"></div>

css:
<style>
    .ty{
        width:300px;
        height:200px;
        border:1px solid gray;
        border-radius:15
    }
</style>
~~~



##### textarea文本域设置

固定大小，禁用拖动
相同外观，滚条适应

~~~css
textarea{
	width:100px;
	height:80px;
	overflow:auto;
	resize:none;
}
~~~



##### 文字居中

~~~css
单行文字居中：
	line-height、height相等就可以
多行文字居中：
	父元素div{display:table-cell;vertical-align:middle;}
	子元素span{display:inline-block;}
块元素居中：position方法，可用于所有元素，行内、块通用
~~~



##### 雪碧图和图标

~~~css
CSS Sprite：CSS雪碧图
.sprite{background:url(sprite.png) no-repeat;height:xx;padding:xx}
.sprite{background-position:-0px -60px;}

IconFont图标：
www.iconfont.cn
先下载，然后在CSS中引入字体文件：
@font-face{
	font-family:”iconfont”;
	src:url(fonts/iconfont.eot);/*IE9*/
	src:url(fonts/iconfont.eot?#iefix) format(“embedded-opentype”),
   		url(fonts/iconfont.woff) format(“woff”),
   		url(fonts/iconfont.ttf) format(“truetype”),
		url(fonts/iconfont.svg) format(“svg”),
	font-width:normal;
	font-style:normal;
}
~~~

