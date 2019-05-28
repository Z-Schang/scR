### DOM

****

**什么是DOM？**

DOM，document object module 文档对象模型，是HTML和XML的标准编程接口。

**DOM继承树是怎样的？**

按原型链接如下：

- Object
- EventTarget
- Node
- Document
- HTMLDocument 
- document

其中：

1. Document.prototype 定义了 getElementsByName();
2. HTMLDocument.prototype 定义了 getElementsByTagName(); 
3. document.documentElement 代表html文档【整个html标签】

**JS如何脚本化CSS？**

- 脚本化CSS用于行间样式

- 格式必为驼峰命名

- 复合属性分开写(background border)

- 以字符串方式写入，且只有style可写

  PS：浮动脚本：sth.style.cssFloat;  避免命名冲突

****

#### DOM的相关方法集合：

- 获取HTML内容方法：

  ~~~javascript
  document.getElementById('');
  document.getElementsByTagName('');	// 类数组
  document.getElementsByName('');  //类数组，常用于form\img\ifarame
  document.getElementsByClassName();  //类数组
  //  静态类，不能动态获取的方法：
  document.querySelector();
  document.querySelectorAll(); //类数组
  ~~~

- 遍历结点方法：

  ~~~javascript
  sth.parentNode;  // 一个元素只有一个父节点【顶为document】
  sth.childNodes;  //子节点
  sth.firstChild;  //第一个子节点，(last最后一个)
  sth.nextSibling;  //下个兄弟节点
  
  // 遍历元素节点【IE9以下仅支持children】
  sth.parentElement;
  sth.children;  //类数组
  sth.firstElementChild / lastElementChild
  sth.nextElementSibling / previousElementSibling
  
  // 增删改查
  document.createElement('');  //创建元素结点
  document.createTextNode(''); //创建文本结点
  document.createComment('');  //创建注释结点
  sth.appendChild(span);  //类等push，剪切
  parent.insertBefore(a,b); //a插到b之前
  parent.removeChild(); //剪切出来
  parent.remove(); //销毁
  parent.replaceChild(a,b);//把b替换为a
  ~~~

  ~~~javascript
  div.firstChild.nodeName	//元素标签名，大写【只读】
  div.childNode[0].nodeValue //文本注释内容【读写】
  div.childNode[0].nodeType //结点类型
  	// 1 元素
  	// 2 属性
  	// 3 文本	
  	// 8 注释
  	// 9 文档【根节点】
  ~~~

  ~~~javascript
  // 习题，选出元素节点，不用 children
  function retChild(node){
      var temp = {
          length : 0,
          push : Array.prototype.push,
          splice : Array.prototype.splice//类数组转换【必写】
      };
      var child = node.childNode,
          len = child.length;
      for(var i = 0, i < len; i ++){
          if(child[i].nodeType === 1){
              temp.push(child[i]);
          }
      }
      return temp;
  }
  ~~~

- 元素节点的属性和方法：

  ~~~javascript
  // 属性：
  .innerHTML
  .innerText  // 老火狐没有
  .textContent  // 老IE没有
  // 方法：
  .setAttribute('class', 'demo');
  .getAttribute('id');
  .className = 'data';
  ~~~

  ~~~javascript
  // 给所有li标签添加属性this-name，赋值为该标签结点名字
  var allLi = document.getElementsByTagName('li');
  for(var i = 0; i < allLi.length; i ++){
      allLi[i].setAttribute('this-name', allLi[i].nodeName);
  }
  ~~~

- 窗口属性相关知识：

  ~~~javascript
  //获取滚动条滚动距离
  window.pageXoffset;
  // 兼容IE:
  document.body.scrollLeft/Top; //4.5.8
  document.documentElement.scrollLeft/Top; //6.7
  
  //获取可视区窗口属性
  window.innerWidht
  // 兼容IE：
  document.documentElement.clientWidth;
  
  文档类型检测：
  <!DOCTYPE html>
  标准模式
  混杂模式
  检测：document.compatMode 
  // CSS1：标准；BackCompat：怪异
  ~~~

- 元素属性相关知识

  ~~~javascript
  div.offsetWidth
  div.offsetTop //查看元素位置【对于无定位父级元素，返回相对文档坐标；父级有定位返回相对于有定位的父级坐标】
  div.offsetParent //返回有定位的父级
  ~~~

- 获得样式属性

  ~~~javascript
  window.getComputedStyle(div, "after").width;
  //兼容IE：
  sth.currentStyle.width
  实战中，一般通过className来切换样式。
  ~~~

****

#### DOM事件

事件是交互体验的核心！

事件绑定：

- onclick：高兼容(等同于写在HTML标签内)

- div.addEventListener("click",function(){},false);

  可绑定多个处理函数，但函数地址相同则只执行一次

- div.attachEvent("onclick", function(){{}});

  IE 专属，this指向window，函数地址相同则只执行一次

~~~javascript
删除事件：
sth.onclick = null;
sth,removeEventListener('click', test, false)
~~~

事件处理：

- 事件冒泡【自底而上，由子到父】

  不冒泡的事件：表单事件 ( 如focus / change / submit )

  取消冒泡：event.stopPropagation();  /  【IE】event.cancelBubble = true;  

- 事件捕获【自上而底，由父到子】

  设置捕获：sth.addEventListener(type, handle, true);

  div.setCapture();【IE】

  解除捕获：div.releaseCapture(); 【IE】

- 默认事件

  表单提交 / a跳转 / 右键菜单

  取消默认：return false

  ~~~javascript
  // 取消右键菜单
  document.oncontextmenu = function(){
      return false;
  }
  // 取消跳转
  // <a href="javascript:void()"></a>
  ~~~

- 事件源对象

  源对象获取：event.target  /  【IE】event.srcElement

- 事件委托

  原理是利用了事件冒泡，事件源对象进行处理

  ~~~javascript
  //ul中有无数li，要求点哪个打印哪个数字
  var ul = document.getElementByTagName('ul')[0];
  ul.onclick = function(e){
      var event = e || window.event;
      var target = event.target || event.srcElement;
      console.log(target.innerText);
  }
  ~~~

- 鼠标事件

  click = mouseup + mousedown

  mouseover = mouseenter

  mouseout = mouseleave

  移动端

  touchstart / touchmove / touchend

  DOM3规定，click只能监听左键，(0左 1中 2右)

  ~~~javascript
  // 鼠标点击停留300毫秒以下：打开，大于300毫秒：不打开
  var fTime = 0;
  var lTime = 0;
  var key = false;
  document.onmousedown = function(){
      fTime = new Date().getTime();
  }
  document.onmouseup = function(){
      lTime = new Date().getTime();
      if(lTime - fTime < 300){
          key = true;
      }
  }
  document.onclick = function(){
      if(key){
          console.log('open');
          key = false;
      }else{
          console.log('no-open');
      }
  }
  ~~~

- 键盘事件

  onkeypress  onkeydown  onkeyup

  down => press => up

  keydown 检测所有案件，操作类案件

  ~~~javascript
  // 检测按下的键盘ASCII码
  document.onkeypress = function(e){
  	console.log(String.fromCharCode(e.charCode));
  }
  ~~~

- 表单类操作

  oninput onblur change

  ~~~javascript
  var input = document.getElementByTagName('input')[0];
  input.oninput = function(e){
      console.log(this.value);//实时更新
  }
  input.change = function(e){
      console.log(this.value);//失焦触发
  }
  ~~~

- 事件分类

  ~~~javascript
  // 滚动执行
  window.onscroll = function(){
      console.log(window.pageXOffset + " " + window.pageYOffset)
  };
  // 加载完执行
  window.onload =function(){}
  ~~~
