#### CSS 性能优化

背景缩写：

~~~css
background: url(xxx) no-repeat 80px 80px;
注:80px 80px 是定位
~~~



字体缩写

~~~css
font: "微软雅黑" 12px/1.5rem bold;
PS：
style("微软雅黑") 和 size(12x) 必写
1.5rem 指的是行高
~~~



- 在开发过程属性可以用纵向书写，整站发布的时候用工具压缩成横向书写方式。

  压缩工具：YUI Compressor（tool.oschina.net/jscompress）

  图片压缩工具：ImageOptim(需下载)

- 最后一个属性结尾分号不必要，url()中引号也可有可无。

- 浏览器解析选择器由右到左，

  解析效率：id > class > 元素 > 相邻 > 子 > 后代

  所以，不在id/class前加元素名；最好不超过3层，靠右的尽可能精确

- 使用 less / scss 与编译器大大提升开发效率

