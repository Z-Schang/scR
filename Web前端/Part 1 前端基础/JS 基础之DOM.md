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



****

**DOM的相关方法集合：**

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


