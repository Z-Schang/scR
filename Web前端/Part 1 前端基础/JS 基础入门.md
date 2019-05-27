#### JavaScript 主要分为三个部分

- ECMA
- DOM
- BOM



#### ECMA

****

1. **JS 七种数据类型**

   基本类

   - Undefined
   - Null
   - Boolean
   - Number
   - String
   - Symbol 【 ES6 新增的一种原始数据类型，它的字面意思是：符号、标记。代表独一无二的值 】

   引用类

   - Object 【本质：一组无序的名值对组成的】

   **拓展**：typeof 返回值

   - string、number、boolean、undefined、object、function
   - null 是 object “空对象”

   null==undefined    true

   null===undefined  false

   **数据类型转换**

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

     - 除空格,0,null,未定义以外数字字符的boolean都为true

     - NaN 与其他数值进行比较的结果总是不相等的，包括它自身在内。因此，不能用 Number.NaN 比较来检测一个值是不是数字，而只能调用 isNaN() 来比较。while(k!=NaN) 判断是否为数字



2. **预编译**

   **JS引擎是怎样工作的，分为三步，各是什么？**

   JS是解释性语言，编译一行，执行一行。【汤姆猫游戏】

   JS引擎执行JS先后进行了：语义分析 => 预编译 => 解释执行【听 => 转换 => 说】



   **预编译发生在什么时候？在脚本代码script执行前，函数执行前都发生了什么？**

   JS引擎工作流程：

   引擎检查代码有无低级语法错误，然后**为变量和函数开辟内存空间**，最后解释执行。

   对于脚本代码执行前，预编译做两件事：

   1. 查找全局变量声明，变量名作全局变量属性，赋值undefined
   2. 查找函数声明，函数名作全局变量属性，赋值为函数引用【匿名函数不汇入预编译】

   对于函数执行前，预编译做4件事

   1. 创建AO对象
   2. 查找函数形参、函数内部变量声明，形参名和变量名作为AO对象属性，值为undefined
   3. 实形统一，实参赋给形参
   4. 查找函数声明，函数名作为AO对象属性，值为函数引用

   注：页面产生时创建了一个GO全局对象(window)，加载第一个脚本文件，加载完毕后分析语法是否合法，开始预编译，GO预编译完后开始执行，遇到执行函数才生成AO。若GO和AO有同个预编译项，AO执行时优先使用AO。

   ~~~javascript
   global = 100;
   function fn(){
   	console.log(global); 	//undefined, AO自己有global
   	global = 200;
   	console.log(global);	//200
   	var global = 300;
   }
   fn();
   var global;
   //GO(a : 5, test : func)
   var a = 5;
   function test(){
       a = 0;//这里改的是test()中AO的a
       alert(a);//AO{a:0}
       alert(this.a);//GO{a:5}【this指向window】
       var a;//这个提前，为AO声明变量
       alert(a);//AO{a:0}
   }
   test();//生成AO
   console.log(a);//GO{a : 5}
   ~~~



3. **作用域和闭包**

   **什么是上下文？分为哪几类？**

   上下文即整个脚本结构上各个模块的关系

   分为运行期上下文和执行期上下文两类

   运行期：存储运行期上下文集合[[scope]]

   执行期：执行期上下文对象集合，链式连接，叫作用域链，查找变量时由作用域链顶往下查

   **什么是闭包。运用闭包可以实现什么功能？**

   原理：闭包的技术原理就是利用作用域链是单向的这一特征。

   原句: JavaScript中的函数运行在它们被定义的作用域里，而不是它们被执行的作用域里

   理解: 内部函数被保存到外部生成闭包，导致原作用链不释放，内存泄漏。

   ​	所谓闭包，就是一个函数即使在自身作用域之外执行，也依然能记住并且能访问自己的自身作用域，这种用法就叫做闭包。

   可运用于

   - 共有变量
   - 存储结构
   - 模块化开发

   ~~~javascript
   // 经典实例：
   function tenli(){
       var arr =[];
       for(var i = 0; i< 10; i ++){
           arr[i] = function(){
               console.log(i);
           }
       }
       return arr;// 函数被保存到外面
   }
   var myArr = tenli();
   for(var i = 0; i < 10; i ++){
       myArr[i]();
       // 打印10个10
   }
   function ktenli(){
       var arr= [];
       for(var i = 0; i< 10; i ++){
           (function(j){
               arr[j] = function(j){
                   console.log(j);
               }
           })(i);	// 立即执行函数，破解闭包
       }
       return arr;
   }
   
   // 模块化开发
   var zsc = (function(){
       var name = "ZhangShuChang";
       function callName(){console.log(1)}
       return function(){
           callName();
       }
   })();
   zsc();//1
   ~~~

4. **对象**

   - 添加属性：MrZ.wife = "???";

   - 查找属性：console.log(MrZ.sex);

   - 更改属性：MrZ.health = 200;

   - 删除属性：delete MrZ.sex; 

     注：delete操作符可以从对象中删除属性，delete操作符只能作用在对象的属性上，对变量和函数名无效，且delete是不会直接释放内存的，只是间接的中断对象引用

     ~~~javascript
     (function(x){
         delete x;
         return x;
     })
     // delete x 没有意义，因为delete对变量无效
     ~~~

   - 构造对象：

     - var obj = {};

     - var obj = new Object();

     - function Person(mark){}  //**构造函数**的方法

       var person = **new Person**(mark1); 	//属性不互通

     - var person = Object.create(Person.prototype);

       注：不是所有对象都继承自Object.prototype，如 Object.create(null);

   - 深入构造函数

     内部原理：

     ~~~javascript
     function Person(name, sex){
         // var this;
         this.name = name;
         this.sex = sex;
         this.skill = function(){
             console.log("rock and roll");
         }
         // return this;  this 为构造函数自动生成的一个变量，存放属性和方法
     }
     Person.prototype.city = "GZ";
     var zsc = new Person("zsc", "male");
     // 每 new 一个对象，生成一个构造函数，每个构造函数都有一个原型
     // 原型：Parent.prototype【可生成通用属性】
     
     // 更改属性
     Person.prototype.city = "SH";
     // 最终 zsc 的 city 属性变为 SH
     
     // 更改整个原型对象
     Person.protoype = {
         city = "SZ";
     }
     // 最终 zsc 的city 属性还是为 SH
     // 相当于执行了 
     // Person.prototype = {city:"SH"}
     // __proto__ = Person.prototype;
     // Person.prototype = {city:"SZ"}  【完全新建了一个obj】
     //简单理解就是：
     // a = 1
     // b = a
     // a = 2 此时a怎么变与b值都无关
     ~~~

     原型：

     - 原型基于函数
     - prototype 是对象的共有祖先

     原型链：

     ![链条的全貌](E:\前端公开课\原型链\图例\链条的全貌.jpg)

     ~~~javascript
     // 通过原型进行方法重写
     Object.prototype.toString() = function(){
         retrun "toString is change";
     }
     ~~~

     constructor 构造器：

     用于标记构造函数，避免原型链错乱

     ~~~javascript
     function Person(){}
     Person.prototype = {
     	name : 'Niko',
     	age : 29,
     	job: 'enge',
     	constructor: Person
     }
     ~~~

   - 对象的链式调用

     ~~~javascript
     var obj = {
         run: function(){
             doSth;
             return this;
         },
         jump: function(){
             doSth;
             return this;
         }
     }
     obj.run().jump();  // 跑步后跳跃
     ~~~

   - 对象中的对象引用

     ~~~javascript
     var deng = {
         wife1 : {name : "xx"},
         wife2 : {name : "bb"},
         wife3 : {name : "aa"},
         wife4 : {name : "kk"},
         sayWife : function(num){
             return this['wife' + num];
         }
     }
     ~~~

   - 对象的遍历

     ~~~javascript
     for(var prop in obj){
         if(obj.hasOwnProperty(prop)){
             console.log(prop);
         }
     }
     // hasOwnProperty：用来检测一个对象是否含有特定的自身属性；和 in 运算符不同，该方法会忽略掉那些从原型链上继承到的属性。
     ~~~

5. **包装类**

   原始值要调用属性是需要包装的！

   - 原始值和引用值存储方式不同
   - 原始值无引用方法

   ~~~javascript
   var num = 4;
   num.len = 3;
   //new Number(4).len = 3;
   //delete
   console.log(num.len);
   //再次新建new Number(4).len，结果undefined
   		
   var str = "abcd";
   str.length = 2;
   //new String('abcd').length = 2
   //delete
   console.log(str);//abcd
   //new String('abcd').length;
   console.log(str.length);//4
   
   var str = "abc";
   str += 1;
   var test = typeof(str);
   if(test.length == 6){
   	test.sign = "typeof可能返回了String";
   	// newString(test).sign = "..."
   }
   // 这里又newString(test).sign
   console.log(test.sign);//undefined
   ~~~

6. **继承**

   - 传统原型链继承

     ~~~javascript
     Father.prototype.skill = "smoke";
     function Father(){};
     var fath = Father();
     Son.prototype = fath;
     function Son(){
         var son = new Son();
     }
     // 缺点：过多继承了没用属性(如smoke)
     ~~~

   - 借用构造函数

     ~~~javascript
     var Teacher = function(name,sex,sub){
         this.name = name;
         this.sex = sex;
         this.sub = sub;
     }
     function Student(name,sex,sub,grade){
         Teacher.call(this, name, sex, sub);
         this.grade = grade;
     }
     var stu = new Student();
     // 缺点：每次继承都要调用函数，性能低，且不能继承构造函数的原型
     ~~~

   - 共享原型

     ~~~javascript
     Father.prototype.money = "1亿";
     function Father(){};
     function Son(){};
     Son.prototype = Father.prtotoype;
     var son = new Son();
     // 缺点：不能随意修改自己的原型，相互影响
     ~~~

   - 圣杯继承

     ~~~javascript
     function sb(fath, son){
         function z(){};
         z.prototype = fath.prototype;
         son.prototype = new z();
         son.prototype.constructor = son;
     }
     ~~~

7. **关于this**

   - 函数预编译中，this => window
   - 全局作用域中，this => window
   - call / apply中，函数运行可以改变this指向
   - sth.dosth();   doSth中的this指向sth

   ~~~javascript
   function myFunc(zsc){
       //{__proto__: myFunc.prototype}
       //var this = Object.create(myFunc.prototype); 
       var a = 123;
       function b(){};
   }
   new myFunc();//此时上面发生
   ~~~

   习题部分，明天继续~

