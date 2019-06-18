## HTML

- `<script>`、`<script async>`和`<script defer>`的区别

  script 标签在html文档中加载会阻塞

  使用 async 和defer 方法，可以让 script 异步加载，从而提高用户体验

  async 和 defer 的区别，在于defer 就算异步加载完，也等到html解析完毕再按顺序执行，而 async 异步加载完直接执行

  还有一个注意点就是 async 和 defer 只有在拥有 src 属性的 script 标签中才能生效。

- link 标签和 script 标签在文档中的位置问题

  link 一般置于 head 标签，因为这么做可以让页面逐步呈现，用户体验佳，若置于文档底部附件，可能会导致阻止渲染，会导致呈现空白页面或没有样式的内容

  script 一般置于 body 标签的末尾，因为脚本在下载和执行时会阻塞 html 解析，放在底部可以确保解析完后再下载执行脚本。

  但是，script 放在底部意味不能异步加载脚本，所以可以使用 defer 属性来异步加载 script

- 渐进式渲染

  用于提高网页性能，尽快呈现页面的技术

  - 图片懒加载，当用户滚动到图片部分时，js 将加载并显示图像
  - 使用延迟加载脚本或监听，如 document.onload
  - 异步加载 html 片段，把 html 拆分，通过异步请求，分块发送给浏览器。

- img 标签中 srcset 属性，浏览器处理过程？

  应用于响应式图片，使用 srcset 和 sizes 来提供不同尺寸的图像

  srcset 定义浏览器选择的图像集，图像大小

  sizes 定义媒体条件，选择第一符合要求的图像

  浏览器处理过程：

  1. 查看设备宽度
  2. 检查sizes列表中哪个媒体条件符合
  3. 查看槽的大小
  4. 加载 srcset 中的最接近槽大小的图像

  ~~~html
  <img srcset="elva-fairy-320w.jpg 320w,
               elva-fairy-480w.jpg 480w,
               elva-fairy-800w.jpg 800w"
       sizes="(max-width: 320px) 280px,
              (max-width: 480px) 440px,
              800px"
       src="elva-fairy-800w.jpg" alt="Elva dressed as a fairy">
  srcset参数：
  文件名，图像固有宽度
  sizes参数：
  媒体条件，图像填充槽的宽度
  ps:最后一个槽的宽度是没有媒体条件的，它是默认的，当没有任何一个媒体条件为真时，它就会生效。 当浏览器成功匹配第一个媒体条件的时候，剩下所有的东西都会被忽略，所以要注意媒体条件的顺序。
  ~~~

  或者使用 picture 标签

  ~~~html
  <picture>
    <source media="(max-width: 799px)" srcset="elva-480w-close-portrait.jpg">
    <source media="(min-width: 800px)" srcset="elva-800w.jpg">
    <img src="elva-800w.jpg" alt="Chris standing up holding his daughter Elva">
  </picture>
  ~~~


## CSS