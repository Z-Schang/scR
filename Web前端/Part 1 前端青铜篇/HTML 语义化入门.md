### **语义化网页结构**

****

**什么是语义化？**

简单理解，就是“说人话”！

对开发同事，对搜索引擎，都是这个道理。对于同事，语义化有利于理解各个标签含义，如果全篇是div span，那就像见面只会说“吃了没”，“天气不错”一样无聊！对于搜索引擎，如果没有用好各标签含义，那SEO也不知道你是想表达什么。

**语义化好处？**

1. 对人：利于开发调试，后期维护
2. 对SEO：利于搜索引擎优化，提高网站热度

几个方面来看待语义化

- 标题语义化：一个页面只有一个h1；h1~h6不要断层；不要用h1~h6定义样式(即不用来作为CSS样式)；不用div代替h1~h6

- 图片语义化：img 有两个重要属性alt和title；其中 alt 是用于图片描述，是给搜索引擎看的，当图片无法显示会显示alt文字；title 是给用户看的，鼠标悬停显示内容。
  *在H5中，引入了figure和figcaption两个元素增强图片语义化。

  ~~~html
  <figure>
  	<img src="" alt=""/>
  	<figcaption></figcaption>
  </figure>
  ~~~

- 表格语义化：table表格，caption标题，thead表头，tbody表身，tfoot表尾，tr行，th表头格，td表格

- 表单语义化：label 用于显示在输入控件旁边的说明性文字。

  ~~~html
  <input id="radioX" type="radio"/><label for="radioX">单选框</label>
  for：语义上绑定了label和表单元素，ID；增强了鼠标可用性，文本可点击。
  
  <fieldset>
  	<legend>表单组标题</legend>
  	...
  </fieldset>
  fieldset和legend：增强表单语义，可定义fieldset元素的disabled属性来禁用	整个组中的表单元素
  ~~~

- 其他语义化：

  ~~~html
  W3C规定
  <br/>只适用于段落中的换行，不能用于其他标签。
  <srtong>、<em>用于“强调”，在搜索引擎有一定权重。
  <del>定义被删文本，<ins>定义被更新的文本。
  <img>
  ①HTML使用img添加图片；
  ②通过CSS使用背景图片。
  如果图片作为HTML的一部分，想被搜索引擎识别，用 img；
  如果是修饰作用，不想被识别，就用背景图片 background-image
      
  最后提一嘴id 和 class的使用
  ID用于大结构和关键结构，如logo，导航，主题内容，底部信息栏等
  * 搜索引擎识别页面的结构是通过标签语义和ID属性是别的！
  ~~~

### 总结：

*仅仅为了改变样式，就用CSS来实现，不用HTML标签
*优先使用正确的语义化标签，在考虑用div、span标签
*样式只会改变标签的外观，不改变标签的语义



#### HTML拓展

**XHTML**：

- 标签必须闭合<br/>
- 属性、标签必须小写
- 标签属性必须带引号
- id 属性代替 name 属性



**HTML5：**

- 目前最新款的HTML，除了标签之外，还拥有SVG、canvas等技术。让HTML从“标记语言”转为“编程语言”

  特点

  - 化繁为简的文档声明：<!DOCTYPE html>
  - 标签不区分大小写，但实际开发建议小写
  - 允许属性不加引号，但实际开发还是要加
  - 允许部分属性属性值省略，如checked，readonly

