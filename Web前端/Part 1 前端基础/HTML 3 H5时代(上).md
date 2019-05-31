## H5，标签语言的逆袭



##### h5特点：

- 基于html, css, dom, javascript【本质】
- 减少对外部插件需求【自强】
- 错误处理优化【自省】
- 更多取代脚本的标记【自立】
- h5独立于设备【随和】
- 开发进程对公众透明【廉洁】

------

##### h5有趣新特性:

- 绘画canvas元素和svg
- 媒介回放的video、audio
- 本地离线存储localStorage sessionStorage
- 新的特殊内容元素，article\footer\header\nav\section【增强语义化】
- 新的表单控件，calendar[日历] date time email url search

------

##### h5新添标签：

布局类：用来布局，加强语义化的标签： (类div)

1. header	
2. footer
3. article -> div 
4. section -> p
5. nav 
6. aside

功能类：画板、音频功能

1. svg
2. canvas
3. audio	音频
4. video	视频

其他：

**自定义标签：行级元素**

------

##### html5新属性

- contenteditable 是否可以修改文本内容[true false]
- draggable 是否可以拖放[true false]*
- hidden 隐藏[直接加hidden]
- **data-xxx 自定义属性[data-id="mark1"]**

------

##### 拖放

- 属性：draggable:auto true false

- 拖动事件：
  ​	 dragstart 开始拖放触发
  ​	 dragend 拖放结束后触发
  ​	 drag 拖动时触发
  ​	 	事件监听：dom.ondragstart = function(e){...}
  ​	释放区事件：
  ​	 dragenter 被拖元素进入释放区
  ​	 dragover 被拖元素在释放区内移动
  ​	 dragleave 被拖元素出释放区
  ​	 drop 被拖动元素在释放区抬起鼠标
  ​	 	事件监听：dom.ondragover = function(e){
  ​	 			e.preventDefault();//防止触发不了drop
  ​	 	                 }

  【**默认情况下，数据/元素不能放置到其他元素中。 如果要实现改功能，我们需要防止元素的默认处理方法。我们可以通过调用 event.preventDefault() 方法来实现 ondragover 事件。**】

- 数据传递：
  ​	e.dataTransfer[传输数据到释放区的对象]
  ​	e.dataTransfer.setData('x', 字符串);
  ​	**只能两点传输：dragstart ===> drop**
  ​	e.dataTransfer.setData('x', JSON.stringify({id: e.target.id}))
  ​	【JSON.parse JSON.stringify】
  ​	JSON.parse(e.dataTransfer.getData('x'));
  ​	e.dataTransfer.types 返回数据格式 字符串数组
  ​	e.dataTransfer.clearData('x') 移除指定格式数据
  ​	e.dataTransfer.files 返回被拖动文件的列表 

------

##### 拖拽demo：

```html
<style>
		#wrap{
			width:500px;
			height:50px;
			border:1px solid #000;
		}
		.demo{
			width:50px;
			height:50px;
			background-color:orange;
			display:inline-block;
		}
		#demo2{
			background-color:blue;
		}
		#demo3{
			background-color:green;
		}
		#demo4{
			background-color:red;
		}
		#demoBox{
			width:500px;
			height:500px;
			border:1px solid #000;
		}
	</style>
</head>
<body>
	<div id="wrap">
		<div id="demo" class="demo" draggable="true"></div>
		<div id="demo2" class="demo" draggable="true"></div>
		<div id="demo3" class="demo" draggable="true"></div>
		<div id="demo4" class="demo" draggable="true"></div>
	</div>
	<div id="demoBox"></div>
	<script>
	// 配合draggable使用!
	var id = null;
	var demo = document.getElementById('demo');
	var demoBox = document.getElementById('demoBox');
	var wrap = document.getElementById('wrap');
	// demo.ondragstart = function(e){
	// 	id = this.id
	// }
	wrap.ondragstart = function(e){
		// id = e.target.id;//冒泡选择
		e.dataTransfer.setData('id', e.target.id);//数据传输
	}
	demoBox.ondragover = function(e){
		e.preventDefault();//防止触发不了drop
	}
	demoBox.ondrop = function(e){
		// var oDiv = document.getElementById(id).cloneNode(true);
		var oDiv = document.getElementById(e.dataTransfer.getData('id')).cloneNode(true);//接收数据
		this.appendChild(oDiv);
	}
	</script>
```

****

##### canvas 画布

canvas主要用在 游戏 或 图表 里面

canvas的**尺寸设置在标签内部**！

在 **codepen** 有 canvas 的极品案例

canvas历史：
​	apple的safari 1.3引入
​	ie9之前不支持

**支持查询：** http://caniuse.com/

两个对象：
​	元素对象（canvas）相对于画布	[canvas]
​	上下文对象相对于画笔	[ctx]

fill 和 stroke 都是作用在当前所有子路径
完成一条路径后要重新开始另一条路径要用beginPath方法，开始新的集合

------

canvas使用：

```html
<canvas width="500" height="500" id="cans"></canvas>
<script>
var oCanvas = document.getElementById('cans');
var ctx = oCanvas.getContext('2d');/*上下文对象(画笔)创建*/
//画图形
ctx.moveTo(100, 100);//起点
ctx.lineTo(200, 200);//终点

ctx.lineWidth = 10;  //粗细 
ctx.strokeStyle = 'red';//颜色
ctx.fillStyle = bg;//图片填充
ctx.closePath();//闭合(两条线才生效)

ctx.fill();//填充
ctx.stroke();//下笔画，描边 
		
ctx.beginPath();//拿起画笔，重新画💗【新建】
ctx.moveTo(100, 100);//新起点

// 矩形
	ctx.rect(x,y,w,h);
	ctx.stroke();//or ctx.fill()
	//直接画
	ctx.fillRect(x,y,w,h);
	ctx.strokeRect(x,y,w,h);

// 橡皮擦
	ctx.clearRect(0,0,300, 300)

// demo-掉落的矩形：
	ctx.fillRect(100, 100, 50, 50);
	var y = 100;
	var timer = setInterval(function(){
		ctx.clearRect(0, 0, 300, 300);
		ctx.fillRect(100, y, 50, 50);
		y += 10;
		if(y > 250){
			clearInterval(timer);
		}
	}, 100);

//弧形
	ctx.arc(x, y, r, s, e,  0);//起始弧度, 终止弧度, 时针方向0顺1逆
	ctx.arc(100, 100, 50, 0, Math.PI/2, 0);
	ctx.fill();//填充
	【圆的3点方向是0，六点方向Π/2，九点方向Π】
    //demo：小豆人
	ctx.moveTo(100, 100);
	ctx.arc(100, 100, 50, 0, Math.PI/2, 1);
	ctx.closePath();
	ctx.stroke();

//圆角
	ctx.arcTo(x1, y1, x2, y2, r);
				起点   终点  圆角半径
	ctx.moveTo(100, 110);
	ctx.arcTo(100, 200, 200, 200, 10);
	ctx.arcTo(200, 200, 200, 100, 10);
	ctx.arcTo(200, 100, 100, 100, 10);
	ctx.arcTo(100, 100, 100, 200, 10);
	ctx.stroke();

//贝塞尔
	ctx.quadraticCurveTo(x1, y1, ex, ey);
	ctx.moveTo(100, 100);
	ctx.quadraticCurveTo(200, 200, 400, 200);
	ctx.stroke();

//坐标轴移动
	ctx.translate(x, y);
	ctx.translate(100, 100);
	ctx.fillRect(0, 0, 100, 100);
	ctx.translate(-100, -100);
	ctx.fillRect(0, 0, 50, 50);

//缩放坐标轴
	ctx.scale(x, y);

//旋转坐标轴
	ctx.rotate(Math.PI/4);

//水平缩放\水平倾斜\垂直倾斜\垂直缩放\水平移动\垂直移动
	ctx.setTransform(a, b, c, d, e, f);
		//不受之前坐标轴设定影响
	transform(...);
		// 参数同上,受之前坐标轴设定影响

ctx.save();//保存此时刻坐标轴状态
ctx.restore();//读取上次save坐标轴状态[消耗次数]
// 多少个restore需要等量的save, 栈存储
		
//💗插入图片
	ctx.createPattern(image, "repeat|repeat-x|repeat-y|no-repeat");
	var img = new Image();
	img.src = 'img/1.jpg';
	img.onload = function(){
		var bg = ctx.createPattern(img, 'no-repeat');
		ctx.fillStyle = bg;
		ctx.fillRect(0, 0, 400, 400);
	}
		
//渐变
    //径向渐变
	var bg = ctx.createLinearGradient(0, 0, 500, 500);
	bg.addColorStop(0, 'red');//0%
	bg.addColorStop(.5, 'green');
	bg.addColorStop(1, 'yellow');
	ctx.fillStyle = bg;
	ctx.fillRect(0, 0, 500, 500);
	// 圆渐变
	var bg = ctx.createRadialGradient(x1, y1, r1, x2, y2, r2);

// 阴影
	ctx.shadowColor = 'red';
	ctx.shadowBlur = 10;
	ctx.shadowOffsetX = 10;
	ctx.shadowOffsetY = 10;
	ctx.fillRect(100, 100, 100, 100);

//文本
	ctx.fillStyle = 'green';
	ctx.font = '50px sans-serif';
	ctx.fillText('Hi', 100, 100);

//线段样式
	ctx.lineCap = 'round|square|butt';
				   /*圆角, 加长, 默认*/
		
//闭合
	ctx.lineJoin = 'miter|round|bevel'
					/*尖角, 圆角, 削角*/
	ctx.miterLimit = 20;//斜接部分超过则变为bevel

//裁剪
	ctx.clip();	//当前路径外的区域不再绘制
	可以在clip()前使用save()方法保存, 后续通过restore()方法恢复

//合成
	ctx.globalCompositeOperation = 'source-in';//更多参考文档

//透明
	ctx.globalAlpha = '0.5';

//图片
	var img = new Image();
	img.src = 's.jpg';
	img.onload = function(){
		ctx.drawImage(img, 0, 0, 200, 200);
		//从0,0开始画, 图片尺寸200*200
		//9参数,前四个为所绘制目标元素起始点\宽高
		//后四个为canvas绘制的起始点和大小
		var data = oCanvas.toDataURL();/*必须在本地服务器*/
		var oImg = document.getElementsByTagName('img')[0];
		oImg.src = data;
	}

// 导出canvas内容
	canvas.toDataURL() 是canvas自身方法非ctx上下文对象
	/*受同源策略影响, 需要在本地服务器打开*/
	//将canvas内容抽取成一张图片, base64编码格式, 放进img元素里

var data = ctx.getImageData(0,0,500,500);
//百万数据, 250000*4(像素点rgba)
ctx.putImageData(data,500,500);

命中检测
ctx.isPointInPath(x, y);//是否在线上
ctx.isPointInStroke(x,y);//是否在区域内

</script>
```

------

##### 混合使用

```javascript
var oCanvas = document.getElementById('cans');
var ctx = oCanvas.getContext('2d');
ctx.fillStyle = 'green';
ctx.arc(200, 200, 50, 0, Math.PI*2, 0);
ctx.fill();
ctx.save();
ctx.clip();//裁点
ctx.closePath();
ctx.beginPath();
ctx.restore();
ctx.fillStyle = 'red';
ctx.fillRect(200, 200, 100, 100);
ctx.fill();
```

------

canvas实现刮刮乐

```html
<style>
		canvas{
			border:1px solid #eee;
			background-size:cover;
		}
</style>

<body>
	<canvas width="500" height="500" id="cans"></canvas>
	<script>
	var oCanvas = document.getElementById('cans');
	var ctx = oCanvas.getContext('2d');
	var lastX, lastY, nowX, nowY;
	init();
	function init(){
		ctx.fillStyle = '#ccc';
		ctx.fillRect(0, 0, 500, 500);
		var oImg = new Image();
		var x = Math.random();
		oImg.src = x < 0.5 ? '1.jpg' : '2.jpg';
		oImg.onload = function(){

			oCanvas.style.backgroundImage = 'url("' + oImg.src + '")';//必加引号
			//合成方法
			ctx.globalCompositeOperation = 'destination-out';
			//在新图像外显示已有图像。只有新图像外的已有图像部分会被显示，新图像是透明的。
			document.addEventListener('mousedown', downFun, false);
            //false 由里向外冒泡；	true 由外向里捕获
		}
	}

	function downFun(e){
		lastX = e.clientX - oCanvas.offsetLeft;
		lastY = e.clientY - oCanvas.offsetTop;
		document.addEventListener('mousemove', moveFun, false);
		document.addEventListener('mouseup', upFun, false);
	}

	function moveFun(e){
		nowX = e.clientX - oCanvas.offsetLeft;
		nowY = e.clientY - oCanvas.offsetTop;
		ctx.beginPath();//新建画笔
		ctx.lineWidth = '40';
		ctx.moveTo(lastX, lastY);
		ctx.lineTo(nowX, nowY);
		ctx.stroke();
		// ctx.closePath();
		ctx.arc(nowX, nowY, 20, 0, Math.PI * 2, 0);
		ctx.fill();
		lastX = nowX;
		lastY = nowY;
	}
        
	function upFun(){
		document.removeEventListener('mousemove', moveFun, false);
		clearAll();
	}

	function clearAll(){
		var d = ctx.getImageData(0, 0, 500, 500);//获取数据
		var len = d.data.length;
		var num = 0;
		for(var i = 0; i < len; i += 4){
			if(d.data[i] == 0){
				num ++;
			}
		}
		if(num > 500 * 500 *0.8){
			ctx.clearRect(0, 0, 500, 500)
		}
	}
	</script>
</body>
```

****

##### H5 SVG

svg：可缩放的矢量图形，由图形构成，不会失真，应用于图表图标、动效和矢量图

与Canvas区别：

![sc区别](C:\Users\lenovo-pc\Desktop\渡一前端\总结笔记\H5\sc区别.png)

```html
<svg width="300" height="300" viewBox="0, 0, 200, 200">
<!-- 直线 -->
	<line x1="100" y1="100" x2="200" y2="200"></line>
    line{
		stroke:red;/*默认颜色是透明的*/
		stroke-width:10px;
		stroke-linecap:square;/*round圆帽, butt默认*/
		stroke-dasharray:10px 20px 30px;/*切割展示成虚线*/
		stroke-dashoffset: 10px;/*偏移*/
	}
<!-- 矩形 -->
	<rect x='50' y='50' width='50' height='50' rx='10' ry='10'></rect>
<!-- 圆形 -->
	<circle r='50' cx='50' cy='50'></circle>
<!-- 椭圆 -->
	<ellipse rx='100' ry='50' cx='400' cy='150'></ellipse>
    				大小				  位置
<!-- 折线 -->
	<polyline points="100 100, 200 50, 300 100, 400 50"></polyline> 
    polyline{
		fill:transparent;/*默认fill*/
		stroke:red;
		stroke-opacity:0.5;
		stroke-linejoin:bevel;/*削尖, miter默认, round圆滑*/
		stroke-miterlimit:20;/*无单位!*/
	}
<!-- 多边形 -->
	<polygon points="100 100, 200 50, 300 100, 400 50"></polygon>
    polygon{
		fill:transparent;/*默认fill*/
		stroke:red;
		fill-opacity:0.5;
	}
<!-- 文本 -->
	<text x=400 y=150>k-dash</text>
<!-- path -->
	<path d='M 100 100 L 200 200 L 200 200'></path>
	<!-- 大小写区别:小写相对于上一点而定位 -->
	<!-- 大写绝对定位,小写相对定位 -->
	<path d='M 100 100 H 200 V 300 z'></path>
	<!-- H水平, V竖直, z闭合路径 -->
    path{
		stroke:red;
		fill:transparent;/*不填充*/
	}
<!-- 圆弧 -->
	<path d='M 100 100 A 70 120 90 1 1 150 200'></path>
							  椭圆 旋转 1大圆弧 顺逆时针1顺 截至点
<!-- 贝塞尔曲线 -->
	<path d="M 100 100 Q 200 50 300 300 T 350 200"></path>

渐变:
	<defs>
		<linearGradient id="bg1" x1="0" y1="0" x2="0" y2="100%">
			<stop offset="0%" style="stop-color:rgba(255,255,0,1)"></stop>
			<stop offset="100%" style="stop-color:rgba(255,0,0,1)"></stop>
		</linearGradient>
		<radialGradient id="bg2" cx="50%" cy="50%" r="50%" fx="50%" fy="50%">
			<stop offset="0%" style="stop-color:rgba(255,255,0,1)"></stop>
			<stop offset="100%" style="stop-color:rgba(255,0,0,1)"></stop>
		</radialGradient>
	</defs>
	<rect x="100" y="100" width="200" height="200" style="fill:url(#bg1)"></rect>

滤镜:
	<defs>
		<filter id="Gadussian_Blur">
			<feGaussianBlur in="SourceGraphic" stdDeviation="20">
		</filter>
	</defs>
	<rect x y width height fill="yellow" style="filter:url(#Gadussian_Blur)"></rect>
</svg>

svg事件
	var svg = document.getElementsByTagName('svg')[0];
	var line = document.getElementsByTagName('line')[0];
	line.getTotalLength();/*获取长度*/
	line.getPointAtLength(50);
	//严格来说只适用于path!
```

------

demo：抽风效果

```html
line{
	stroke:red;
	stroke-width:10px;
	stroke-dasharray:300px;
	stroke-dashoffset:300px;
	animation:move 2s linear infinite alternate-reverse;
}
@keyframes move{
	0%{
		stroke-dashoffset:300px;
	}
	100%{
		stroke-dashoffset:0;
	}
}
<script>
		// 创建svg
		var svg = document.createElementNS('http://www.w3.org/2000/svg','svg');
		var line = document.createElementNS('http://www.w3.org/2000/svg','line');
		svg.setAttribute('width', 300);
		svg.setAttribute('height', 300);
		line.setAttribute('x1',0);
		line.setAttribute('x2',300);
		line.setAttribute('y1',100);
		line.setAttribute('y2',100);
		svg.appendChild(line);
		document.body.appendChild(svg);
</script>
```

------

demo：仪表盘

```html
<style>
	path{
		stroke-width:10px;
		fill:transparent;
		stroke:#eee;
    }
	#demo{
		stroke:aqua;
		transition:stroke-dashoffset 1s;
	}
</style>
<body>
	<input type="text" id="inp">
	<svg width="500" height="500">
		<path d="M 100 200 A 60 60 0 1 1 200 200"></path>
		<path d="M 100 200 A 60 60 0 1 1 200 200" id='demo'></path>
	</svg>
	<script>
		var len = demo.getTotalLength();
		demo.style.strokeDashoffset = len;
		demo.style.strokeDasharray = len;
		inp.onblur = function(){
			if(Number(this.value)){
				demo.style.strokeDashoffset = (100 - this.value) / 100 * len;
			}
		}
	</script>
</body>
```

****

