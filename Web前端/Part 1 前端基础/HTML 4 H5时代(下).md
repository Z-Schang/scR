##### H5 音频

------

```html
--音
<audio controls autoplay preload="auto">
	<source src="1.mp3" type="audio/mpeg"></source>
	<source src="1.ogg" type="audio/ogg"></source>
</audio>
--频
<video src="1.mp4" controls autoplay poster="x.jpg"></video>

js操作：
<script>
var audio = document.createElement('audio');
var audio = new Audio();//  video不可以用new
audio.setAttribute('controls', 'controls');
//audio.controls = true;
audio.src = "1.mp3";
audio.setAttribute('autoplay','autoplay');
//audio.autoplay = true;
//audio.preload = 'auto';
audio.loop = "loop";
document.body.appendChild(audio);
</script>
```

------

##### 属性：

- controls	        用户控件, 没有设置则不显示标签
- autoplay        自动播放
- preload         预加载, 规定是否页面加载后载入影片, 与autoplay冲突
  ​		       none \ metadata 加载完元数据载入 \ auto 加载需要的
- loop               是否循环播放
- poster           【**video独有**】视频不能用时使用图片替代,否则空白,  封面照片

##### 其他属性：

- video.volume -= 0.3;                  //音量调节	0~1
- audio.playbackRate += 0.3        //速率调节 1正常, 负数回放
- audio.currentTime = 50;            //播放时间, 单位为秒
- audio.duration                            //视频时长
- audio.played                               //已播放
- audio.buffered                            //缓存
- audio.seekable                           //可否跳转
- audio.paused                              //是否暂停
- audio.seeking                              //是否移动进度条
- audio.ended                                //是否结束
- audio.readyState                        //视频状态
- audio.networkState                   //网络状态

```javascript
x.onclick = function(){
	if(audio.volume <= 0.7){
		audio.volume += 0.3;
	}else{
		audio.volume = 1;
	}
}

c.onclick = function(){
	if(audio.playbackRate < 2){
		audio.playbackRate += 0.1;
	}
}

play.onclick = function(){
	if(audio.paused){
		audio.play();
		this.innerText = '暂停';
	}else{
		audio.pause();
		this.innerText = '播放';
	}
}
```

------

##### 方法：

```javascript
video.play();
video.pause();
video.load();//重载

if(video.canPlayType('audio/mp3')){
	video.src = '1.mp3';
	video.play();
}
```

------

##### 事件：

play				播放触发
pause			暂停触发
loadedmetadata	浏览器获取完媒体的元数据后触发
loadeddata		浏览器加载完当前帧数据,准备播放时触发
ended			播放结束触发

------

##### 状态：

![媒体网络状态](C:\Users\lenovo-pc\Desktop\渡一前端\总结笔记\H5\媒体网络状态.png)

![媒体状态](C:\Users\lenovo-pc\Desktop\渡一前端\总结笔记\H5\媒体状态.png)

------

##### H5 存储 历史 异步

运动优化

```javascript
//传统运动
var box = document.getElementsByClassName('box')[0];
var timer;
function move(){
//way1
	timer = setInterval(function(){
	box.style.left = box.offsetLeft + 10 + 'px';
	if(box.offsetLeft > 600){
		clearInterval(timer);
	}
	},10);
//way2
	timer = setTimeout(function(){
	box.style.left = box.offsetLeft + 10 + 'px';
		if(box.offsetLeft < 600){
			move();
		}else{
			clearTimeout(timer);
		}
	},10);

//h5优化:
	timer = requestAnimationFrame(function(){
		box.style.left = box.offsetLeft + 10 + 'px';
		if(box.offsetLeft < 600){
			move();
		}else{
			cancelAnimationFrame(timer);
		}
	});//默认时间16.666666,不用传, 1s刷新60次。优势:屏幕刷新频率,不丢帧

}
move();

		
//兼容
window.requestAnimationFrame = (function(){
	return window.requestAnimationFrame || 
	 window.webkitRequestAnimationFrame ||
		window.mozRequestAnimationFrame ||
	function(callback){
		window.setTimeout(callback, 1000/60);
	}
})();

function run(){
	box.style.left = box.offsetLeft + 10 + 'px';
	var timer = requestAnimationFrame(run);
	if(box.offsetLeft > 600){
		cancelAnimationFrame(timer);
	}
}
```

------

##### webstorage

- webStorage		不会传到服务器端 	5M
  - localstorage	         永久存储	        作用域:文档源限制
  - sessionStorage	  临时存储[窗口]	作用域:文档源 + 窗口限制
- cookie                      会传到服务器端		4K
  - 存储信息到用户设备上
  - navigator.cookieEnabled    检测是否启用了cookie
  - document.cookie = 'name="Mike"; max-age=1000'     设置cookie
  - document.cookie      获得cookie

**根本区别：时间不同, 大小不同**

```javascript
//存:
	localstorage.info = JSON.stringify({name:'ss', company:'dd'});
	localstorage.setItem('name','ss');
//取:
	JSON.parse(localstorage.info);
	localstorage.getItem('name');
//删:
	localstorage.removeItem('xx');
```

![cookie和storage区别](C:\Users\lenovo-pc\Desktop\渡一前端\总结笔记\H5\cookie和storage区别.png)

------

##### history

- history.length           历史页数
- history.back()            历史上一页
- history.forward()      历史下一页
- history.go(3);             跳转至历史第三页
- history.pushState(null, null, "同域url/#a");           添加历史纪录
- history.replaceState(null, null, '#a');                      替换当前历史纪录
- window.addEventListener('popstate',function(e){
  ​	//当更改历史纪录发生,只有手动更改才会触发,调用pushreplace不触发
  })
- hashchange事件,当哈希值改变时触发,用于构建单页面应用

```javascript
//demo : 历史跳转
<input type="text" id="inp">
<button id="btn">go</button>
<ul id="wrap">
</ul>
var data = [{name:'kk'},{name:'dd'},{name:'ww'}];
function renderDom(data){
    var str = '';
    data.forEach(function(ele){
        str += '<li>' + ele.name + '</li>';
    });
    wrap.innerHTML = str;
}
renderDom(data);
btn.onclick = function(){
    var key = inp.value;
    var dataList = data.filter(function(item){
        return item.name.indexOf(key) > -1;
    });
    renderDom(dataList);
    history.pushState({
        key: key
    },null, '#'+ key);
}
//出栈事件监听
window.addEventListener('popstate', function(e){
    console.log(e.state);
    var key = e.state ? e.state.key : '';
    var dataList = data.filter(function(item){
        return item.name.indexOf(key) > -1;
    });
    inp.value = key;
    renderDom(dataList)
})
```

拓展：

1. hash值浏览器是不会随请求发送到服务器端的（即地址栏中#及以后的内容）。
2. 可以通过window.location.hash属性获取和设置hash值。
3. 如果注册onhashchange事件，设置hash值会触发事件。可以通过设置window.onhashchange注册事件监听器，也可以在body元素上设置onhashchange属性注册。
4. window.location.hash值的变化会直接反应到浏览器地址栏（#后面的部分会发生变化）
5. 同时浏览器地址栏hash值的变化也会触发window.location.hash值的变化，从而触发onhashchange事件。
6. 当浏览器地址栏中URL包含hash如http://www.baidu.com/#home ，这时按下enter，浏览器发送http://www.baidu.com/请求至服务器,请求完毕之后设置hash值为#home，进而触发onhashchange事件。
7. 当只改变浏览器地址栏URL的hash部分，这时按下enter,浏览器不会发送任何请求至服务器，这时发生的只是设置hash值新修改的hash值，并触发onhashchange事件。
8. html的a标签属性href可以设置为页面的元素ID如#top,当点击该锚链接时页面跳转至该id元素所在区域，同时浏览器自动设置window.location.hash属性，同时地址栏hash值发生改变，并触发onhashchange事件。

------

##### worker

- worker异步执行js，跨域访问！

- worker不操作dom!!!适用于数据运算

- worker和主文件要满足同源策略

- worker和主线程的通信

- worker.postMessage(500);  发送数据

- message  接收事件

- worker的js操作:

  ```javascript
  this.onmessage = function(e){
  	var num = 0;
  	for(var i = 0; i < 1000; i++){
  		num ++;
  	}
  	var sum = e.data + num;
  	postMessage(sum);
  	this.close();//辞职
  }
  
  var worker = new Worker('worker.js');
  worker.postMessage(500);
  console.log('aaa');
  worker.onmessage = function(e){
  	console.log(e.data);
  	worker.terminate();//炒鱿鱼
  }
  ```

- 结束worker

  ```
  close()在worker作用域中调用worker.js  [工人辞职]
  worker.terminate()  [炒鱿鱼]
  ```

  ![worker缺点](C:\Users\lenovo-pc\Desktop\渡一前端\总结笔记\H5\worker缺点.png)

------

##### 引入模块:

```javascript
importScripts('add.js');//直接使用
```

importScripts用于在一个js里面包含其他的js文件。

相当于C里面的#include。利用importScripts这个强大的利器，我们就可以像C/C++/Java一样写js了。比如我们用js写了几个文件A.js，B.js，C.js，它们分别位于不同的路径下面。当我们在D.js中需要引入上面3个js文件的时候，就需要importScripts这个强大的利器了

------

##### fileReader

预览\异步发送请求(上传文件)

![fileReader读取事件](C:\Users\lenovo-pc\Desktop\渡一前端\总结笔记\H5\fileReader读取事件.png)

![fileReader](C:\Users\lenovo-pc\Desktop\渡一前端\总结笔记\H5\fileReader.png)

```html
<input type="file">
<img src="" alt="">
<div class="progress">
	<div class="bar"></div>
</div>
<span class="text"></span>
<button class="abort">终止</button>
<script>
var inp = document.getElementsByTagName('input')[0];
var img = document.getElementsByTagName('img')[0];
var bar = document.getElementsByClassName('bar')[0];
var text = document.getElementsByTagName('span')[0];
var btn = document.getElementsByTagName('button')[0];
var reader = new FileReader();
inp.onchange = function(){
	console.log(inp.files);
	reader.readAsDataURL(inp.files[0]);
}
//开始加载
reader.onloadstart = function(e){
	console.log('start', e, e.target.result);
	//this = e.target
}
//加载过程，进度条变化
reader.onprogress = function(e){
	console.log('progress', e.loaded / e.total * 100%);
	var precent = e.loaded / e.total * 100;
	var width = Math.round(300 * precent / 100);
	bar.style.width = width + 'px';
	text.innerHTML = Math.round(precent) + '%';
}
//加载成功
reader.onload = function(e){
	console.log('success', e);
	img.src = this.result;
}
//加载完（不一定成功）
reader.onloadend = function(e){
	console.log('end', e);
}
//暂停加载
btn.onclick = function(){
	reader.abort();
}
</script>
```

分割文件读取

```html
<style>
	img{
		display:block;
		height:200px;
	}
	.progress{
		width:300px;
		height:30px;
		border:1px solid #222;
	}
	.bar{
		width:0;
		height:30px;
		background-color:greenyellow;
	}	
</style>
<body>
	<input type="file">
	<img src="" alt="">
	<div class="progress">
		<div class="bar"></div>
	</div>
	<span class="text"></span>
	<button class="abort">终止</button>
<script>
var inp = document.getElementsByTagName('input')[0];
var img = document.getElementsByTagName('img')[0];
var bar = document.getElementsByClassName('bar')[0];
var text = document.getElementsByTagName('span')[0];
var btn = document.getElementsByTagName('button')[0];

inp.onchange = function(){
	bar.style.width = 0;
	var reader = new PartFileReader(inp.files[0], 'readAsDataURL', {
		loadStart: function(){console.log('start load');},
		progress: function(e, loaded, total){
				var self = this;
				var precent = loaded / total * 100;
				var width = Math.round(300 * precent / 100);
				bar.style.width = width + 'px';
				text.innerHTML = Math.round(precent) + '%';
				btn.onclick = function(){
					console.log(self);
					self.abort();
				}
			},
		load: function(){},
		loadend: function(){},
		abort: function(){
			alert('你终止了上传');
		}
	});
}

function PartFileReader(files, type, event){
	this.files = files;
	this.type = type;
	this.event = event;
	this.step = 1024 * 1024;
	this.loaded = 0;
	this.total = files.size;
	this.reader = new FileReader();
	this.abort = this.reader.abort();
	this.readPartFile(0);//必须写在尾部
	this.bindEvent();
}

PartFileReader.prototype.readPartFile = function(start){
	if(this.files.slice){
		var file = this.files.slice(start, start + this.step);//从0开始每步每步截
		switch(this.type){
			case 'readAsBinaryString' : 
				this.reader.readAsBinaryString(file);
				break;
			case 'readAsDataURL' :
				this.reader.readAsDataURL(file);
				break;
			case 'readAsText' :
				this.reader.readAsText(file);
				break;
			case 'readAsArrayBuffer' : 
				this.reader.readAsArrayBuffer(file);
				break;
			default:
				break;
		}
	}
}

PartFileReader.prototype.bindEvent = function(){
	var self = this;
	this.reader.onloadstart = function(e){
		self.event.loadStart && self.event.loadStart.call(this, e);
	}
	this.reader.onprogress = function(e){
		self.loaded += e.loaded;
		self.event.progress && self.event.progress.call(this, e, self.loaded, self.total);
	}
	this.reader.onload = function(e){
		self.event.load && self.event.load.call(this, e);
		if(self.loaded < self.total){
			self.readPartFile(self.loaded);
		}
	}
	this.reader.onloadend = function(e){
		self.event.loadend && self.event.loadend.call(this, e);
	}
	this.reader.onabort = function(e){
		self.event.abort && self.event.abort.call(this, e);
	}
}
</script>
</body>
```

------

##### Websocket

Websocket是一种**网络协议**，是在http基础上做了优化的协议，与http无直接关系

和http区别：**连接方式**

和http共同：**TCP协议**



- HTTP  规定传输格式

  - 缺陷是通信只能由客户端发起,服务器不能实时发送新数据给客户端
  - Ajax轮训-定时器发送请求

- webSocket  解决实时问题

  - 发送一个请求, 以后就可以互通数据

  - 特点:
    建立在TCP协议之上**,服务器端实现较易**
    对HTTP有良好兼容性， 默认端口也是80 443，**握手阶段采用http协议，不易被屏蔽**
    可通过**各种http代理服务器**
    数据格式轻量,**性能开销小,通信高效**
    可发送文本, 可发送二进制数据
    **不受同源限制**,客户端可与任意服务器通信
    协议标识符为ws(加密wss) 服务器网址url

    ​	

事件:
​	onerror连接错误触发
​	onmessage接收数据时触发
优点:

1. 客户端与服务器都可以主动传送数据给对方
2. 不用频繁创建TCP请求\销毁请求, 减少网络宽带资源占用,节省服务器资源
3. 可跨域访问

```javascript
var socket = new WebSocket('ws://echo.websocket.org/');
console.log(socket.readyState);//0 未建立
socket.onopen = function(e){
	console.log(socket.readyState);//1 已建立可通信
	socket.send('Hello');
}
socket.onmessage = function(e){
	console.log(e, e.data);
	console.log(socket.readyState);//1
	socket.close();
	console.log(socket.readyState);//2 连接正在进行关闭
	socket.send('Hello2');//不行
}
socket.onclose = function(e){
	console.log(socket.readyState);//3 已经关闭
}
```

****

##### geolocation  devicemotion deviceorientation

API：应用程序接口,封装好的函数方法或属性事件

##### geolocation

获取当前地理位置信息【需要开启GPS】

```javascript
//查看所有功能
console.log(window.navigator.geolocation);
//应用
function success(e){
	console.log('success', e);
}
function fail(e){
	console.log('fail', e);
}
window.navigator.geolocation.getCurrentPosition(success, fail, options);
```

监视位置变化

```javascript
// watchPosition();
var options = {};
var watcher = window.navigator.geolocation.watchPosition(success, fail, options);
```

option参数

```javascript
option = {
    timeout: 1000,//请求超时时间 默认infinity
	enableHighAccuracy: true,//是否高精准度, 默认false
	maximumAge: 1000//过期时间 默认0[不断更新]
}
```

清除地理位置

```javascript
window.navigator.geolocation.clearWatch(watcher);
```

------

##### devicemotion

 监听加速度变化
属性: 

- accelerationIncludingGravity		重力加速度
- rotationRate(alpha, beta, gamma)    旋转速率
- interval获取时间间隔

**均为只读**

```javascript
//demo: 
var speed = 25;
var lastTime = 0,
	lastX = 0,
	lastY = 0,
	lastZ = 0;
window.addEventListener('devicemotion', function(event){
	console.log(event);
	demo.innerHTML = 'acceleration-x' + event.acceleration.x + '<br/>' + event.acceleration.y + '<br/>' + event.acceleration.z;
	var x = event.acceleration.x;
	var y = event.acceleration.y;
	var z = event.acceleration.z;
	var nowTime = (new Date()).getTime();
	if(nowTime - lastTime > 500){
		lastTime = nowTime;
		if(Math.abs(x - lastX) > speed || Math.abs(y - lastY) > speed ||  Math.abs(z - lastZ) > speed){
			alert('摇一摇');
			lastX = x;
			lastY = y;
			lastZ = z;
		}
	}
})
```

------

##### deviceorientation 

监听设备在方向上的变化

![设备方向监听](C:\Users\lenovo-pc\Desktop\渡一前端\总结笔记\H5\设备方向监听.png)

- z 0-360 (北0),  x -180~180,  y -90~90
- ios指北针: webkitCompassHeading     正北0 正东90 正南180 正西270
  ​		   webkitCompassAccuracy    指北针的精确度,表示偏差,一般为10

```javascript
	window.addEventListener('deviceorientation', function(e){
		demo.innerHTML = 'alpha: ' + e.alpha + e.beta + e.gamma;
	}, false)
```

****

##### iframe 互通数据

```javascript
// 父页面
<iframe src="http://localhost:8899/" frameborder="0"></iframe>

var oIframe = document.getElementsByTagName('iframe')[0];
oIframe.onload = function(){
	console.log(oIframe.contentWindow);
//父页面发送数据
	oIframe.contentWindow.postMessage({num:123},"http://localhost:8899/");
	// oIframe.contentWindow.postMessage({num:123},"*");跨域资源共享
}
//父页面接收数据
	window.addEventListener('message', function(e){
		console.log(e.data);//{son: 'son'}
	})
```

```javascript
// 子页面:
//子页面接收数据
window.addEventListener('message', function(e){
	console.log(e.data);//{num:123}
});
//子发送数据
window.onload = function(){
	window.parent.postMessage({son:'son'},"*");
}
```

------

##### 联动图表

**💗echarts**：图表网 数据可视化图表

1. 定宽高
2. 初始化              vazr myC = echarts.init(document.getElementById('wrap'));
3. 配置参数          option
4. 渲染                  myC.setOption(option);

```html
//demo
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>x</title>
	<style>
		.box1,.box2{
			width:400px;
			height:400px;
			display:inline-block;
			margin:30px;
			border:1px solid #000;
		}
	</style>
</head>
<body>
	<div class="box1"></div>
	<div class="box2"></div>
	<script src="jquery.js"></script>
	<script src="echarts.js"></script>
	<script>
		var myB1 = echarts.init($('.box1')[0]);
		var myB2 = echarts.init($('.box2')[0]);
		var alldata;
		function getData(url){
			$.ajax({
				type: 'GET',
				url: url,
				success: function(data){
					console.log(data);//查看返回数据
					alldata = data.sort(compare('num'));
					getBar();
				},
				error: function(){
					console.log('error');
				}
			});
		}
		getData('data.json');

		function compare(pro){
			return function(a, b){
				return a[pro] - b[pro];//小到大排序
			}
		}

		//生成柱形图
		function getBar(){
			var option = {
				title: {
		 			text: '2016~2018总销量',
		 			subText: '神话公司'
		 		},
		 		legend: {
		 			data: ['销量']
		 		},
		 		 xAxis: {
	            data: []//x轴
	       		 },
	        	yAxis: {},
	        	series: [{
	            name: '销量',
	            type: 'bar',
	            data: []//y轴
	        	}]
			};
			alldata.forEach(function(ele, index){
				option.xAxis.data[index] = ele.name;
				option.series[0].data[index] = ele.num;
			});
			myB1.setOption(option);

			getPie(alldata[0].year);
			myB1.on('click', function(e){
				console.log(e);//查看返回数据
				console.log(alldata[e.dataIndex].year);
				var data = alldata[e.dataIndex].year;
				getPie(data);
			});
		}

		function getPie(data){
			var option = {
				title : {
			        text: '年销量',
			        subtext: '神华集团',
			        x:'center'
			    },
			    tooltip : {
			        trigger: 'item',
			        formatter: "{a} <br/>{b} : {c} ({d}%)"
			    },
			    legend: {
			        orient: 'vertical',
			        left: 'left',
			        //数据
			        // data: ['直接访问','邮件营销','联盟广告','视频广告','搜索引擎']
			        data:[]
			    },
			    series : [
			        {
			            name: '销量',
			            type: 'pie',
			            radius : '55%',
			            center: ['50%', '60%'],
			            // data: [obj{value:ele.num name:ele.y}]
			            data:[
			                // {value:335, name:'直接访问'},
			                // {value:310, name:'邮件营销'},
			                // {value:234, name:'联盟广告'},
			                // {value:135, name:'视频广告'},
			                // {value:1548, name:'搜索引擎'}
			            ],
			            itemStyle: {
			                emphasis: {
			                    shadowBlur: 10,
			                    shadowOffsetX: 0,
			                    shadowColor: 'rgba(0, 0, 0, 0.5)'
			                }
			            }
			        }
			    ]
			};

			data.forEach(function(ele, index){
				console.log(ele);
				option.legend.data.push(ele.y);
				var obj = {};
				obj.value = ele.num;
				obj.name = ele.y;
				option.series[0].data.push(obj);
			});
			myB2.setOption(option);
		}
	</script>
</body>
</html>
```

data.json

```json
[
    {
        "name": "羽绒服",
        "num" : 300,
        "year": [
            {
                "y": 2016,
                "num": 60
            },
            {
                "y": 2017,
                "num": 100
            },
            {
                "y": 2018,
                "num":140
            }
        ]
    },
    ...
]
```

