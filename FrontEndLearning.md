# FrontEndLearning

## HTML 基础

### HTML 标签

水平线: `<hr>`, 用作分割内容;  
换行: `<br>`，不产生新段落换行;  
注释: `<!-- 注释内容 -->`;  
段落: `<p>`, 用作段落分割;  
文本格式化: `<b>`, 加粗;`<strong>`, 加粗;`<i>`, 斜体;`<em>`, 斜体;`<mark>`, 高亮;`<small>`, 小号字体;`<del>`, 删除线;`<ins>`, 下划线;`<sub>`, 下标;`<sup>`, 上标;  
区块: `<div>`，用作区块分割, 对分组内容进行格式化;`<span>`，用作行内分割, 对行内内容进行格式化;  
框架: `<iframe>`, 用于在网页中显示一个独立的 HTML 页面;  
链接: `<a href="url">`, 用于定义超链接, 其中 url 为#时表示当前页面的锚点。

### HTML 属性

常见的 HTML 属性有:  
class:为 HTML 元素定义一个或多个类名（引用样式表中的类）。  
id:定义 HTML 元素的唯一 id。  
style:规定元素的行内样式（inline style）。  
title:描述了元素的额外信息（作为工具条使用）。  
display: 规定元素应该生成的框的类型。
alt(图像):规定替换文本，当图像无法显示时显示该文本。  
download(链接):规定被下载的超链接目标。  
target(链接):规定在何处打开链接文档。有"\_blank"(新窗口)、"\_self"(当前窗口)、"\_parent"(父窗口)、"\_top"(顶层窗口)。

### HTML `<head>`部分

-   `<head>` 元素包含了所有的头部标签元素。
-   `<title>` 元素描述了文档的标题，包括浏览器工具栏、收藏夹默认和搜索引擎结果页上的标题。
-   `<base>` 元素为页面上的所有链接规定默认地址或默认目标，即定义所有标签默认的 target 属性。
-   `<link>` 元素定义文档与外部资源的关系, 比如引入 css 表等。
-   `<meta>` 元素提供有关页面的元信息，比如针对搜索引擎和更新频度的描述。`<meta>`常见的标签有: `charset`(定义文档的字符编码)、`keywords`(定义文档的关键词)、`description`(定义文档的描述)、`author`(定义文档的作者)、`viewport`(设置视口的宽度和缩放比例)。
-   `<style>` 元素定义文档的样式信息, 可以直接引入 css 文件。
-   `<script>` 元素用于定义客户端脚本, 可以直接引入 js 文件。

### HTML 表单和输入

表单和输入一般用于收集。  
action:规定当提交表单时向何处发送表单数据。当有 submit 按钮时，点击按钮会向 form 的 action 属性指定的地址发送表单数据。  
method: 规定用于发送表单数据的 HTTP 方法。常见的有 get 和 post。  
`<input>`: 用于表单输入。常见 type 有:text(文本域), password(密码域), radio(单选框), checkbox(复选框), submit(提交按钮), button(按钮), file(文件域)  
HTML5 新元素:  
`<datalist>`: 规定输入域的选项列表。  
`<keygen>`: 规定用于表单的密钥对生成器字段。  
`<output>`: 规定不同类型的输出，比如脚本的输出。

### HTML iframe

iframe 元素用于在网页中显示一个独立的 HTML 页面。

-   iframe 的优点:
    -   原封不动嵌入其他网页。
    -   可以嵌入多个网页。
-   iframe 的缺点:
    -   会增加服务器的 http 请求数。
    -   阻塞主页面的 onload 事件。
    -   与主页面共享连接池，会影响页面的并行加载。
    -   不利于 SEO。
    -   安全性方面，容易点击劫持、跨域资源控制等。
-   iframe 与父页面的通信:
    -   父页面发送消息：`iframe.contentWindow.postMessage()`
    -   iframe 接收消息：`window.addEventListener('message', function() {})`

### XHTML

XHTML 是更严格更纯净的 HTML 版本。其中的规则有:

-   开头必须是 `<!DOCTYPE html>`，声明文档类型
-   元素必须被正确地嵌套，必须始终关闭，区分大小写，必须有个根元素
-   属性必须小写，值必须用引号包围，属性值必须被赋值

### HTML5 新特性

1. 语义化标签。引入了新的语义化标签，如`<header>`、`<footer>`、`<nav>`、`<article>`、`<section>`、`<aside>`、`<figure>`、`<figcaption>`等，使得页面结构更加清晰。
2. 多媒体支持。引入了`<audio>`、`<video>`等标签，使得网页支持音频和视频。
3. 表单增强。引入了新的输入类型(如`email`、`url`、`number`、`range`、`date`、`time`、`color`)和属性(如表单验证`required`、`pattern`,表单自动完成`autocomplete`,表单自动聚焦`autofocus`)。
4. Canvas 和 SVG。引入了`<canvas>`和`<svg>`标签，使得网页支持绘图与动画。SVG 和 Canvas 的区别在于 SVG 是基于矢量的，而 Canvas 是基于位图的。
5. Web 存储。引入了`localStorage`和`sessionStorage`，能够比传统的 cookie 更好地存储数据。

#### HTML5 SVG 和 HTML Canvas

SVG 指可伸缩矢量图形 (Scalable Vector Graphics)。  
HTML SVG 用来定义用于网络的基于矢量的图形。  
xmlns: 定义命名空间。命名空间，是一个用来区分不同 XML 元素的独特标识符，一般默认为 "http://www.w3.org/2000/svg"。  
Canvas 是一个矩形区域，您可以控制其每一像素。Canvas 拥有多种绘制路径、矩形、圆、字符以及添加图像的方法。  
HTML Canvas 是使用 JavaScript 在 HTML 页面上绘图的一种方法。  
在 HTML 中，SVG 和 Canvas 都是用来绘图的，它们区别在于:SGG 不依赖分辨率，支持事件处理，适合大型渲染区域的应用，复杂度高会影响性能，不适合游戏;Canvas 依赖分辨率，不支持事件处理，文本能力渲染弱，能够以.png 或.jpg 格式保存图像，适合游戏密集型应用。

#### HTML5 应用缓存

HTML5 引入了应用程序缓存，这意味着 web 应用可进行缓存，并可在没有因特网连接时进行访问。  
缓存开启:在文档的 `<html>` 标签中包含 manifest 属性，指向一个 manifest 文件。

##### Manifest 文件:

CACHE MANIFEST: 在此标题下列出的文件将在首次下载后进行缓存。  
NETWORK: 在此标题下列出的文件需要与服务器的连接，且不会被缓存。  
FALLBACK: 在此标题下列出的文件规定当页面无法访问时的默认页面。

### Emmet

1. `!` 初始化 html 文件。
2. id: `element#id`表示`<element id="id"></element>`。
3. class: `element.classA.classB`表示`<element class="classA classB"></element>`。
4. 子元素: `parent>child`表示`<parent><child></child></parent>`。
5. 兄弟元素: `element1+element2`表示`<element1></element1><element2></element2>`。
6. 上级元素: `element^`表示`<element></element>`。
7. 重复元素: `element*3`表示`<element></element><element></element><element></element>`。
8. 属性: `element[attr="value"]`表示`<element attr="value"></element>`。
9. 文本: `element{content}`表示`<element>content</element>`。
10. 编号: `element$*3`表示`<element1></element1><element2></element2><element3></element3>`。
11. 分组: `element1>(element2>element3)+p`表示`<element1><element2><element3></element3></element2><p></p></element1>`。

## CSS 基础

### CSS 语法

CSS 规则由两个主要的部分构成:选择器，以及一条或多条声明。  
选择器:通常是您需要改变样式的 HTML 元素。
声明:包含了一个属性和一个值。属性和值之间用冒号分开，声明之间用分号分开。
注释:`/* 注释内容 */`。

### CSS 选择器

-   选择器类别
    -   id 选择器:`#id`，用于指定一个唯一的 HTML 元素。
    -   class 选择器:`.class`，用于指定一组 HTML 元素。其中，"."前面可以加上标签名，表示该标签下的 class。
    -   嵌套选择器:`p {}`，表示选择 p 标签下的元素; `.myclass p {}`，表示选择 class 为 myclass 的元素下的 p 标签; `p.myclass {}`，表示选择 class 为 myclass 的 p 标签。
    -   后代选择器:`div p {}`，表示选择 div 标签下的所有 p 标签。
    -   群组选择器:`h1, h2, h3 {}`，表示选择 h1、h2、h3 标签。
    -   子元素选择器:`div>p {}`，表示选择 div 下的直接子元素 p。
    -   相邻兄弟选择器:`div+p {}`，表示选择 div 后面的第一个 p 元素。
    -   后续兄弟选择器:`div~p {}`，表示选择 div 后面的所有 p 元素。
    -   属性和值选择器:`[attribute(=value)]`，表示选择具有指定属性值的元素。分隔符~=、\*=(包含指定值)、|=(值为指定值或一个单词内以指定值开头)、^=(值以指定值开头)、$=(值以指定值结尾)。
-   选择器优先级  
    !important > 内联选择器 > id 选择器 > class 选择器 > 标签选择器 > 通配符选择器 > 继承。

### CSS 创建

外部样式表:`<link rel="stylesheet" type="text/css" href="mystyle.css">`，在外部文件中定义样式。样式表应该以.css 扩展名保存。  
内部样式表:`<style>`，在`<head>`中定义样式。  
内联样式:`<p style="color: red;">`，在 HTML 元素中使用样式。  
优先权:内联样式 > 内部样式 > 外部样式 > 浏览器默认样式，并且是继承关系。

### CSS 计量单位

常见的计量单位有:

1. 绝对单位  
   px: 像素，绝对单位，不可伸缩。  
   pt: 物理长度单位，1pt=1/72in。
2. 相对单位
   rpx: 相对单位，相对于屏幕宽度的 1/750。
   em: 相对单位，相对于所在容器的 font-size 大小。  
   rem: 相对单位，相对于 html 的 font-size 大小。  
   %: 百分比，相对于父元素的大小。  
   vw/vh: 视窗宽度/视窗高度，相对于 viewpoint 的大小。  
   ch: 字符宽度，相对于 0 的宽度。
3. 有时会用到 calc()函数，用于动态计算长度值。如:`width: calc(100% - 100px);`。

### CSS 伪类和伪元素

1. 伪类是指已有元素处于某种特殊的状态时，为其添加对应的样式。

    常见的伪类:  
    a:link/visited/hover/active a 的四种状态。  
    _:first-child/last-child/nth-child(n) 选择第一个/最后一个/第 n 个子元素。  
    input:enabled/disabled/checked input 的三种状态。  
    _:lang(language) 选择指定语言中替换成符号的元素。  
    示例:

    ```css
    a:link {
        color: #ff0000;
    } /* 未访问的链接 */
    div:nth-child(2) {
        background: #ff0000;
    } /* 第二个 div 元素 */
    ```

2. 伪元素是指创建一些不在文档树中的元素，并为其添加样式。
   常见的伪元素:  
   ::first-line 选择元素的第一行。  
   ::first-letter 选择元素的第一个字母。  
   ::before 在元素之前插入内容。  
   ::after 在元素之后插入内容。  
   示例:
    ```css
    p::first-line {
        color: #ff0000;
    } /* 段落的第一行 */
    p::first-letter {
        font-size: xx-large;
    } /* 段落的第一个字母 */
    ```
    常见的伪元素属性:
    content: 插入内容。  
     counter-increment: 增加计数器。  
     counter-reset: 重置计数器。
    ```css
    p::before {
        content: "Read this: ";
        font-weight: bold;
    } /* 在 p 元素之前插入内容 */
    ```

### CSS 行内和块级

#### 空元素

-   空元素是指没有内容的元素，如`<br>`、`<hr>`、`<img>`、`<input>`、`<link>`、`<meta>`。

#### 行内元素(内联元素, inline)

-   行内元素不会独占一行，相邻的行内元素会排列在同一行，直到一行排不下才会换行。
-   行内元素的 height、width 属性无效，宽高由内容撑开。
-   常见的行内元素有 a、span、strong、em、img、input、label、select、textarea。

#### 块级元素(block)

-   块级元素会独占一行，相邻的块级元素会各自占一行。
-   块级元素的 height、width、margin、padding 属性都有效。
-   宽度默认是容器的 100%。
-   常见的块级元素有 div、h1~h6、p、ul、ol、li、dl、dt、dd、table、form。

#### 行内块级元素(inline-block)

-   行内块级元素会独占一行，但是不会换行，相邻的行内块级元素会排列在同一行。
-   常见的行内块级元素有 img、input。

#### 相互转换

行内元素可以和块级元素相互转换，通过 display 属性实现。

-   display: inline; 转块级元素
-   display: block; 转行内元素
-   display: inline-block; 转行内块级元素

### CSS 继承

-   无继承性的属性
    -   display
    -   部分文本属性(white-space)
    -   盒子模型属性(width, height, margin, padding, border...)
    -   背景属性(background-开头的属性)
    -   定位属性(position, float, clear, z-index...)
    -   生成内容属性(content)
-   有继承性的属性
    -   字体系列属性(font-开头的属性)
    -   大部分文本系列属性(text-开头的属性, text-align, text-indent, text-transform)
    -   其他文本系列属性(color, line-height, letter-spacing, word-spacing)
    -   其他属性(visibility, cursor, direction...)
-   所有元素可继承的属性
    -   visibility
    -   cursor
-   内联元素可继承的属性
    -   字体系列属性(font-开头的属性)
    -   除 text-indent 和 text-align 以外的文本系列属性
-   块级元素可继承的属性
    -   text-indent
    -   text-align

### 布局讲解

#### display

display 属性用于定义元素的显示方式。

-   inline: 行内元素，不换行，不可以设置宽高。
-   block: 块级元素，换行，可以设置宽高。
-   inline-block: 行内块级元素，不换行，可以设置宽高。
-   table: 表格元素，显示为表格。
-   table-cell: 表格单元格元素，显示为表格单元格。
-   none: 不显示。和 visibility:hidden 不同，none 会使元素不占据空间。
-   flex: 弹性布局，可以设置弹性容器的子元素如何排列。(重要!)
-   grid: 网格布局，可以设置网格容器的子元素如何排列。(重要!)

##### flex

flex 属性用于设置弹性容器的子元素如何排列。

-   flex-direction: 设置主轴的方向，row(默认值，水平方向)、row-reverse(水平方向，从右到左)、column(垂直方向)、column-reverse(垂直方向，从下到上)。
-   flex-wrap: 设置子元素是否换行，nowrap(默认值，不换行)、wrap(换行)、wrap-reverse(换行，从下到上)。
-   flex-flow: flex-direction 和 flex-wrap 的简写形式。

-   flex-grow: 设置子元素的拉升因子，默认为 0，即不侵占剩余空间。当 flex-grow 大于 0 时，以宽度为例，对应计算公式为:`totalWidth = ele.width + RemainWidth * ele.flow-grow / sumFlowGrow`。
-   flex-shrink: 设置子元素的收缩因子，默认为 1，即当空间不足时，子元素会收缩。当 sumFlexShrink 大于 1 时，以宽度为例，对应计算公式为:`totalWidth = ele.width - RemainWidth * (ele.flex-shrink * ele.width) / sum(width * flex-shrink)`。
-   flex-basis: 设置子元素的基准值，默认为 auto。当 flex-basis 为 0 时，表示计算收缩忽略自身宽高；当 flex-basis 为 auto 时，表示计算收缩时考虑自身宽高。
-   flex: flex-grow, flex-shrink, flex-basis 的简写形式。

justify-content 属性用于设置弹性容器的子元素在主轴上的对齐方式。

-   flex-start: 默认值，子元素在主轴上左对齐。
-   flex-end: 子元素在主轴上右对齐。
-   center: 子元素在主轴上居中对齐。
-   space-between: 子元素在主轴上两端对齐，子元素之间的间隔相等。
-   space-around: 子元素在主轴上均匀分布，子元素两侧的间隔相等。

align-items 属性用于设置弹性容器的子元素在交叉轴上的对齐方式。

-   flex-start: 子元素在交叉轴上顶部对齐。
-   flex-end: 子元素在交叉轴上底部对齐。
-   center: 子元素在交叉轴上居中对齐。
-   baseline: 子元素在交叉轴上以基线对齐。
-   stretch: 默认值，子元素在交叉轴上拉伸。

order 属性用于设置弹性容器的子元素的排列顺序。默认值为 0，值越小，排列越靠前。

max-width, min-width, max-height, min-height: 设置元素的最大宽度、最小宽度、最大高度、最小高度。可以控制 flex 收缩时的最大最小值。

#### grid

grid 属性用于设置网格容器的子元素如何排列。

-   grid-template-columns: 设置网格容器的列宽。常见的值有 auto(自动分配宽度)、repeat(n, value)(重复 n 次 value)、fr(剩余空间分配)。
-   grid-template-rows: 设置网格容器的行高。
-   grid-template-areas: 设置网格容器的区域。用''和空格分隔区域，用'.'表示空白区域。
-   grid-gap: 设置网格容器的行列间距。
-   grid-auto-flow: 设置网格容器的子元素如何排列。row(默认值，按行排列)、column(按列排列)、row dense(按行排列，紧凑排列)、column dense(按列排列，紧凑排列)。

-   grid-area: 设置网格子元素的区域, 起到了标签的作用。也可以是 grid-row-start, grid-column-start, grid-row-end, grid-column-end 的简写形式。
-   grid-column: 是 grid-column-start 和 grid-column-end 的简写形式。可以书写 [number] span, 表示占了[number]列。也可以书写 [number] / [number] 表示起始列和结束列。（列的[number]为结束的开始）。
-   grid-row: 同 grid-column，表示行。

#### position

position 属性用于定义元素的定位方式。

-   static: 默认值，元素按照文档流进行排列，不会被绝对定位或浮动元素覆盖。元素会忽略 top、right、bottom、left 等定位属性。
-   relative: 相对定位，元素相对于自身原来的位置进行定位。当元素设置了 top、right、bottom、left 属性时，元素会相对于原来的位置进行偏移。
-   fixed: 固定定位，元素相对于浏览器窗口进行定位，即使页面滚动，元素也不会移动。
-   absolute: 绝对定位，元素相对于最近的已定位(position 不为 static)祖先元素进行定位。如果没有已定位的祖先元素，则相对于最初的包含块进行定位。
-   sticky: 粘性定位，元素在相对定位和固定定位之间切换。当元素在视口内时，元素会相对于视口进行定位；当元素在视口外时，元素会相对于文档流进行定位。
-   inherit: 继承父元素的定位方式。

##### z-index

z-index 属性用于设置元素的堆叠顺序。

-   z-index 默认值为 0，值可以为负数，值越大，元素越靠前。
-   z-index 只对定位元素有效，即 position 属性不为 static 的元素。
-   z-index 只对同级元素有效，不同级元素之间的 z-index 无法比较。

#### overflow

overflow 属性用于设置元素的溢出内容的处理方式。

-   visible: 默认值，内容不会被修剪，会溢出。
-   hidden: 内容会被修剪，不会溢出。
-   auto: 自动决定是否溢出。

overflow: hidden 常见处理三种情况:

-   清除浮动: 一般而言，父级元素不设置高度时，高度由随内容增加自适应高度。当父级元素内部的子元素全部都设置浮动 float 之后，子元素会脱离标准流，不占位，父级元素检测不到子元素的高度，造成父级元素塌陷。此时可以通过设置 overflow: hidden 来清除浮动，使父级元素检测到子元素的高度。
-   遮罩：给一个元素中设置 overflow:hidden，那么该元素的内容若超出了给定的宽度和高度属性，那么超出的部分将会被隐藏，不占位。
-   解决外边距折叠：当两个相邻的块级元素的外边距相遇时，外边距会合并为一个外边距，取两者中的最大值。此时可以通过设置 overflow: hidden 来清除外边距折叠。

#### 盒模型

传统盒子模型:元素的从内到外依次是内容，内边距，边框，外边距。

-   内容(content):文本、图片等内容。
-   内边距(padding):内容和边框之间的距离。
-   边框(border):内边距和外边距之间的距离。
-   外边距(margin):边框和相邻元素之间的距离。

注意点：

-   传统盒子模型的宽度与高度为内容的宽度与高度（即 css 中设置的 width 和 height）+内边距+边框，而不包括外边距。由于传统盒子模型往往需要计算内边距和边框，因此 box-sizing 属性被引入。当 box-sizing 为 border-box 时，css 中设置的 width 和 height 包括内边距和边框，此时设置内边距和边框会缩减内容的宽度和高度。
-   外边距折叠：当两个相邻的块级元素的外边距相遇时，外边距会合并为一个外边距，取两者中的最大值。若是要清除外边距折叠，有这么几种方法：display 设置为 inline-block；设置 float 不为 none；设置 position 为 absolute 或 fixed。
-   margin 是设置元素的外边距，一般来说分为上下左右四个方向。margin 设置 1 个值，表示上下左右都是这个值；设置 2 个值，上下是第一个值，左右是第二个值；设置 3 个值，上是第一个值，左右是第二个值，下是第三个值；设置 4 个值，表示上右下左。一般来讲，margin 设置 auto 只能使元素水平居中，因为上下的 auto 值默认为 0。
-   padding, margin, border 都可以单独设置上下左右的值，如 padding-top, margin-left 等，并且可以为负值。

#### float 的使用与清除

浮动盒子是指元素脱离文档流，向左或向右移动，直到遇到包含块或另一个浮动元素的边缘。浮动元素会被文字识别并绕开，不会影响父盒子的宽高，所以会导致布局混乱。  
float 属性用于定义元素的浮动方式:

-   left: 元素向左浮动。
-   right: 元素向右浮动。
-   clear 属性用于控制清除元素的浮动方式，使元素不会被浮动元素覆盖。
-   left: 元素不允许左侧有浮动元素。
-   right: 元素不允许右侧有浮动元素。
-   both: 元素不允许左右两侧有浮动元素。

clear 属性用于清除浮动元素，避免浮动元素对父元素的影响。

-   none: 默认值，不清除浮动。
-   left: 不允许左侧有浮动元素。
-   right: 不允许右侧有浮动元素。
-   both: 不允许左右两侧有浮动元素。

浮动元素会脱离文档流，会影响父元素的高度，可能会导致父元素塌陷。下面为解决方法示例:

```html
<!-- 清除浮动一般是为了避免float属性无法撑开父元素，造成父元素塌陷的问题。 -->
<style>
    .test {
        float: left;
        height: 100px;
        width: 100px;
    }
</style>
<div class="outer">
    <div class="test"></div>
    <div class="test"></div>
</div>
<!-- 解决方法1 添加新元素-->
<div class="outer">
    <div class="test"></div>
    <div class="test"></div>
    <div style="clear:both;"></div>
</div>
<!-- 解决方法2 父元素使用overflow属性-->
<style>
    .outer {
        overflow: auto; // 或hidden
    }
</style>
<!-- 解决方法3 使用伪元素-->
<style>
    .outer::after {
        content: "";
        display: block;
        clear: both;
    }
</style>
```

#### BFC 与 IFC

##### BFC

BFC(Block Formatting Context) 块级格式化上下文，是一个独立的渲染区域，只有 Block-level Box 参与，它规定了内部的 Block-level Box 如何布局。简单来说，BFC 是一个完全独立的布局环境，让空间子元素不会影响到外布局。

-   BFC 的触发的简单条件：
    -   overflow: hidden
    -   display: inline-block
    -   position: absolute/fixed
    -   display: table-cell/flex/grid
-   BFC 规则
    -   BFC 就是一个块级元素，块级元素会在垂直方向一个接一个的排列
    -   BFC 就是页面中的一个隔离的独立容器，容器里的标签不会影响到外部标签
    -   垂直方向的距离由 margin 决定， 属于同一个 BFC 的两个相邻的标签外边距会发生重叠
    -   计算 BFC 的高度时，浮动元素也参与计算
-   BFC 的应用
    -   使用 Float 脱离文档流，高度塌陷
    -   Margin 边距重叠
    -   两栏布局

##### IFC

IFC(Inline Formatting Context) 行内格式化上下文。简单来说，IFC 的 line box 高度由其包含行内元素中最高的实际高度计算而来(不受竖直方向的 padding/margin 影响)。IFC 中的 line box 一般左右都贴紧整个容器，从而避免文字在行内元素中的溢出。

-   IFC 的触发条件：块级元素中包仅含内联元素
-   IFC 应用
    -   只计算水平方向的 padding, margin, border
    -   元素水平居中

#### 常见的居中方式

##### 垂直居中

-   绝对定位 + 负 margin
    ```css
    .parent {
        position: relative;
    }
    .child {
        position: absolute;
        top: 50%;
        transform: translateY(-50%);
    }
    ```
-   flex 布局
    ```css
    .parent {
        display: flex;
        align-items: center;
    }
    ```
-   table 布局
    ```css
    .parent {
        display: table-cell;
        vertical-align: middle;
    }
    ```
-   grid 布局
    ```css
    .parent {
        display: grid;
        place-items: center;
    }
    ```

##### 水平居中

-   行内元素
    ```css
    .parent {
        display: inline-block;
        text-align: center;
    }
    ```
-   绝对定位 + 负 margin
    ```css
    .parent {
        position: relative;
    }
    .child {
        position: absolute;
        left: 50%;
        transform: translateX(-50%);
    }
    ```
-   flex 布局
    ```css
    .parent {
        display: flex;
        justify-content: center;
    }
    ```
-   grid 布局
    ```css
    .parent {
        display: grid;
        justify-content: center;
    }
    ```
-   table 布局
    ```css
    .parent {
        display: table-cell;
        text-align: center;
    }
    ```
-   margin: auto
    ```css
    .parent {
        position: relative;
        margin: 0 auto;
    }
    ```

## JavaScript 基础

JavaScript 大小写敏感。
JavaScript 为弱类型语言，且支持动态类型，不需要声明变量的类型。
JavaScript 语句以分号结尾，可以不写，但不推荐。
在文本中可用\进行折行。

### JS 的输出

`document.write()`：向 HTML 输出流写内容。
`window.alert()`：弹出警告框。
`console.log()`：在控制台输出信息。
innerHTML：获取或替换 HTML 元素的内容。

### JS 基础语法

1. 变量定义：
    - var: ES5 定义变量，存在变量提升, 可以重复定义。
    - let: ES6 定义变量，不会变量提升，不可重复定义, 有块级作用域。
    - const: ES6 定义常量，不会变量提升，不可重复定义，有块级作用域，引用地址不可变。
2. 注释: 单行注释`//`，多行注释`/* */`。

#### JS 类型

1. 基本类型: number, string, boolean, null, undefined, Symbol(ES6), bigint(ES11)
2. 引用类型: object(array, Math, regexp, date...), function。
3. 2 种不包含任何值的类型: null, undefined。(NaN, Infinity 是 Number 类型)
4. 类型判断和类型转换
    - typeof 可以判断基本数据类型，但无法区分 Object 和 Array 类型。一般运用 Constructor 或者 instanceof 进行判断, 即`variable.constructor == Array`, `variable instanceof Array`。
    - 任意转字符串: `String()`, `toString()`, `+""`, `${}`。
    - 任意转数字: `Number()`, `parseInt()`, `parseFloat()`, `+`(置于字符串前)(无法转换则返回 NaN)。
    - 数字转整数: `Math.floor()`, `Math.ceil()`, `Math.round()`, `~~`, `parseInt()`。
    - 任意转布尔: `Boolean()`, `!!`。
    - json 转换: `JSON.stringify()`、`JSON.parse()`。
5. 原型链
    - 原型：每一个对象从被创建开始就和另一个对象相关联，从另一个对象继承属性和方法，则另一个对象就是原型。
    - 原型链：当读取实例对象的属性时，如果找不到，就会查找与该对象关联的原型对象中的属性，如果还查不到，就去找原型的原型，一直找到为止，如果还找不到就是 null（也是对象）。在此过程中，由互相关联的原型组成的链状结构就是 原型链。
    - 构造函数：创建对象的函数。
    - `__proto__`：通过实例对象的 `__proto__` 属性，可以获得对象的原型对象，等同于 Object.getPrototypeOf()。
    - prototype：每个构造函数都有一个 prototype 属性，指向一个原型对象，这个对象包含由特定类型的所有实例共享的属性和方法。
    - constructor：每个原型对象都有一个 constructor 属性，指向构造函数。
    - 构造函数，对象实例和原型对象(也是一个实例)的关系：
        - 构造函数 function Array(){} ---- let a = new Array(); ----> 对象实例 a
        - 对象实例 a ---- a.proto ----> 原型对象 Array.prototype
        - 对象实例 a ---- a.constructor ----> 构造函数 function Array(){} (实际上a没有constructor属性，而是通过原型链查找的)
        - 原型对象 Array.prototype ---- Array.prototype.constructor ----> 构造函数 function Array(){}
    - 而另一方面，构造函数实际上也是对象，是 Function 构造函数的实例，所以构造函数也有 proto 属性，即`Array.__proto__ === Function.prototype`。特殊的，`Function.__proto__ === Function.prototype`。

### JS 对象

1. JS 中对象的定义:
    ```JavaScript
    var person = {
        firstName: "John",
        lastName: "Doe",
        age: 50,
        eyeColor: "blue"
    };
    ```
2. 对象属性可以用`.`或`[]`进行访问。
3. 对象的创建:
    - `new`关键字: 通过构造函数创建对象，构造函数中的 this 指向新创建的对象。
    - `Object.create(proto, propertiesObject)`: 创建对象，指定原型和属性。只会继承原型对象的属性，不会继承构造函数的属性。
    - 字面量创建: 直接创建对象，不需要构造函数。
4. 常用的对象方法
    - Object.is(value1, value2): boolean，判断两个值是否相同。
    - Object.assign(target, source): typeof target，将 source 的属性复制到 target，浅拷贝。
    - Object.entries(obj): Array 和 Object.fromEntries(arr): Object，返回对象的键值对数组和数组的键值对对象，用于遍历对象。
    - Object.keys(obj): Array 与 Object.values(obj): Array，返回对象的键和值。注意，Object.keys()有个特殊的地方，如果属性名大于等于 0 的正整数，返回值按照从小到大排序；否则，返回值按照创建顺序排序。
    - Object.freeze(obj): Object，冻结对象，不可修改。
    - Object.getPropertyOf(obj): Object，返回对象的原型。
    - Object.create(proto, propertiesObject): Object，创建对象，指定原型和属性。
5. 常见的子对象
    - Math: 数学对象，包含数学常量和函数。
    - Date: 日期对象，用于处理日期和时间。
    - RegExp: 正则表达式对象，用于匹配字符串。
    - Array: 数组对象，用于存储多个值。
    - Function: 函数对象，用于定义函数。
    - Map: 映射对象，用于存储键值对。
    - Set: 集合对象，用于存储唯一值。

#### JS String

-   在 JS 中，字符串是一串字符，可以用单引号、双引号、反引号进行定义。
-   字符串长度用.length 获取。
-   字符串可以是对象，可以用`new String()`创建，此时该对象可以调用字符串方法。
-   字面量创建: `"", '', ``。
-   String 常用属性或方法:
    -   `length`: 字符串长度。
    -   `indexOf(str, start)`: 查找字符串中的子字符串，返回第一个匹配的位置。
    -   `slice(start, end)`: 提取字符串的一部分，从左到右，支持负数。
    -   `substring(start, end)`: 提取字符串的一部分，不支持负数。
    -   `replace(value, newValue)`: 替换字符串中第一个匹配的子字符串。
    -   `concat(str1, str2, ...strN)`: 连接两个或多个字符串。
    -   `trim()`: 去除字符串两端的空格。
    -   `charAt(index)`: 返回指定位置的字符。
    -   `includes(str)`: 判断字符串是否包含指定字符串。
    -   `split(separator, limit)`: 将字符串分割为字符串数组。

#### JS Array

-   数组是一种特殊的对象，用于存储多个值。
-   数组的元素可以是不同的数据类型，可以通过索引进行访问。
-   字面量创建: `[]`。
-   Array 常用属性和方法:
    -   同 String: `length`, `indexOf()`, `slice()`, `concat()`
    -   `join(separator)`: 将数组元素连接成字符串，用指定的分隔符分隔。
    -   `pop()`: 删除数组的最后一个元素。
    -   `push(item1, item2, ...itemN)`: 向数组的末尾添加一个或多个元素。
    -   `shift()`: 删除数组的第一个元素。
    -   `unshift(item1, item2, ...itemN)`: 向数组的开头添加一个或多个元素。
    -   `reverse()`: 颠倒数组中元素的顺序。
    -   `sort(compareFunction)`: 对数组元素进行排序。
    -   `splice(index, howmany, item1, item2, ...itemN)`: 删除从 index 开始的 howmany 个元素，并插入新元素。
    -   `forEach(function(item, index, arr))`: 用于调用数组的每个元素，并将元素传递给回调函数。
    -   `map(function(item, index, arr))`: 用于对数组的每个元素执行函数，并返回包含结果的数组。
    -   `filter(function(item, index, arr))`: 用于筛选数组的元素，并返回符合条件的元素。
    -   `reduce(function(total, item, index, arr), initialValue)`: 用于累加器，从左到右。
    -   `flat(depth)`: 用于将数组扁平化, 降维。

#### JS 运算符

特殊比较运算符: `==`和`===`，前者会进行类型转换，后者不会。(注意，NaN 不等于自身, +0 不等于-0, 两者用`===`会出错，可以用`Object.is()`进行比较)
逻辑运算符: `&&`、`||`、`!`。
扩展运算符: `...`，用于函数参数、数组、对象等, 用于对数组进行解构。
其他运算符: `in`——比较特殊，右边必须是对象（因此不能判断数组存在），判断对象是否具有指定的属性。
空值运算符：`??=`, `??`, `?.`——见 ES6 特性

#### JS 循环

类似 C，有 for、while、do-while、for-of 等循环, 写法也类似。
注意: js 中 for-in 用来遍历对象的属性，不适用于数组，数组使用 for-of 遍历。(for-in 在数组里遍历表示遍历下标)

若拷贝数组 arr,浅拷贝:

-   `arr.slice()`: 返回一个新数组，包含从开始到结束的元素。
-   `arr.concat()`: 返回一个新数组，包含原数组的值。
-   `[...arr]`: 返回一个新数组，包含原数组的值。
-   `Array.from(arr)`: 返回一个新数组，包含原数组的值。
    深拷贝:
-   `JSON.parse(JSON.stringify(arr))`: 返回一个新数组，包含原数组的值。
-   手写递归

#### JS 正则(RegExp)

JS 中正则表达式由 /pattern/modifiers(可选) 组成。  
正则一般在 search()、replace()、match()、test()、exec()等方法中使用。
常见的 modifiers(修饰符)有: i(执行对大小写不敏感的匹配)、g(执行全局匹配)、m(执行多行匹配)。

### JS this 关键字

this 关键字在不同的对象中有不同的含义:

-   默认绑定。单独使用，this 表示全局对象，默认绑定 window；
-   隐式绑定。对象调用，this 表示调用对象；
-   显示绑定。apply、call、bind，this 表示传入的对象（例外：传入为 null/unfefined 时，this 表示全局对象）；
-   new 绑定。构造函数调用，this 表示新创建的对象；
    优先级: new > 显示 > 隐式 > 默认。
    除此之外的特例：
-   箭头函数。this 表示上级作用域的 this 值。
-   间接函数引用。如`(obj1.foo = obj2.foo)()`，foo 中`console.log(this)`，此时类似直接调用，this 表示全局对象。

### JS 函数

JS 中函数也存在函数提升。
函数可以自调用，即在函数末尾添加(), 则会自动调用。

JS 比较重要的函数:

-   Object.assign(target, source): 用于将所有可枚举属性的值从一个或多个源对象复制到目标对象。
-   Object.keys(obj): 用于返回一个由给定对象的自身可枚举属性组成的数组。
-   Array.splice(start, deleteCount, item1, item2, ...): 用于向/从数组中添加/删除项目，然后返回被删除的项目。

#### JS 函数参数

显示参数: 通过函数名传递的参数。默认为 undefined。
隐式参数: 通过 arguments 对象传递的参数。arguments 对象是一个类数组对象，每个函数可以自由访问自身的 arguments 对象。即`arguments[n]`表示第 n 个参数。
JS 中参数传递是按值传递，如果传递的是对象，则传递的是对象的引用。

#### JS 闭包

一个函数和对其周围状态（lexical environment，词法环境）的引用捆绑在一起（或者说函数被引用包围）， 这样的组合就是闭包（closure）。也就是说，闭包让你可以在一个内层函数中访问到其外层函数的作用域。在 JavaScript 中，每当创建一个函数，闭包就会在函数创建的同时被创建出来。

-   闭包特点：
    -   让外部访问函数内部变量成为可能。
    -   避免使用全局变量，保护内部变量。
    -   使变量长期驻留在内存中。
-   闭包常见应用场景：

    -   **封装私有变量**

        ```javascript
        function createCounter() {
            let count = 0; // 私有变量

            return {
                increment: function () {
                    count++;
                    console.log(count);
                },
                decrement: function () {
                    count--;
                    console.log(count);
                },
                getCount: function () {
                    return count;
                },
            };
        }
        const counter = createCounter();
        counter.increment(); // 输出 1
        counter.decrement(); // 输出 0
        console.log(counter.getCount()); // 输出 0
        ```

    -   **创建模块**

        ```javascript
        const myModule = (function () {
            let privateVariable = "Hello";

            function privateMethod() {
                console.log("This is a private method.");
            }

            return {
                publicMethod: function () {
                    console.log(privateVariable);
                    privateMethod();
                },
            };
        })();

        myModule.publicMethod(); // 输出 "Hello" 和 "This is a private method."
        ```

    -   **保存外部函数的变量**
        ```javascript
        function outerFunction(x) {
            return function innerFunction(y) {
                return x + y;
            };
        }
        const add5 = outerFunction(5);
        console.log(add5(3)); // 输出 8
        ```
    -   **setTimeout 循环问题**
        ```javascript
        // 错误示例
        for (var i = 1; i <= 5; i++) {
            setTimeout(function () {
                console.log(i); // 输出 6 6 6 6 6
            }, 1000);
        }
        // 正确示例：使用闭包保存每次循环的 i 值
        for (var i = 1; i <= 5; i++) {
            (function (j) {
                setTimeout(function () {
                    console.log(j); // 输出 1 2 3 4 5
                }, 1000);
            })(i);
        }
        ```

#### JS 工厂函数

工厂函数是指返回对象的函数，它既不是类也不是构造函数。在 JS 中，任何函数都可以返回一个对象，当不使用 new 关键字时，却返回一个对象时，该函数就是工厂函数。

```JavaScript
// 工厂函数样例
const createPerson = (name, age) => {
    return {
        name: name,
        age: age
    };
};
```

### JS 异步编程

#### Promise

Promise: 用于异步编程，可以链式调用。

-   Promise 的构造:

```JavaScript
var promise = new Promise(function(resolve, reject) {
    // 异步操作
    if (/* 异步操作成功 */) {
        resolve(value);
    } else {
        reject(error);
    }
});
```

-   Promise 会返回一个 Promise 对象，可用以下几个方法进行处理:

    -   `then()`: 用于指定 resolve 和 reject 的回调函数。如果 then 中是一个值，那么会被忽略。
    -   `catch()`: 用于指定 reject 的回调函数。
    -   `finally()`: 用于指定不管 Promise 对象最后状态如何都会执行的操作。
    -   `resolve()`: 用于将 Promise 对象的状态改为 resolved。如果 resolve 中是一个值，那么会返回一个新的 Promise 对象。
    -   `reject()`: 用于将 Promise 对象的状态改为 rejected。如果 reject 中是一个值，那么会返回一个新的 Promise 对象。

-   Promise 常见的方法:
    -   `Promise.all([p1, p2, ...])`: 用于将多个 Promise 实例包装成一个新的 Promise 实例。
    -   `Promise.race([p1, p2, ...])`: 用于将多个 Promise 实例包装成一个新的 Promise 实例，只要有一个实例率先改变状态，新的实例就会跟着改变状态，返回值为第一个改变状态的实例的返回值。

#### 定时器

JS 提供一些原生的方法来实现定时器功能。

-   常见的定时器
    -   `setTimeout(function, delay)`: 用于在指定的延迟时间后执行函数。返回一个定时器 ID。
    -   `setInterval(function, delay)`: 用于在指定的时间间隔内重复执行函数。返回一个定时器 ID。
-   定时器的清除
    -   `clearTimeout(timerId)`: 用于清除定时器。
    -   `clearInterval(timerId)`: 用于清除定时器。
-   定时器的使用注意事项:
    -   定时器的延迟时间最短为 4ms，并且并非为严格的延迟时间，这是因为 JS 是单线程的，定时器的延迟时间是相对的，如果定时器里有大量的代码需要执行，那么定时器的延迟时间会被延长。
    -   定时器是异步的，定时器的回调函数会在当前执行栈清空后执行。
    -   定时器一般属于宏任务。
    -   `requestAnimationFrame()`是浏览器专门为动画设计的 API，相比于普通的定时器，它会保持刷新率与浏览器一致，避免了不必要的性能浪费。

#### defer

-   defer 是一个异步加载的标签属性，用于延迟加载脚本，等到文档加载完毕再加载脚本。
-   defer 属性只有在外部脚本文件时才有效，内部脚本文件不会延迟加载。
-   defer 和 async 的区别在于，defer 是按照文档顺序加载脚本，而 async 是异步加载脚本，不会阻塞页面渲染。

```html
<script
    src="demo_defer.js"
    defer
></script>
```

#### async 和 await

-   async 函数: 用于定义异步函数，返回一个 Promise 对象。await 关键字: 用于等待 Promise 对象的返回结果。
-   async 与 defer 区别在于，async 是异步加载，不会阻塞页面渲染，而 defer 是延迟加载，会等到文档加载完毕再加载脚本。
-   async 可以对 Promise 进行简化，使代码更加清晰，例子如下:

```JavaScript
function promiseTest(message) {
    return new Promise(function(resolve, reject) {
        setTimeout(function(){
            console.log(message);
            resolve();
        }, 1000);
    });
}
// before
promiseTest("First").then(function() {
    return promiseTest("Second");
}).then(function() {
    promiseTest("Third");
});
// after
async function asyncTest() {
    await promiseTest("First");
    await promiseTest("Second");
    await promiseTest("Third");
}
```

#### 异步代码的执行顺序

JS 的异步机制和事件循环有关。

##### 事件循环

事件循环是 JS 实现异步的机制，JS 是单线程的，通过事件循环实现异步。

1. 事件循环涉及三个存储区:
    - 函数调用栈: 存储函数调用。
    - 宏任务队列: 存储宏任务，执行顺序为 script(主代码)、setTimeout、setInterval、setImmediate、I/O、UI rendering。
    - 微任务队列: 存储微任务，如 process.nextTick、Promise、MutationObserver、async 函数中 await 后的函数。

压入队列顺序按照上述存储区依次执行，并且为先进后出，所以先执行当前宏队列的同步代码，然后执行该宏队列的微任务，接着执行下一个宏队列的同步代码，依次循环。

### JS 类

类的构造函数: `constructor`，用于初始化类的实例。类可以匿名创建。

#### 类继承

-   定义
    -   类: JS 的类其实是语法糖，本质上还是函数。但类不会提升。
    -   类继承: 使用`extends`关键字。子类构造函数中用`super()`可以调用父类的构造函数。
    -   getter 和 setter: 用于获取和设置对象的属性。
    -   静态方法: 使用`static`关键字，又称为类方法。
-   ES5 类继承的几种方式
    -   原型链继承: `Child.prototype = new Parent()`。缺点：无法向父类传递参数；子实例更改父实例的引用类型属性会影响所有实例。
    -   构造函数继承: `Parent.call(this, arguments)`。缺点：不可继承父类原型上的方法; 无法实现构造函数的复用。
    -   组合继承: 结合原型链继承和构造函数继承。缺点：调用两次父类构造函数。
    -   寄生组合继承: 使用 Object.create() 创建父类原型的副本。

### JS HTML DOM

DOM: Document Object Model，文档对象模型，是 HTML 和 XML 的应用程序接口。
DOM 是文档的逻辑结构，可以通过 JS 进行访问和修改。

#### DOM 节点创建

`document.createElement(tag)`: 创建一个新的元素节点。
`document.createTextNode(text)`: 创建一个新的文本节点。
`document.createAttribute(name)`: 创建一个新的属性节点。

#### DOM 查找

`document.getElementById(id)`: 通过 id 获取元素。
`document.getElementsByTagName(tag)`: 通过标签名获取元素。
`document.getElementsByClassName(class)`: 通过类名获取元素。
`document.querySelector(selector)`: 通过选择器获取元素。
`document.querySelectorAll(selector)`: 通过选择器获取所有元素，返回一个 NodeList(静态快照)。

#### DOM 修改

`element.innerHTML`: 获取或设置元素的内容。
`element.attribute`: 获取或设置元素的属性。
`element.style`: 获取或设置元素的样式。

#### DOM EventListener

EventListeners: 用于处理事件，可以通过`addEventListener()`添加事件监听器。
事件冒泡和事件捕获: 事件冒泡是从内向外传递，事件捕获是从外向内传递。通过设置`useCapture`参数可以选择是否使用事件捕获。
`element.addEventListener(event, function)`: 为元素添加事件监听器。
`element.removeEventListener(event, function)`: 为元素移除事件监听器。

#### DOM Collection

Collection: 一组元素，可以通过`document.getElementsByTagName()`等方法获取。
获取到的 Collection 是一个类数组对象，可以通过`item()`或`[]`进行访问，但不可以使用`push()`,`pop()`,`valueof()`等方法。

#### DOM 节点

节点: DOM 中的所有内容都是节点，节点可以是元素节点、属性节点、文本节点等。
`element.appendChild(node)`: 为元素添加子节点。
`element.insertBefore(newnode, existingnode)`: 在元素中插入新节点。
`element.removeChild(node)`: 删除元素的子节点。
`element.replaceChild(newnode, oldnode)`: 替换元素的子节点。
JS 可以通过一些方法获得 HTML DOM 节点列表(NodeList)，比如`childNodes`、`querySelectorAll()`等。
NodeList 与 Collection 区别:
NodeList 是动态的，当文档结构发生变化时，NodeList 会自动更新，相当于是对象的索引;而 Collection 是静态的，相当于是对象的克隆。

### JS 对象

JS 中对象是引用类型，可以通过`new Object()`或`{}`进行创建。
对象属性可以通过`.`或`[]`进行访问或设置。
对象构造器: 用于创建对象的函数，`function objectName(arg1, arg2, ...) {this.arg1 = arg1; ...}`。

### 可枚举和可迭代

-   定义
    -   可枚举: 对象的属性可以被枚举。一般由`defineProperty()`方法中的`enumerable`属性决定。
    -   可迭代: 对象可以被迭代。一般由`Symbol.iterator`属性决定。
-   区别
    -   可枚举: 主要用于对象的属性，可以通过`for...in`循环遍历。
    -   可迭代: 主要用于对象的值，可以通过`for...of`循环遍历。
-   常见的可枚举和可迭代对象:
    -   可枚举: 对象、数组等。
    -   可迭代: 数组、字符串、Map、Set。

### ES6 新特性

#### import 和 export

ES6 中新增了模块化的概念，可以通过`import`和`export`进行导入和导出。

-   默认导出: `export default function() {}`
-   命名导出: `export function fun1() {}`
-   两者区别:
    -   数量限制: 默认导出只能有一个，命名导出可以有多个。
    -   导入方式: 默认导出可以直接导入，命名导出需要使用`{}`导入。
    -   使用场景: 默认导出适用导出模块主要功能或核心功能，命名导出适用导出模块中的多个相关功能或辅助功能。
    -   可读性与维护性: 默认导出命名灵活，适合简单模块，命名导出可读性好，适合复杂模块。

#### 解构赋值

-   解构赋值: 用于从数组或对象中提取值，然后对变量进行赋值。
-   数组解构: `let [a, b, ...rest] = [1, 2, 3, 4, 5]`
-   对象解构: `let {a} = {a: 1, b: 2}`。
-   默认值: `let {a = 1} = {variable}`。

#### 空值运算符

-   `??=`: 空值赋值运算符，仅在变量为 null 或 undefined 时赋值。
-   `??`: 空值合并运算符，当左侧为 null 或 undefined 时，返回右侧的值，否则返回左侧的值。
-   `?.`: 可选链运算符，用于判断对象的属性是否存在，如果不存在则返回 undefined，避免报错。

#### 生成器

function\* 用于定义生成器函数，生成器函数返回一个生成器对象。

```JavaScript
function* fun() {
    yield 1;
    yield 2;
    yield 3;
}

let generator = fun();
for (let value of generator) {
    console.log(value);
}
```

#### 箭头函数

-   箭头函数(Lambda 函数): ES6 新增的函数定义方式，可以简化函数定义。箭头函数无法提升。
-   省略: 当只有一个参数时，可以省略括号; 当只有一个表达式时，可以省略大括号和 return；当只返回一个对象时，用括号包裹对象，不需要 return。
-   示例: `let fun = (a, b) => a + b`;
    ```JavaScript
    // 普通函数
    var x = function(x, y) {
        return x * y;
    }
    // 箭头函数
    var x = (x, y) => x * y;
    ```
-   箭头函数注意点：
    -   箭头函数没有自己的 this，会继承父作用域的 this，且无法改变。
    -   箭头函数没有 arguments 对象，可以使用 rest 参数代替。
    -   箭头函数没有 prototype 属性，无法作为构造函数使用。
    -   箭头函数无法作为 Generator 函数使用。

#### 模板字符串

-   模板字符串: 用于创建多行字符串，可以嵌入变量。
-   模板字符串使用反引号`进行定义，变量使用'${}'进行替换，同时还支持多行文本。

```JavaScript
let name = "John";
let age = 30;
let text = `My name is ${name}, I am ${age} years old.`;
```

#### 元编程

元编程是指在运行时操作代码的能力，ES6 提供了一些元编程的方法。元编程可以总结为两类：反射和代理。

##### Proxy

Proxy 用于定义基本操作的自定义行为，可以用于拦截对象的操作。类似于猴子补丁。

-   Proxy 的构造: `let proxy = new Proxy(target, handler)`。
-   Proxy 的 handler 构造: `let handler = {get: function(target, prop, receiver) {}}`。
-   Proxy 的 handler 方法: `get`, `set`, `apply`, `construct` 等等。
-   Proxy 的设计目的：
    -   用于拦截对象的操作，可以用于实现数据绑定、数据校验、数据转换等。
    -   用于实现一些默认行为，可以用于实现默认值、类型检查等。

```JavaScript
let handler = {
    get: function(target, name) {
        return name in target ? target[name] : 37;
    }
};
let p = new Proxy({}, handler);
p.a = 1;
console.log(p.a, p.b); // 1, 37
```

##### Reflect

Reflect 是一个内置对象，提供了一系列静态方法，用于替代一些操作符和方法。

-   Reflect 的方法: `Reflect.get(target, name, receiver)`。
-   Reflect 的方法: `Reflect.set(target, name, value, receiver)`。
-   Reflect 的设计目的:
    -   将 Object 对象的一些明显属于语言内部的方法（比如 Object.defineProperty），放到 Reflect 对象上。
    -   修改某些 Object 方法的返回结果，让其变得更合理。
    -   让 Object 操作都变成函数行为。
    -   让 Proxy 对象可以方便调用 Reflect 对象的方法，完成默认行为，作为修改行为的基础。(代理陷阱)

```JavaScript
// 普通调用
console.log(obj.attr);
console.log(arr[0]);
// Reflect 调用
console.log(Reflect.get(obj, 'attr'));
console.log(Reflect.get(arr, 0));
// 代理陷阱
const proxy = new Proxy(obj, {
    set(target, key, value, receiver) {
        const res = Reflect.set(target, key, value, receiver);
        if(res) console.log(`Set ${key} success`);
        return res;
    }
});
```

### 作用域

-   作用域: 变量的可访问范围。作用域最大的用处就是隔离变量，避免变量冲突。
-   词法作用域和动态作用域:
    -   词法作用域: 变量的作用域在代码编写时就已经确定了，JS 是词法作用域，通过作用域链实现。__函数的作用域由函数定义时的位置决定__。
    -   动态作用域: 变量的作用域在运行时确定。___函数的作用域由函数调用时的位置决定__。
-   作用域类型:
    -   全局作用域: 在任何地方都可以访问的变量。
    -   函数作用域: 在函数内部定义的变量，只能在函数内部访问。
    -   块级作用域: 在代码块内部定义的变量，只能在代码块内部访问。
-   var, let, const 的区别:
    -   var: 声明的变量是全局作用域或函数作用域，存在变量提升，允许重复声明。
    -   let: 声明的变量是块级作用域，不存在变量提升，不允许重复声明。
    -   const: 声明的变量是块级作用域，不存在变量提升，不允许重复声明，且必须初始化。

### JS 执行上下文
    执行上下文是 JS 代码执行的环境，包含了变量、函数、对象等信息。执行上下文分为三种:全局执行上下文、函数执行上下文、eval 执行上下文。
#### 执行栈
    执行栈，也叫调用栈，具有后进先出（LIFO）的特性。每当一个函数被调用时，都会创建一个新的执行上下文，并将其压入栈中。当函数执行完毕后，执行上下文会被弹出栈。
-   变量提升: js引擎执行时是一段段执行的，对于函数和变量的声明会提前到当前作用域的顶部进行处理。其中，函数声明提升优先级高于变量声明，但是函数赋值表达式不会提升。
#### 全局执行上下文
    全局执行上下文是 JS 代码执行的第一个上下文，包含了全局变量和函数。全局上下文只有一个，在浏览器中是 window 对象，在 Node.js 中是 global 对象。全局上下文中的变量和函数可以在任何地方访问。
#### 函数执行上下文
    函数执行上下文是函数被调用时创建的上下文，包含了函数的参数、变量、作用域链等信息。执行过程包括三个阶段:
-   执行上限文会激活变量对象(VO)，创建作用域链，确定 this 的指向。
-   代码执行阶段会执行函数体内的代码，创建活动对象（AO），并将参数和变量添加到 AO 中。AO包括：
    -   arguments: 存储函数参数的对象。
    -   变量对象: 存储函数内的变量声明和函数声明。
    -   this: 指向当前执行上下文的对象。
-   回收阶段: 当函数执行完毕后，执行上下文会被弹出栈，释放内存。


## TypeScript 基础

-   TypeScript 是 JavaScript 的超集，可以编译为纯 JavaScript。
-   TypeScript 支持类型注解、接口、类、模块等。
-   TypeScript 为静态类型，优势在于:
    -   可以尽早发现错误与 bug；
    -   减少了复杂的错误处理；
    -   将数据与行为分离；
    -   有利于代码重构。

以下重点叙述 TypeScript 区别于 JavaScript 的部分。

### TypeScript 变量声明

-   TypeScript 支持变量声明时指定类型，如`let name: string = "John";`。
-   联合类型: 变量可以有多种类型，如`let name: string | number = "John";`。
-   类型断言: 用于告诉编译器变量的类型，有两种形式，`<type>value`和`value as type`。
-   非空断言: 用于告诉编译器变量不为空，如`let stu{ name!: string; } = {}; console.log(stu!.name);`。
-   类型推断: TypeScript 可以根据变量的值推断变量的类型, 如果未申明类型，则默认类型为 any。

### TypeScript 类型

-   js继承: TypeScript 支持js所有的基本类型和引用类型。   
-   大写与小写: TypeScript 中大小写敏感。对于基本类型， 大写表示包装对象与字面量都能使用，小写只能使用字面量。对于`Object`，表示广义对象，兼容基本类型和object类型。在实际开发中，更倾向于使用小写字母的类型，一是基本类型中字面量应用更广泛，并且ts将很多内置方法限制于字面量类型，二是`Object`过于宽泛，可能会导致类型不安全。
-   值类型: 值类型是指变量存储的是值本身。当使用`const`时，ts会自动推断为值类型。
-   联合类型: 联合类型是指变量可以有多种类型，如`let name: string | number = "John";`。
-   交叉类型: 交叉类型是指将多个类型合并为一个类型，如`type Person = {name: string} & {age: number}`。基本类型的联合意义不大，会被推断为`never`类型。
-   `tuple` 和 `array`:
    -   `tuple`: 元组类型，表示一个固定长度的数组，每个元素可以是不同类型，如`let tuple: [string, number] = ["John", 30];`。
    -   `array`: 数组类型，表示一个可变长度的数组，所有元素必须是相同类型，如`let array: number[] = [1, 2, 3];`。
-   `never`, `any`, `unknown`:
    -   `never`: 表示永远不会有值的类型，通常用于函数抛出异常或无限循环的情况。`never`可以被赋值给任何类型。
    -   `any`: 表示任意类型，可以是基本类型、对象、数组等。使用 any 会失去类型检查。`any`会让失去ts使用的价值，一般应用于适配老旧代码或ts无法推断类型的场景。
    -   `unknown`: 表示未知类型，类似于 any，但 unknown 需要进行类型检查后才能使用。`unknown`无法赋值给其他类型，也无法调用方法，进行运算也是有限的，需要经过“类型缩小”才可使用，可以被视为`any`的安全替代品。
-   枚举类型: 枚举类型是 TypeScript 中的一种特殊类型，用于定义一组命名的常量。可以使用数字或字符串作为枚举值，如`enum Color {Red, Green, Blue}`。`Enum`的成员默认不需要赋值，系统会自动从零开始递增赋值; 若需要赋值，则类型只能为`number`或`string`。


### TypeScript 函数

-   TypeScript 可以指定返回值类型，如`function fun(): number {return 1;}`。
-   TypeScript 可以指定参数类型，如`function fun(name: string): void {console.log(name);}`; 可以指定可选参数，如`function fun(name?: string): void {console.log(name);}`；可以指定默认参数，如`function fun(name: string = "John"): void {console.log(name);}`；可以指定剩余参数，如`function fun(...name: string[]): void {console.log(name);}`。
-   TypeScript 支持函数重载，即可以定义多个同名函数，但参数类型或个数不同。

### TypeScript interface 和 type

-   接口: 用于定义对象的类型，可以包含属性、方法、索引签名等。
-   接口定义: 使用`interface`关键字，如`interface Person {name: string; age: number;}`。
-   接口可以设置数组的索引值和元素类型，如`interface StringArray { [index: number]: string; }`。
-   接口也支持继承，并且支持多继承，如`interface Person extends Name, Age {}`。

-   类型：用于定义类型别名，可以包含基本类型、联合类型、元组、对象等。
-   类型定义: 使用`type`关键字，如`type Name = string;`。
-   类型别名可以定义联合类型，如`type Name = string | null;`。
-   类型别名可以定义元组，如`type Name = [string, number];`。

-   类型和接口的区别:

    -   语法方面有区别:

        ```TypeScript
        // type 定义
        type Name = string

        // interface 定义
        interface Name {
            name: string
        }
        ```

    -   实现继承方面有区别:

        ```TypeScript
        // type 继承 type
        type Person = { name: string }

        type Student = Person & { stuId: number }

        // interface 继承 interface
        interface Person {
            name: string
        }

        interface Student extends Person {
            stuId: number
        }
        ```
    -   属性映射方面有区别:

        ```TypeScript
        interface Person {
            name: string
            age: number
        }
        // type 映射
        type PersonCopy = {
            [K in keyof Person]: Person[K]
        }

        // interface 无法映射
        ```

    -   type 可以定义基本类型、联合类型、元组、对象等，而 interface 只能定义对象类型。
    -   interface 可以定义多个同名接口，会自动合并，而 type 不行。

-   使用建议：
    -   官方推荐使用 interface，其他无法满足需求的情况下用 type。但是因为联合类型和交叉类型是比较常用的，所以避免不了大量使用 type 的场景，一些复杂类型也需要通过组装后形成类型别名来使用。
    -   如果想保持代码统一，还是可选择使用 type。通过上面的对比，type 其实可涵盖 interface 的大部分场景。
    -   对于 React 组件中 props 及 state，推荐使用 type，这样能够保证使用组件的地方不能随意在上面添加属性。如果有自定义需求，可通过 HOC（高阶组件）二次封装。
    -   编写三方库时使推荐使用 interface，其更加灵活自动的类型合并可应对未知的复杂使用场景

### TypeScript 对象

-   TypeScript 中对象的定义: 使用`{}`，如`let person = {name: "John", age: 30};`。
-   类型模版: TypeScript 的对象必须是特定类型的实例，因此直接使用未申明的对象会报错，可以使用类型模版进行定义，如`let person: {name: string, age: number} = {name: "John", age: 30};`。

### TypeScript 泛型

-   泛型: 用于创建可重用的组件，一个组件可以支持多种类型。泛型可以设置默认类型，如`function identity<T = string>(arg: T): T {return arg;}`。
-   泛型标识符: TypeScript 有各种泛型标识符，`T`表示泛型类型，`K, V`表示键值对，`E`表示数组元素类型, `R`表示返回类型, `U, V`表示第二、第三个泛型类型参数。
-   函数泛型: 使用泛型来创建一个可以支持多种类型的函数。
    ```TypeScript
    // 泛型函数
    function identity<T>(arg: T): T {
        return arg;
    }
    // 泛型函数 变量定义 写法1
    let myIdentity: <T>(arg: T) => T = identity;
    // 泛型函数 变量定义 写法2
    let myIdentity: {<T>(arg: T): T} = identity;
    ```
-   接口泛型: 使用泛型来创建一个可以支持多种类型的接口。
    ```TypeScript
    // 泛型接口
    interface GenericIdentityFn<T> {
        (arg: T): T;
    }
    ```
-   泛型约束: 用于限制泛型类型。
    ```TypeScript
    // 泛型约束
    interface Lengthwise {
        length: number;
    }
    function logLength<T extends Lengthwise>(arg: T): void {
        console.log(arg.length);
    }
    logLength("Hello"); // 5
    logLength(10); // Error: Argument of type 'number' is not assignable to parameter of type 'Lengthwise'.
    ```


### TypeScript 命名空间

命名空间: 用于组织代码，避免命名冲突。
命名空间定义: 使用`namespace`关键字，如`namespace Validation {export function isLetter(s: string): boolean {return /^[A-Za-z]+$/.test(s);}}`。
命名空间引用: 使用`/// <reference path="Validation.ts" />`引用命名空间。

### TypeScript 模块

模块: 可以更换的代码块，可以导入和导出。
导入模块: 使用`import`关键字，如`import {name} from "./module";`。
导出模块: 使用`export`关键字，如`export {name};`。

### TypeScript 声明文件

声明文件: 用于描述已有代码的类型，以便 TypeScript 编译器识别(特别是第三方库)。
声明文件定义: 使用`declare`关键字，如`declare var jQuery: (selector: string) => any;`。
声明文件后缀: 一般为`.d.ts`。

## jQuery

jQuery 是一个快速、简洁的 JavaScript 库，可以简化 HTML 文档的遍历、事件处理、动画等操作。

### jQuery 语法

基础语法: `$(selector).action()`，`$`是 jQuery 的标识符，`selector`是选择器，`action()`是要执行的动作。
选择器: jQuery 中的选择器与 CSS 选择器类似，可以通过标签名、类名、id 等进行选择。
选择器常见有如下几种:

-   元素选择器: `$("p")`，选择所有`<p>`元素。
-   id 选择器: `$("#test")`，选择 id 为 test 的元素。
-   类选择器: `$(".test")`，选择所有 class 为 test 的元素。
-   属性选择器: `$("[href]")`，选择所有带有 href 属性的元素。
-   多元素选择器: `$("p, .test")`，选择所有`<p>`元素和 class 为 test 的元素。
-   创建元素: `$("<p></p>")`，创建一个`<p>`元素。

### jQeury 链

jQuery 链: jQuery 方法可以链接在一起，形成链式调用。
例如，`$("p").hide().show().addClass("test")`。

### jQuery DOM 操作

jQuery 中的 DOM 操作与 JS 类似，但是更加简洁。
获得内容或属性: `text()`、`html()`、`val()`、`attr()`。
设置内容或属性: `text("content")`、`html("content")`、`val("content")`、`attr("attribute", "value")`。
添加元素: `append()`、`prepend()`(内部)、`after()`、`before()`(外部)。
删除元素: `remove()`、`empty()`。
设置 CSS: `addClass()`、`removeClass()`、`toggleClass()`。

### jQuery AJAX

jQuery 中的 AJAX 操作更加简洁，可以通过`$.ajax()`进行异步请求。
常见的方法:
`$(selecotr).load(url, data, callback)`: 从服务器加载数据，并把返回的数据放入元素中。
`$.get(url, data, callback)`: 通过 HTTP GET 请求载入信息。
`$.post(url, data, callback)`: 通过 HTTP POST 请求载入信息。
`$.ajax({url: url, type: type, data: data, success: function(result){}})`: 通过 HTTP 请求载入信息。

## 补充知识

### CSS 预处理器

CSS 预处理器指的是用一种专门的编程语言，为 CSS 增加了一些编程的特性，将其编译成正常的 CSS 文件。  
常见的 CSS 只是标记语言，不支持变量、嵌套、混合、继承等功能，而 CSS 预处理器可以支持这些功能。  
常见的 CSS 预处理器有两大类：基于 Ruby 的 Sass 和基于 JavaScript 的 Less。

#### CSS 预处理器的优缺点

-   优点:
    -   提高 CSS 代码的可维护性，可读性。
    -   提供了变量、嵌套、混合、继承等功能。
    -   可以使用函数来减少重复代码。
-   缺点:
    -   需要预编译，增加了额外的工作量。
    -   语法不同，需要学习新的语法。
    -   可能会增加项目的复杂度。

#### Sass 和 Less 的对比

-   Sass:
    -   语法更加严谨，功能更加强大。
    -   有两种语法格式，Sass 基于缩进，SCSS 改进了 Sass 的语法，更接近 CSS。
    -   支持条件语句、循环语句等。
-   Less:
    -   语法更接近 CSS，学习成本更低。
    -   功能相对较少，但是足够日常使用。
    -   使用 JavaScript，可以在客户端和服务端运行。
-   区别:
    -   变量:Sass 使用`$`，Less 使用`@`。混合:Sass 使用`@mixin`，Less 使用`.mixin()`。
    -   Sass 在服务端处理，以往在 Ruby 环境下，现在则是 Dart Sass/Node Sass。Less 是在客户端处理，所以常规需要引入 less.js 到浏览器中。
    -   Sass 支持条件语句、循环语句等，Less 不支持。
    -   Sass 工具库为 Compass，该工具库提供了大量的模块和模板，可以直接使用。Less 则有 UI 组件库 Bootstrap，该组件库是比较流行的 UI 组件库。

### PostCSS

PostCSS 是一个用 JavaScript 工具和插件转换 CSS 代码的工具。  
PostCSS 的工作原理是将 CSS 解析成抽象语法树，然后对抽象语法树进行处理，最后再转换成 CSS。  
一般来说，CSS 预处理器和 PostCSS 只需要选择一个即可，因为 PostCSS 可以实现 CSS 预处理器的大部分功能。  
常见的 PostCSS 插件有：Autoprefixer、postcss-cssnext、postcss-pxtorem 等。

#### 常见应用场景

-   自动添加浏览器前缀: Autoprefixer 可以根据 Can I Use 网站的数据，自动添加浏览器前缀。
-   使用未来的 CSS 语法: PostCSS 可以使用未来的 CSS 语法，如变量、嵌套、混合等。
-   压缩 CSS 代码: PostCSS 可以压缩 CSS 代码，减少文件大小。
-   提高 CSS 代码的可维护性: PostCSS 可以使用插件来提高 CSS 代码的可维护性，如使用 BEM 规范等。
-   提高 CSS 代码的性能: PostCSS 可以使用插件来提高 CSS 代码的性能，如使用 CSS Modules 等。

### Web Components

-   Web Components 是一种用于创建可重用的自定义元素的技术，可以用于创建自定义的 HTML 元素、模板、样式和脚本。
-   Web Components 由四个主要技术组成: - Custom Elements: 用于创建自定义元素。 - Shadow DOM: 用于封装元素的样式和脚本，不允许外部访问。 - HTML Templates: 用于定义模板。 - HTML Imports: 用于导入模板。
    样例如下:

```html
<user-card
    image="https://semantic-ui.com/images/avatar2/large/kristy.png"
    name="User Name"
    email="yourmail@some-email.com"
></user-card>

<template id="userCardTemplate">
    <style>
        :host {
            display: flex;
            align-items: center;
            width: 450px;
            height: 180px;
            background-color: #d4d4d4;
            border: 1px solid #d5d5d5;
            box-shadow: 1px 1px 5px rgba(0, 0, 0, 0.1);
            border-radius: 3px;
            overflow: hidden;
            padding: 10px;
            box-sizing: border-box;
            font-family: "Poppins", sans-serif;
        }

        .image {
            flex: 0 0 auto;
            width: 160px;
            height: 160px;
            vertical-align: middle;
            border-radius: 5px;
        }

        .container {
            box-sizing: border-box;
            padding: 20px;
            height: 160px;
        }

        .container > .name {
            font-size: 20px;
            font-weight: 600;
            line-height: 1;
            margin: 0;
            margin-bottom: 5px;
        }

        .container > .email {
            font-size: 12px;
            opacity: 0.75;
            line-height: 1;
            margin: 0;
            margin-bottom: 15px;
        }

        .container > .button {
            padding: 10px 25px;
            font-size: 12px;
            border-radius: 5px;
            text-transform: uppercase;
        }
    </style>

    <img class="image" />
    <div class="container">
        <p class="name"></p>
        <p class="email"></p>
        <button class="button">Follow John</button>
    </div>
</template>

<script>
    class UserCard extends HTMLElement {
        constructor() {
            super();
            var shadow = this.attachShadow({ mode: "closed" });

            var templateElem = document.getElementById("userCardTemplate");
            var content = templateElem.content.cloneNode(true);
            content
                .querySelector("img")
                .setAttribute("src", this.getAttribute("image"));
            content.querySelector(".container>.name").innerText =
                this.getAttribute("name");
            content.querySelector(".container>.email").innerText =
                this.getAttribute("email");

            shadow.appendChild(content);
        }
    }
    window.customElements.define("user-card", UserCard);
</script>
```

### Map 和 Object

Map 和 Object 非常相似，但它们仍然存在一些区别：

1. 额外的键: Map 默认情况不包含任何键，而 Object 包含原型链上的键。
2. 键的类型: Map 的键可以是任何类型，而 Object 的键只能是 String 或 Symbol。
3. 键的顺序: Map 保留插入顺序，而 Object 顺序不保证(自然数会被排序)。
4. 大小: Map 有 size 属性，Object 只能用 Object.keys(obj).length 来获取大小。
5. 遍历: Map 可以直接遍历(输出为[key, value])，Object 需要先转换为数组再遍历。
6. 性能: Map 在插入和删除元素时性能更好。

### JS 内存泄漏

JS 内存泄漏有以下几种情况:

1. 无用的全局变量: 全局变量不会被回收。
2. 闭包: 闭包中的变量会一直存在。
3. 未被清理的定时器: 定时器不会被自动清理。
4. 未被销毁的事件监听器: 事件监听器不会被自动销毁。
5. DOM 引用: 未被销毁的 DOM 引用会导致内存泄漏。
6. 循环引用: 循环引用会导致内存泄漏。

### call, apply 和 bind

-   call, apply 和 bind 都是用于改变函数的 this 指向。
-   call, apply 和 bind 无法改变箭头函数的 this 指向。
-   call, apply 和 bind 的区别：
    -   call 和 apply 都是立即执行函数，bind 是返回一个新函数。
    -   call 传递参数 arg1, arg2, ...; apply 传递参数数组[arg1, arg2, ...]。

### 模块化

#### CommonJS 规范

CommonJS 规范加载模块是同步的，所以只有加载完成才能执行后面的操作。

-   CommonJS 的特点:
    -   导入与加载使用的是 module, exports, require。多值用 module.exports，单值用 exports。
    -   所有代码都运行在模块作用域，不会污染全局作用域。
    -   模块可以多次加载，但只会在第一次加载时运行一次，然后缓存。
-   CommonJS 的应用场景：
    -   Node.js 是 CommonJS 规范的主要实践者。
    -   浏览器端使用 Browserify、Webpack 等工具可以使用 CommonJS 规范。

#### AMD 模块化
AMD (Asynchronous Module Definition) 是一种异步模块定义规范，主要用于浏览器端的模块化开发。

-   AMD 的特点:
    -   导入与加载使用的是 define 和 require。
    -   支持依赖管理，可以指定模块的依赖。
    -   支持回调函数，可以在模块加载完成后执行回调函数。
-   AMD 的应用场景:
    -   主要用于浏览器端的模块化开发，如 RequireJS。（目前已经逐步被 ES6 模块化取代。）
    -   可以与 CommonJS 规范结合使用，如使用 curl.js。

#### ES6 模块化

ES6 模块化是异步加载的，可以在任何地方引入模块。

-   ES6 模块化的特点:
    -   ES6 模块化不是对象，而是通过 export 和 import 来导出、导入模块。
    -   ES6 模块化是编译时加载，效率更高。
    -   ES6 模块化是动态引用，可以实现按需加载。
-   ES6 模块化的应用场景:
    -   主流的 ES6 模块化一般应用于前端开发，通过 Webpack、Rollup 等工具进行打包。
    -   Node.js 在 v13.2.0 版本开始支持 ES6 模块化。

#### ES6 模块化和 CommonJS 的区别

-   CommonJS 是同步加载，ES6 模块化是异步加载。
-   CommonJS 是运行时加载，ES6 模块化是编译时加载。
-   CommonJS 是值拷贝，ES6 模块化是值引用。
-   循环加载时，CommonJs 返回的是未完成状态的 exports 对象，ES6 模块化返回的是一个引用对象。

### 浏览器相关

#### cookie, sessionStorage 和 localStorage 的区别

1. 存储位置
    - cookie: 存储在客户端。
    - sessionStorage: 存储在客户端。
    - localStorage: 存储在客户端。
2. 存储大小
    - cookie: 4KB。
    - sessionStorage: 5MB。
    - localStorage: 5MB。
3. 数据有效期
    - cookie: 可以设置过期时间。
    - sessionStorage: 仅在当前会话有效。
    - localStorage: 永久有效。
4. 作用域不同
    - cookie: 同源的所有窗口。
    - sessionStorage: 同源的当前窗口。
    - localStorage: 同源的所有窗口。

#### 浏览器输入 URL 后发生了什么

1. **URL 解析**: 浏览器会解析 URL，提取协议、主机、端口、路径、查询参数、哈希等信息。
2. **缓存检查**: 浏览器会检查缓存，如果有缓存且未过期，则直接从缓存中获取资源。
3. **DNS 解析**: 浏览器首先会将 URL 转换为 IP 地址。这个过程称为 DNS 解析。浏览器会先检查本地缓存，如果没有找到，则会向 DNS 服务器发送请求，获取对应的 IP 地址。
4. **建立 TCP 连接**: 获取到 IP 地址后，浏览器会与服务器建立 TCP 连接。这个过程包括三次握手：
    - 客户端发送一个 SYN 包到服务器。
    - 服务器接收到 SYN 包后，返回一个 SYN-ACK 包。
    - 客户端接收到 SYN-ACK 包后，再发送一个 ACK 包，连接建立完成。
5. **发送 HTTP 请求**: TCP 连接建立后，浏览器会向服务器发送一个 HTTP 请求。请求包括请求行、请求头和请求体。请求行包含请求方法（如 GET、POST）、请求 URL 和 HTTP 版本。请求头包含一些元数据，如 User-Agent、Accept 等。请求体包含请求的具体数据（如 POST 请求的数据）。
6. **服务器处理请求**: 服务器接收到请求后，会根据请求的内容进行处理。服务器可能会查询数据库、调用其他服务等，最终生成响应数据。
7. **服务器返回响应**: 服务器处理完请求后，会返回一个 HTTP 响应。响应包括状态行、响应头和响应体。状态行包含 HTTP 版本、状态码和状态描述。响应头包含一些元数据，如 Content-Type、Content-Length 等。响应体包含具体的响应数据（如 HTML 页面、JSON 数据等）。
8. **浏览器渲染页面**: 浏览器接收到响应后，会根据响应的数据渲染页面。这个过程包括以下步骤：
    - **解析 HTML**: 浏览器会解析 HTML 文档，构建 DOM 树。
    - **解析 CSS**: 浏览器会解析 CSS 文件，构建 CSSOM 树。
    - **构建渲染树**: 浏览器会将 DOM 树和 CSSOM 树结合，构建渲染树(Render Tree)。
    - **布局(回流)**: 浏览器会根据渲染树计算每个元素的位置和大小。
    - **绘制**: 浏览器会将元素绘制到屏幕上。
9. **执行 JavaScript**: 浏览器在解析 HTML 和 CSS 的过程中，会遇到 JavaScript 文件。浏览器会暂停解析，下载并执行 JavaScript 文件。JavaScript 可以操作 DOM 和 CSSOM，修改页面内容和样式。
10. **建立后续连接**: 如果页面中包含其他资源（如图片、视频、CSS 文件、JavaScript 文件等），浏览器会继续发送请求，下载这些资源，并进行渲染。
11. **关闭连接**: 页面加载完成后，浏览器会关闭与服务器的连接。这个过程包括四次挥手：
    - 客户端发送一个 FIN 包到服务器。
    - 服务器接收到 FIN 包后，返回一个 ACK 包。
    - 服务器发送一个 FIN 包到客户端。
    - 客户端接收到 FIN 包后，返回一个 ACK 包，连接关闭。
12. **用户交互**: 页面加载完成后，用户可以与页面进行交互。浏览器会根据用户的操作（如点击、输入等）发送请求，更新页面内容。

#### 浏览器如何渲染页面

1. **解析 HTML**: 浏览器会解析 HTML 文档，构建 DOM 树（Document Object Model）。DOM 树是 HTML 文档的结构化表示，每个 HTML 标签都是一个节点，节点之间有父子关系。
2. **解析 CSS**: 浏览器会解析 CSS 文件，构建 CSSOM 树（CSS Object Model）。CSSOM 树是 CSS 样式的结构化表示，每个 CSS 规则都是一个节点，节点之间有父子关系。
3. **构建渲染树**: 浏览器会将 DOM 树和 CSSOM 树结合，构建渲染树。渲染树是页面的可视化表示，每个节点都是一个可见元素。渲染树不包含不可见的元素（如 `<head>` 标签）和被隐藏的元素（如 `display: none` 的元素）。
4. **布局（回流）**: 浏览器会根据渲染树计算每个元素的位置和大小，这个过程称为布局或回流。布局是一个自上而下的过程，从根节点开始，依次计算每个节点的位置和大小。
5. **绘制（重绘）**: 浏览器会将渲染树的每个节点绘制到屏幕上，这个过程称为绘制或重绘。绘制是一个自下而上的过程，从叶子节点开始，依次绘制每个节点。
6. **执行 JavaScript**: 浏览器在解析 HTML 和 CSS 的过程中，会遇到 JavaScript 文件。浏览器会暂停解析，下载并执行 JavaScript 文件。JavaScript 可以操作 DOM 和 CSSOM，修改页面内容和样式。
7. **处理用户交互**: 页面加载完成后，用户可以与页面进行交互。浏览器会根据用户的操作（如点击、输入等）发送请求，更新页面内容。
8. **增量布局和绘制**: 当页面内容或样式发生变化时，浏览器会进行增量布局和绘制。增量布局和绘制只会重新计算和绘制发生变化的部分，而不是整个页面。
9. **优化**: 浏览器会对渲染过程进行优化，以提高渲染性能。例如，浏览器会将多个布局和绘制操作合并，减少回流和重绘的次数。

#### 浏览器垃圾回收机制

##### 基本介绍

浏览器具有自动垃圾回收机制，其原理是：垃圾回收器会定期扫描内存中的对象，找到不再使用的对象，然后释放这些对象占用的内存。

##### 标记清除和引用计数

垃圾收集器必须跟踪哪个变量引用了哪个对象，对于不再有用的对象打上标记，然后将其回收。而标记清除和引用计数是两种最常见的标记策略。

-   标记清除（Mark-and-Sweep）: 标记清除算法是一种通过标记对象是否可达来判断对象是否存活的算法。当变量进入环境时，这个变量被标记为“进入环境”。当变量离开环境时，这个变量被标记为“离开环境”。垃圾回收器会定期扫描内存中的对象，找到不再使用的对象，然后释放这些对象占用的内存。
-   引用计数（Reference Counting）: 引用计数算法是一种通过计算对象的引用次数来判断对象是否存活的算法。当对象被引用时，引用计数加一；当对象被释放时，引用计数减一。当引用计数为零时，对象被回收。引用计数算法的缺点是循环引用问题，即两个对象互相引用，导致引用计数永远不为零，对象无法被回收。

##### GC 优化

垃圾回收(Garbage Collection)时，需要停止 JavaScript 的执行，这会导致页面卡顿。为了减少页面卡顿，浏览器会对垃圾回收进行优化。

-   分代回收（Generational Collection）: 分代回收是一种通过将对象分为新生代和老生代来提高垃圾回收效率的算法。新生代中的对象通常存活时间较短，老生代中的对象通常存活时间较长。垃圾回收器会根据对象的存活时间将对象分配到不同的代中，然后对不同的代采用不同的回收策略。
-   增量回收（Incremental Collection）: 增量回收是一种通过将垃圾回收过程分为多个阶段来减少页面卡顿的算法。垃圾回收器会将垃圾回收过程分为多个阶段，然后在每个阶段执行一部分垃圾回收工作，最终完成整个垃圾回收过程。##### 基本介绍
    浏览器具有自动垃圾回收机制，其原理是：垃圾回收器会定期扫描内存中的对象，找到不再使用的对象，然后释放这些对象占用的内存。

#### 浏览器安全

1. **XSS（Cross Site Scripting）**
    - XSS 是一种跨域脚本攻击，攻击者通过在网页中插入恶意脚本，获取用户的敏感信息。
    - 本质原因：网站没有对用户输入的内容进行过滤和转义。
    - 攻击类型
        - 存储型 XSS: 攻击者将恶意脚本存储在目标服务器的数据库中，当用户请求包含恶意脚本的页面时，脚本会被执行。常见于论坛发帖、商品评论等。
        - 反射型 XSS: 攻击者将恶意脚本作为请求的一部分发送到服务器，服务器处理请求并将恶意脚本反射回用户浏览器执行。常见于搜索引擎跳转、短链接等。
        - DOM 型 XSS: 攻击者将恶意脚本嵌入到页面的 DOM 中，通过 JavaScript 动态修改页面的 DOM 结构并执行恶意脚本。常见于搜索框搜索、页面跳转等。
    - 防御措施
        - 输入过滤: 对用户输入的内容进行过滤，移除或转义特殊字符。
        - 输出转义: 对用户输入的内容进行转义，将特殊字符转换为 HTML 实体。
        - CSP（Content Security Policy）: 设置 Content-Security-Policy 头，限制页面加载的资源和执行的脚本。
2. **CSRF（Cross Site Request Forgery）**
    - CSRF 是一种跨站请求伪造攻击，攻击者通过利用用户的登录状态，伪造用户的请求，执行恶意操作。
    - 本质原因：网站没有对请求来源进行验证。
    - 攻击类型
        - GET 请求: 攻击者通过 URL 发送 GET 请求，执行恶意操作。
        - POST 请求: 攻击者通过表单提交 POST 请求，执行恶意操作。
    - 防御措施
        - 同源检测: 在请求中添加 Origin 头，验证请求来源是否合法。
        - CSRF Token: 在请求中添加 CSRF Token, 即一种随机生成的令牌，在网站发起请求时，需要验证 CSRF Token 的有效性。
        - Cookie 双重验证: 在请求中添加 Cookie，验证 Cookie 的有效性。
3. **中间人攻击**
    - 中间人攻击是一种通过拦截和篡改网络通信数据的方式，获取用户的敏感信息。
    - 本质原因：网络通信数据没有加密。
    - 防御措施
        - HTTPS 加密: 使用 HTTPS 协议加密通信数据，保护用户的敏感信息。
        - HSTS（HTTP Strict Transport Security）: 设置 Strict-Transport-Security 头，强制使用 HTTPS 协议通信。
        - 双向认证: 服务器和客户端都需要验证对方的身份，确保通信双方的安全性。
4. **网络劫持**
    - 网络劫持是一种通过篡改 DNS 解析、劫持 IP 地址等方式，将用户的网络流量重定向到攻击者控制的服务器上。
    - 本质原因：网络流量没有加密。
    - 攻击类型
        - DNS 劫持: 攻击者通过篡改 DNS 解析，将用户的域名解析到攻击者控制的服务器上。
        - HTTP 劫持: 攻击者通过篡改 HTTP 请求和响应，将用户的网络流量重定向到攻击者控制的服务器上。

#### 进程和线程

1. 概念
    - 进程: 进程是程序的一次执行过程，是系统进行资源分配基本单位。
    - 线程: 线程是进程的一个实体，是 CPU 调度基本单位。
2. 区别
    - 调度对象: 进程是资源分配的基本单位，线程是 CPU 调度的基本单位。
    - 资源拥有: 进程拥有资源，线程共享资源。
    - 独立性: 进程是独立的，线程是依附于进程的。
    - 开销: 进程切换开销大，线程切换开销小。
3. 浏览器的多进程
    - 浏览器是多进程的，主要包括 1 个浏览器主进程、1 个 GPU 进程、1 个网络进程、多个渲染进程、多个插件进程等。
        - 浏览器主进程: 主要负责界面显示、用户交互、子进程管理、网络资源管理等。
        - GPU 进程: 主要负责 3D 绘制、页面绘制等。
        - 网络进程: 主要负责网络资源的加载。
        - 渲染进程: 主要负责将 HTML、CSS 和 JavaScript 转换为用户可以与之交互的页面。
        - 插件进程: 主要负责插件的运行。
    - 渲染进程的线程主要包括 GUI 渲染线程、JS 引擎线程、事件触发线程、定时器线程、异步 HTTP 请求线程等。
        - GUI 渲染线程: 负责渲染浏览器界面，解析 HTML、CSS，构建 DOM 树和 Render 树，布局和绘制。
        - JS 引擎线程: 负责处理 JavaScript 脚本。GUI 与 JS 引擎是互斥的，当 JS 引擎执行时 GUI 线程会被挂起。
        - 事件触发线程: 负责将事件放入事件队列中，用来控制事件循环。
        - 定时器线程: 负责处理定时器，计算定时器是否到期，到期后将定时器事件放入事件队列中。
        - 异步 HTTP 请求线程: 负责处理 XMLHTTPRequest 请求，当请求完成后将请求的回调函数放入事件队列中。
4. 进程之间的通信
    - 进程之间的通信主要包括管道、消息队列、信号量、共享内存、套接字等。
    - 线程之间的通信主要包括锁、条件变量、信号量、屏障等。
5. 死锁
    - 死锁产生的原因为互斥、请求和保持、非剥夺、循环等待。
    - 避免死锁的方法主要包括破坏死锁产生的条件、预防死锁、检测死锁、解除死锁等。
6. 浏览器标签页之间的通信
    - websocket 协议： WebSocket 是一种网络通信协议，可以在浏览器和服务器之间建立持久连接，实现全双工通信。
    - sharedWorker： SharedWorker 是一种共享的 Web Worker，可以在多个浏览器标签页之间共享数据。
    - localStorage： localStorage 是浏览器提供的本地存储机制，可以在多个浏览器标签页之间共享数据。
    - postMessage： postMessage 是 HTML5 提供的跨文档消息传递机制，可以在多个浏览器标签页之间传递消息。

#### 浏览器缓存

-   浏览器缓存的过程
    1. 浏览器第一次加载资源，服务器返回 200。浏览器从服务器下载资源，并缓存资源与 response header。
    2. 浏览器之后加载资源，先验证强缓存。检验顺序：Expires(验证上一次请求的时间) -> Cache-Control(验证 max-age 是否过期)。
    3. 如果强缓存失效或者没有命中强缓存，浏览器验证协商缓存，向服务器发送带有 If-Modified-Since、If-None-Match、Last-Modified、Etag 等字段的请求。
    4. 服务器收到请求，根据字段判断资源是否更新，返回 304 或者 200。
-   强缓存和协商缓存
    -   强缓存: 浏览器在加载资源时，先检查强缓存，如果命中强缓存，则直接从缓存中获取资源，不会向服务器发送请求。强缓存常见的 header 有 Expires 和 Cache-Control。
        -   Expires: 指定资源的过期时间，是一个绝对时间，如 Expires: Wed, 21 Oct 2020 07:28:00 GMT。
        -   Cache-Control: 指定资源的缓存策略，是一个相对时间，如 Cache-Control: max-age=3600。Cache-Control 包括的字段有 public、private、no-cache、no-store、max-age、must-revalidate 等。
            -   public: 资源可以被任何缓存所缓存。
            -   private: 资源只能被浏览器缓存，不能被代理服务器缓存。
            -   no-cache: 强制浏览器每次都向服务器验证资源是否更新。
            -   no-store: 禁止缓存，浏览器每次都向服务器请求资源。
            -   max-age: 指定资源的最大缓存时间，单位为秒。max-age优先级高于 Expires。
            -   must-revalidate: 强制浏览器在过期后必须向服务器验证资源是否更新。
        -   memory cache 和 disk cache: memory cache 是内存缓存，disk cache 是磁盘缓存。memory cache 的速度更快，但存储空间有限；disk cache 的速度较慢，但存储空间较大。
    -   协商缓存: 如果未命中强缓存，浏览器会向服务器发送请求，服务器根据请求头中的 If-Modified-Since、If-None-Match 等字段判断资源是否更新，如果资源未更新，则返回 304，浏览器从缓存中获取资源。协商缓存常见的 header 有 Last-Modified、Etag、If-Modified-Since、If-None-Match。
        -   Last-Modified: 指定资源的最后修改时间。
        -   Etag: 指定资源的唯一标识符。Etag 的优先级高于 Last-Modified。
        -   If-Modified-Since: 指定资源的最后修改时间，用于协商缓存。一般值为last-modified。
        -   If-None-Match: 指定资源的唯一标识符，用于协商缓存。一般值为Etag。

#### 浏览器存储

-   cookie
    cookie 是一种存储在客户端的数据，用于存储用户的身份认证、会话状态、个性化设置等信息。cookie 有以下特点：
    -   存储位置: 存储在客户端。
    -   存储大小: 4KB。
    -   数据有效期: 可以设置过期时间。
    -   作用域不同: 无法跨域共享。
    -   常见字段： name(cookie 名称)、value(cookie 值)、domain(cookie 作用域)、path(cookie 路径)、expires(cookie 过期时间)、secure(cookie 安全标志)、httpOnly(cookie 是否只能通过 HTTP 协议传输)。
-   sessionStorage
    sessionStorage 是一种存储在客户端的数据，用于存储会话状态、临时数据等信息。sessionStorage 有以下特点：
    -   存储位置: 存储在客户端。
    -   存储大小: 5MB。
    -   数据有效期: 仅在当前会话有效。
    -   作用域不同: 同源窗口。
-   localStorage
    localStorage 是一种存储在客户端的数据，用于存储用户的个性化设置、本地缓存等信息。localStorage 有以下特点：
    -   存储位置: 存储在客户端。
    -   存储大小: 5MB。
    -   数据有效期: 永久有效。
    -   作用域不同: 同源窗口。

### 移动端

#### 移动端适配

H5 端和移动端存在着不同的屏幕尺寸，为了适配不同的屏幕尺寸，需要进行移动端适配。常见的移动端适配方案有多种。

##### viewport

viewport 是移动端浏览器的可视区域，它的大小会影响页面的布局和渲染。在移动端适配中，可以通过设置 viewport 的 meta 标签来控制页面的缩放和布局。

```html
<script>
    // 自适应viewport
    const mobileAdapter = () => {
        const scale = 1 / window.devicePixelRatio;
        const content = `width=device-width, initial-scale=${scale}, maximum-scale=${scale}, minimum-scale=${scale}, user-scalable=no`;
        document
            .querySelector('meta[name="viewport"]')
            .setAttribute("content", content);
    };
    mobileAdapter();
</script>
```

##### 相对定位

1. vw 和 vh 是 CSS3 新增的相对单位，分别表示视口宽度和视口高度的百分比。在移动端适配中，可以使用 vw 和 vh 单位来设置元素的大小，实现页面的自适应。
2. rem 和 em 是 CSS 的相对单位，分别表示相对于根元素和相对于父元素的字体大小。在移动端适配中，可以使用 rem 和 em 单位来设置元素的大小，实现页面的自适应。
3. flex 布局(弹性盒子), grid 布局(网格布局)等布局方式，可以实现页面的自适应。

##### 媒体查询

媒体查询是 CSS3 新增的功能，用于根据不同的媒体类型和特性来应用不同的样式。在移动端适配中，可以使用媒体查询来根据屏幕尺寸和方向来应用不同的样式。

```css
/* 根据屏幕宽度设置字体大小 */
@media screen and (max-width: 320px) {
    body {
        font-size: 12px;
    }
}
@media screen and (min-width: 321px) and (max-width: 375px) {
    body {
        font-size: 14px;
    }
}
@media screen and (min-width: 376px) and (max-width: 414px) {
    body {
        font-size: 16px;
    }
}
```

##### 响应式设计和自适应设计

-   响应式设计: 响应式设计是一种根据不同的屏幕尺寸来调整页面布局和样式的设计方式。响应式设计一般只需要设置一套样式，就可以适配不同的屏幕尺寸。
-   自适应设计: 自适应设计是一种根据不同的设备特性来调整页面布局和样式的设计方式。自适应设计一般需要设置多套样式，根据不同的设备特性来应用不同的样式。

#### 移动端技术栈

1. 原生 APP： 使用原生开发语言，比如 Android- Java/Kotlin，iOS- Objective-C/Swift。
2. 混合 APP： 使用 Web 技术开发，通过 WebView 加载页面，如 PhoneGap、Cordova、Ionic 等。
3. 跨平台 APP： 使用一套代码开发多个平台，如 Flutter、React Native、Weex 等。

-   uni-app 类似框架实现多端开发的底层原理？
    1.  **抽象层/中间层转换：**
        -   **统一 DSL (Domain Specific Language)：** 这些框架通常会定义一套自己的 DSL，这套 DSL 类似于 HTML、CSS 和 JavaScript 的组合，但又在其基础上进行了抽象和扩展，使其能够描述多端通用的 UI 结构和逻辑。
        -   **编译器/转换器：** 框架的核心是一个编译器或转换器，它负责将 DSL 描述的代码转换成各个目标平台能够识别和运行的代码。 例如，将 `uni-app` 的 `.vue` 文件转换成微信小程序、H5 或 App 平台的代码。
    2.  **平台适配层：**
        -   **组件库：** 框架会提供一套跨平台的组件库。 这些组件在不同平台上会渲染成该平台对应的原生组件或模拟组件。 例如，`<button>` 组件在 Web 端可能渲染成 HTML 的 `<button>` 标签，在小程序端则会使用小程序提供的 `<button>` 组件。
        -   **API 适配：** 不同平台提供的 API 接口存在差异。 框架会对这些 API 进行封装和适配，提供统一的 JavaScript API 供开发者调用。 框架内部会将这些统一的 API 调用转换成各个平台特定的 API 调用。
    3.  **运行时环境：**
        -   **Web：** 在 Web 端，框架通常会生成标准的 HTML、CSS 和 JavaScript 代码，这些代码可以直接在浏览器中运行。
        -   **小程序：** 在小程序端，框架会生成符合小程序规范的代码，这些代码需要在小程序运行环境中运行。
        -   **App (Native)：** 在 App 端，通常会使用 WebView 来加载 Web 代码，或者使用 React Native、Weex 等技术将 JavaScript 代码转换成原生组件。

### 性能优化

#### CDN 优化

CDN(Content Delivery Network) 是一种通过在网络边缘部署缓存服务器，提高用户访问速度的技术。CDN 加速的原理是将用户请求的资源缓存在 CDN 节点上，当用户请求资源时，CDN 节点会根据用户的地理位置和网络状况，选择最近的节点返回资源，提高用户访问速度。

1. CDN 系统的组成:
    - **CDN DNS 服务器**: 用于解析用户请求的域名，返回最近的 CDN 节点 IP 地址。
    - **CDN 全局负载均衡器**: 根据用户的地理位置和网络状况，向区域负载均衡器分发请求。
    - **CDN 区域负载均衡器**: 根据全局负载均衡器的指示，向用户返回最近的 CDN 节点 IP 地址。
    - **CDN 缓存服务器**: 缓存用户请求的资源，提高用户访问速度。
2. CDN 加速的优点:
    - **提高用户访问速度**: 将用户请求的资源缓存在 CDN 节点上，提高用户访问速度。
    - **减轻源站压力**: CDN 节点可以缓存用户请求的资源，减轻源站的压力。
    - **提高网站安全性**: CDN 节点可以提供安全防护，防止恶意攻击。
3. CDN 加速的应用场景:
    - **静态资源加速**: 静态资源如图片、视频、CSS、JavaScript 等。
    - **动态内容加速**: 动态内容如 HTML 页面、API 接口等。

#### 懒加载

懒加载是一种延迟加载的技术，用于提高页面的加载速度。懒加载的原理是将页面中的资源延迟加载，当用户需要访问资源时，再加载资源。

1. 图片懒加载:
    - **原理**: 将页面中的图片的 `src` 属性设置为占位图，将真实的图片 URL 存储在 `data-src` 属性中。当图片进入可视区域时，再将 `data-src` 的值赋给 `src` 属性，加载图片。
    - **优点**: 减少页面的加载时间，提高用户体验。
    - **应用场景**: 图片较多的页面，如新闻、博客、电商等。
2. 滚动懒加载:
    - **原理**: 监听页面的滚动事件，当元素进入可视区域时，加载元素。
    - **优点**: 减少页面的加载时间，提高用户体验。
    - **应用场景**: 页面中有大量的图片、视频、广告等。
3. 按需加载:
    - **原理**: 根据用户的操作，动态加载页面的资源。
    - **优点**: 减少页面的加载时间，提高用户体验。
    - **应用场景**: 页面中有大量的资源，但用户不一定会全部加载。

#### 回流和重绘优化

回流(重排)和重绘是影响页面性能的两个重要因素，需要进行优化。

1. 回流和重绘的原因:
    - **回流**: 当页面的布局和几何属性发生变化时，浏览器会重新计算元素的位置和大小，这个过程称为回流。回流会导致页面的布局发生变化，影响整个页面的渲染。
    - **重绘**: 当页面的样式发生变化时，浏览器会重新绘制元素的样式，这个过程称为重绘。重绘不会影响页面的布局，只会重新绘制元素的样式。
2. 回流和重绘的优化:
   将重排优化为重绘:
    - 使用 CSS3 动画代替 JavaScript 动画。
    - 使用 CSS3 过渡代替 JavaScript 动画。
    - 使用 CSS3 transform 代替 top、left 等属性。
    - 使用 requestAnimationFrame 代替 setTimeout 和 setInterval。
    - 使用 documentFragment 代替直接操作 DOM。
    - 使用 display: none 代替 visibility: hidden。

#### 节流和防抖优化

节流和防抖是一种优化页面性能的技术，用于减少函数的执行次数，提高页面的响应速度。

1. 节流和防抖定义
    - **节流**: 节流是一种限制函数的执行频率的技术，当函数被调用时，只有在指定的时间间隔内才能再次调用。
    - **防抖**: 防抖是一种延迟函数执行的技术，当函数被调用时，只有在指定的时间间隔内没有再次调用，才会执行函数。
2. 节流和防抖的应用场景
    - **节流**: 页面滚动、窗口调整、输入框输入等。
    - **防抖**: 搜索框输入、按钮点击、窗口调整等。
3. 节流和防抖的实现

    - 节流

        ```javascript
        const throttle = (fn, delay) => {
            let timer = null;
            return function () {
                if (!timer) {
                    timer = setTimeout(() => {
                        fn.apply(this, arguments);
                        timer = null;
                    }, delay);
                }
            };
        };
        ```

    - 防抖
        ```javascript
        const debounce = (fn, delay) => {
            let timer = null;
            return function () {
                if (timer) {
                    clearTimeout(timer);
                }
                timer = setTimeout(() => {
                    fn.apply(this, arguments);
                }, delay);
            };
        };
        ```

#### 图片优化

图片优化是提高页面性能的重要技术，可以减少页面的加载时间，提高用户体验。

1. 不用图片时，使用 CSS3 代替。
2. 使用合适的图片格式，如 JPEG、PNG、WebP 等。
3. 使用 Base64 编码，减少 HTTP 请求。
4. 使用精灵图、雪碧图，减少 HTTP 请求。
5. 使用 svg 绘制矢量图形，减少 HTTP 请求。

#### 用户体验优化

1. **骨架屏**: 骨架屏是一种在页面加载时显示的占位图，用于提升用户体验。骨架屏可以减少用户的等待时间，提高页面的加载速度。

    - **原理**: 在页面加载时，先显示骨架屏，占位图加载完成后，再替换为真实内容。
    - **优点**: 提升用户体验，减少用户等待时间。
    - **应用场景**: 页面加载时间较长的场景，如电商、新闻、博客等。

2. **优化交互体验**: 优化交互体验可以提升用户体验，减少用户的操作成本。

    - **响应式设计**: 使用响应式设计，适配不同的设备，提高用户体验。
    - **减少操作步骤**: 简化用户的操作步骤，减少用户的操作成本。
    - **提供反馈**: 在用户操作时，提供及时的反馈，提高用户体验。
    - **优化表单**: 优化表单的设计，减少用户的输入成本，提高用户体验。

3. **提高页面可访问性**: 提高页面的可访问性可以提升用户体验，减少用户的操作成本。

    - **使用语义化标签**: 使用语义化标签，提高页面的可访问性。
    - **提供替代文本**: 为图片、视频等资源提供替代文本，提高页面的可访问性。
    - **优化键盘导航**: 优化键盘导航，提高页面的可访问性。
    - **提供语音支持**: 提供语音支持，提高页面的可访问性。

4. **优化页面加载顺序**: 优化页面加载顺序可以提升用户体验，减少用户的等待时间。
    - **优先加载关键资源**: 优先加载关键资源，如 CSS、JavaScript、图片等，提高页面的加载速度。
    - **延迟加载非关键资源**: 延迟加载非关键资源，如广告、统计代码等，减少首屏加载时间。
    - **使用异步加载**: 使用异步加载非关键资源，提高页面的加载速度。

### 网络传输

#### 同源策略

同源策略是浏览器的一种安全策略，用于限制一个源的文档或脚本如何与另一个源的资源进行交互。同源策略包括以下几个方面:

1. **协议相同**: URL 的协议必须相同。
2. **域名相同**: URL 的域名必须相同。
3. **端口相同**: URL 的端口必须相同。

-   三个标签是允许跨域的:
    -   `<img>`: 可以加载不同域名下的图片。
    -   `<link>`: 可以加载不同域名下的 CSS 文件。
    -   `<script>`: 可以加载不同域名下的 JavaScript 文件。

#### 跨域解决方案

1. **JSONP**: JSONP 是一种跨域请求的方式，通过动态创建 `<script>` 标签，将请求的数据作为参数传递到回调函数中。优点是兼容性好，缺点是只支持 GET 请求、不安全。
2. **CORS**: CORS 是一种跨域资源共享的标准，通过在服务器端设置响应头，允许跨域请求。优点是支持所有类型的请求、安全可靠。
3. **WebSocket**: WebSocket 是一种全双工通信协议，通过建立 WebSocket 连接，实现跨域通信。优点是实时性好、支持双向通信，缺点是需要服务器端支持、手写心跳连接等。
4. **Nginx 反向代理**: Nginx 可以作为反向代理服务器，将请求转发到目标服务器，实现跨域请求。优点是配置简单、性能好。

#### HTTP

##### HTTP 与 HTTPS

1. **HTTP**: 超文本传输协议，是一种用于传输超文本的协议。HTTP 是明文传输，不安全。HTTP 端口是 80，是无状态的。
2. **HTTPS**: 超文本传输安全协议，是一种通过加密通道传输超文本的协议。HTTPS 使用 SSL/TLS 加密通道，安全可靠。HTTPS 端口是 443，是有状态的。
    - HTTPS 加密流程:
        1. 客户端向服务器发起 HTTPS 请求。
        2. 服务器返回证书，包含公钥和证书信息。
        3. 客户端验证证书，生成随机数，使用公钥加密随机数，发送给服务器。
        4. 服务器使用私钥解密随机数，生成对称密钥，使用对称密钥加密通信。
        5. 客户端使用对称密钥解密通信，建立安全通道。
    - HTTPS 的优点:
        - 数据传输安全，防止数据被窃取。
        - 身份验证，防止中间人攻击。
        - 排名优化，搜索引擎会优先显示 HTTPS 网站。
    - TLS/SSL 协议:
        - TLS(Transport Layer Security) 是 SSL(Secure Sockets Layer) 的升级版，用于加密通信。
        - TLS/SSL 依赖于三类算法: 对称加密、非对称加密、哈希算法。

##### HTTP 版本迭代

-   HTTP1.0 与 HTTP1.1
    1. HTTP1.1 支持分块传输，可以将响应分块传输，提高传输效率。
    2. HTTP1.1 新增了多个请求头，如 Host、Connection、Accept、Content-Type 等。
    3. HTTP1.1 新增了持久长连接，用 keep-alive 头来告诉服务器不要关闭连接。
    4. HTTP1.1 缓存控制机制引入了更多的缓存头，如 ETag、If-Match、If-None-Match 等。
-   HTTP1.x 与 HTTP2
    1. HTTP1.x 是文本（字符串）传输，HTTP2.x 是二进制传输。
    2. HTTP2 支持多路复用，可以在一个连接上同时传输多个请求和响应。
    3. HTTP2 支持头部压缩，可以减少请求和响应的头部大小。
-   HTTP2 与 HTTP3
    1. HTTP3 使用 QUIC 协议，基于 UDP 协议，支持快速建立连接。
    2. HTTP3 支持 0-RTT，可以在第一次连接时发送数据。

##### HTTP 请求方法

-   **GET**: 请求指定的资源。GET 方法是幂等的，不会对服务器资源产生副作用。
-   **POST**: 向指定资源提交数据。POST 方法不是幂等的，可能会对服务器资源产生副作用。
-   **PUT**: 更新指定资源。PUT 方法是幂等的。
-   **DELETE**: 删除指定资源。DELETE 方法是幂等的。
-   **HEAD**: 请求指定资源的响应头。HEAD 方法是幂等的。
-   **OPTIONS**: 请求指定资源的支持的 HTTP 方法。OPTIONS 方法是幂等的。
-   **PATCH**: 局部更新指定资源。PATCH 方法不是幂等的。
-   **CONNECT**: 建立一个到指定资源的隧道。CONNECT 方法不是幂等的。
-   **TRACE**: 回显服务器收到的请求。TRACE 方法是幂等的。
-   **GET** 和 **POST** 的区别:
    1. 应用场景: GET 是幂等的，用于对服务器资源不会产生影响的场景，比如查询数据；POST 不是幂等的，用于对服务器资源会产生影响的场景，比如用户注册。
    2. 数据传输: GET 请求的数据会附加在 URL 后面，可以被缓存和收藏；POST 请求的数据会附加在请求体中，不会被缓存和收藏。
    3. 安全性: GET 请求的数据会暴露在 URL 中，不安全；POST 请求的数据不会暴露在 URL 中，相对安全。
    4. 数据长度: GET 请求的数据长度有限制，一般为 2KB；POST 请求的数据长度没有限制。
    5. 参数类型: GET 请求的参数类型为 URL 编码；POST 请求的参数类型为表单编码、JSON、XML 等。

##### 常见 HTTP 请求头

1. HTTP Request Headers
    - **Accept**: 指定客户端能够接收的内容类型。
    - **Accept-Encoding**: 指定客户端能够接收的内容编码。
    - **Accept-Language**: 指定客户端能够接收的语言。
    - **Cache-Control**: 指定请求和响应的缓存机制。
    - **Connection**: 指定连接的选项。
    - **Content-Length**: 指定请求体的长度。
    - **Content-Type**: 指定请求体的类型。
    - **Cookie**: 指定请求的 Cookie。
    - **Host**: 指定请求的主机名。
    - **Referer**: 指定请求的来源 URL。
    - **User-Agent**: 指定请求的用户浏览器。
2. HTTP Response Headers
    - **Access-Control-Allow-Origin**: 指定允许访问的域名。
    - **Cache-Control**: 指定响应的缓存机制。
    - **Content-Encoding**: 指定响应的内容编码。
    - **Content-Length**: 指定响应体的长度。
    - **Content-Type**: 指定响应体的类型。
    - **Date**: 指定响应的日期。
    - **Location**: 指定重定向的 URL。
    - **Set-Cookie**: 指定响应的 Cookie。
    - **Server**: 指定响应的服务器。

##### HTTP status code

1. **1xx**: 信息性状态码，表示请求已接收，继续处理。
2. **2xx**: 成功状态码，表示请求已成功接收、理解、接受。
    - **200 OK**: 请求成功。
    - **204 No Content**: 请求成功，但没有内容返回。
    - **206 Partial Content**: 请求成功，但只返回部分内容(分块传输)。
3. **3xx**: 重定向状态码，表示需要进一步操作以完成请求。
    - **301 Moved Permanently**: 永久重定向。
    - **302 Found**: 临时重定向。
    - **303 See Other**: 请求资源存在另一个 URI，应使用 GET 方法获取。
    - **304 Not Modified**: 资源未修改，可以使用协商缓存。
    - **307 Temporary Redirect**: 临时重定向。
4. **4xx**: 客户端错误状态码，表示请求包含语法错误或无法完成请求。
    - **400 Bad Request**: 请求无效。
    - **401 Unauthorized**: 需要认证（第一次）或者认证失败（后续）。
    - **403 Forbidden**: 禁止访问。
    - **404 Not Found**: 未找到资源。
5. **5xx**: 服务器错误状态码，表示服务器无法完成明显有效的请求。
    - **500 Internal Server Error**: 服务器执行请求时发生错误。
    - **502 Bad Gateway**: 服务器作为网关或代理，从上游服务器接收到无效响应。
    - **503 Service Unavailable**: 服务器超负荷或者停机维护，无法处理请求。

#### TCP 与 UDP

##### TCP 三次握手和四次挥手

1. **三次握手**:
    - **第一次握手**: 客户端发送 SYN 包到服务器，请求建立连接，seq=x。
    - **第二次握手**: 服务器接收到 SYN 包，发送 SYN-ACK 包到客户端，确认连接，ack=x+1，seq=y。
    - **第三次握手**: 客户端接收到 SYN-ACK 包，发送 ACK 包到服务器，建立连接，ack=y+1。
    - **三次握手的必要性**: 防止已失效的连接请求报文段突然又传送到了服务端，因而产生错误或者浪费资源。
2. **四次挥手**:
    - **第一次挥手**: 客户端发送 FIN 包到服务器，请求关闭连接，seq=x。
    - **第二次挥手**: 服务器接收到 FIN 包，发送 ACK 包到客户端，确认关闭连接，ack=x+1，seq=y。
    - **第三次挥手**: 服务器发送 FIN 包到客户端，请求关闭连接，ack=x+1，seq=z。
    - **第四次挥手**: 客户端接收到 FIN 包，发送 ACK 包到服务器，确认关闭连接，ack=z+1。
    - **四次挥手的必要性**: 二次挥手后服务端还需要数据传输，不能立即关闭连接。

##### TCP 与 UDP 的区别

1. TCP 是面向连接的，UDP 是面向无连接的。
2. TCP 提供可靠的数据传输，UDP 不保证数据传输的可靠性。
3. TCP 提供流量控制和拥塞控制，UDP 不提供。
4. TCP 是面向字节流的，UDP 是面向报文的。
5. TCP 的头部开销较大，UDP 的头部开销较小。
6. TCP 只能点对点通信，UDP 支持一对一、一对多、多对多通信。

#### 非对称加密过程

以用户向支付宝转账为例:

1. 用户方确认支付宝的数字证书，获取支付宝的公钥。
2. 用户方准备好转账信息(金钱、收款方、用户的公钥等)明文信息。
3. 用户方使用哈希算法对明文信息进行摘要处理，生成摘要信息。
4. 用户方用自己的私钥对摘要信息进行加密，生成数字签名。
5. 用户方随机产生对称秘钥加密明文信息，同时用支付宝的公钥加密对称秘钥，生成密文。
6. 用户方将密文、数字签名发送给支付宝。
7. 支付宝接收到密文和数字签名后，用自己的私钥解密得到对称秘钥，用对称秘钥解密得到明文信息。
8. 支付宝用用户的公钥解密数字签名，得到摘要信息。
9. 支付宝用哈希算法对明文信息进行摘要处理，得到新的摘要信息。
10. 支付宝比较两个摘要信息，如果一致则说明信息未被篡改，否则说明信息被篡改。
11. 支付宝确认信息无误后，完成转账操作。

#### OSI 七层模型

1. **物理层**: 传输介质、信号传输。常见协议: IEEE802.3、IEEE802.11。
2. **数据链路层**: 数据帧传输、差错校验。常见协议: PPP、HDLC、VLAN。
3. **网络层**: IP 地址分配、路由选择。常见协议: IP、ICMP、ARP。
4. **传输层**: 数据传输、差错校验。常见协议: TCP、UDP。
5. **会话层**: 建立连接、维护连接。常见协议: NetBIOS、RPC。
6. **表示层**: 数据格式转换、数据加密。常见协议: JPEG、MPEG、SSL。
7. **应用层**: 应用程序接口、数据传输。常见协议: DNS、HTTP、FTP、SMTP、TELNET。

### 工程化

#### 打包工具

##### Webpack

Webpack 是一个模块打包工具，用于将多个模块打包成一个或多个文件。Webpack 的核心概念是模块化，支持 CommonJS、AMD、ES6 模块等多种模块化规范。

-   Webpack 核心概念:
    -   **入口**: Webpack 的入口文件，指定从哪个文件开始打包。
    -   **输出**: Webpack 打包后的输出文件，指定输出的文件名和路径。
    -   **加载器**: Webpack 的加载器，用于处理不同类型的文件，如 CSS、图片、字体等。
    -   **插件**: Webpack 的插件，用于扩展 Webpack 的功能，如压缩代码、提取 CSS、生成 HTML 等。
    -   **模式**: Webpack 的模式，用于指定打包的模式，如开发模式、生产模式。
-   加载器(Loader)
    -   加载器一般在 `module.rules` 中配置，`test` 用于匹配文件类型，`use` 用于指定加载器。
    -   加载器的执行顺序是从下往上，从右往左。
    -   常见的加载器:
        -   **babel-loader**: 用于将 ES6+ 转换为 ES5。
        -   **css-loader**: 用于处理 CSS 文件。
        -   **style-loader**: 用于将 CSS 插入到 DOM 中。
        -   **file-loader**: 用于处理图片、字体等文件。
        -   **url-loader**: 用于将文件转换为 Base64 编码。
        -   **ts-loader**: 用于将 TypeScript 转换为 JavaScript。
-   插件(Plugin)
    -   Webpack 插件是具有 apply 方法的 JavaScript 对象，插件可以在 Webpack 的生命周期中执行特定的操作。
    -   插件一般在 `plugins` 中配置，插件的执行顺序是从上往下。
    -   常见的插件:
        -   **webpack-bundle-analyzer**: 用于分析打包后的文件大小。
        -   **speed-measure-webpack-plugin**: 用于测量打包的速度。
        -   **optimize-css-assets-webpack-plugin**: 用于压缩 CSS 文件。
        -   **uglifyjs-webpack-plugin**: 用于压缩 JavaScript 文件。
        -   **compression-webpack-plugin**: 启用 gzip 压缩。
-   Loader 和 Plugin 的区别:
    -   生命周期: Loader 在打包之前执行，Plugin 在整个编译周期都起作用。
    -   功能: Loader 实质是转换器，将 A 编译形成 B，操作的是文件; Plugin 是对 Webpack 运行生命周期的不同广播事件进行监听，可以对 Loader 的输出结果进行操作，操作的是 Webpack 的运行过程。
    -   使用方式: Loader 在 `module.rules` 中配置，Plugin 在 `plugins` 中配置。
-   Webpack 常见的功能底层原理
    -   热更新: Webpack 的热更新可以通过`devServer`中的`hot`选项来实现。热更新的原理是通过 WebSocket 连接，监听文件的变化，当文件发生变化时，客户端对比新旧文件的差异后，向 WDS 发送 Ajax 请求，获取更改内容(文件列表, Hash)，客户端借助该信息，继续向 WDS 发起 jsonp 请求， 获取该 chunk 的增量更新。
    -   跨域: Webpack 的跨域可以通过 `devServer` 中的 `proxy` 选项来实现。跨域的原理是通过 `webpack-dev-server` 启动一个本地服务器，将请求转发到目标服务器。
-   Webpack 构建过程
    -   初始化参数：从配置文件和 Shell 语句中读取与合并参数，得出最终的参数
    -   开始编译：用上一步得到的参数初始化 Compiler 对象，加载所有配置的插件，执行对象的 run 方法开始执行编译
    -   确定入口：根据配置中的 entry 找出所有的入口文件
    -   编译模块：从入口文件出发，调用所有配置的 Loader 对模块进行翻译，再找出该模块依赖的模块，再递归本步骤直到所有入口依赖的文件都经过了本步骤的处理
    -   完成模块编译：在经过第 4 步使用 Loader 翻译完所有模块后，得到了每个模块被翻译后的最终内容以及它们之间的依赖关系
    -   输出资源：根据入口和模块之间的依赖关系，组装成一个个包含多个模块的 Chunk，再把每个 Chunk 转换成一个单独的文件加入到输出列表
    -   输出完成：在确定好输出内容后，根据配置确定输出的路径和文件名，把文件内容写入到文件系统

##### Vite

    Vite 是一个新一代的前端构建工具，具有快速、轻量、易用等特点。Vite 的核心概念是模块化，支持 ES6 模块和 CommonJS 模块。

-   Vite 与 Webpack 相比
    -   优点
        -   更快的冷启动: Vite 使用原生 ES6 模块，采用 unbundled 的方式加载模块，避免了 Webpack 的打包过程。
        -   更快的热更新: Vite 使用 HMR 技术，支持模块热替换，避免了 Webpack 的全量刷新。
        -   更简单的配置: Vite 的配置文件更简单，支持 TypeScript 和 JavaScript。
    -   缺点
        -   开发环境首屏加载速度慢: 由于 unbundled 的方式加载模块，vite 首次首屏需要做大量的额外工作。不过首次之后 dev server 会对模块进行缓存，后续的加载速度会快很多。
        -   开发环境懒加载慢: 由于 unbundled 的方式加载模块，需要做 resolve 等

#### Web Worker

    Web Worker 是一种在后台线程中运行 JavaScript 的技术，可以实现多线程编程。Web Worker 可以在主线程和子线程之间进行通信，支持传递数据和消息。Web Worker 的优点是可以提高页面的性能，减少主线程的负担。
-   Web Worker 的使用场景
    -   处理大量计算密集型任务，如图像处理、数据分析等。
    -   处理大量 I/O 密集型任务，如网络请求、文件读取等。
    -   实现多线程编程，提高页面的性能。
-   Web Worker 的使用方法
    1. 创建 Web Worker: 使用 `new Worker()` 创建 Web Worker 实例，传入 Worker 脚本的 URL。
    2. 主线程发送消息: 使用 `postMessage()` 方法向 Web Worker 发送消息，用对象的形式传递数据。
    3. Web Worker 接收消息: 使用 `onmessage` 事件处理程序接收主线程发送的消息，用`e.data`获取数据。
    4. Web Worker 发送消息: 使用 `postMessage()` 方法向主线程发送消息。
    5. 主线程接收消息: 使用 `addEventListener()` 监听 `message` 事件接收 Web Worker 发送的消息。
    6. 终止 Web Worker: 使用 `terminate()` 方法终止 Web Worker 的运行。
-   Web Worker 注意点
    -   Web Worker 不能访问 DOM 和 BOM。
    -   Web Worker 只能使用部分Web API，如 `XMLHttpRequest`、`fetch`、`IndexedDB`、定时器等等。
    -   Web Worker 一般适用于 运算时长 - 通信时长 > 50ms 的场景。

#### SandBox

    SandBox 是一种安全的 JavaScript 执行环境，用于隔离和保护 JavaScript 代码的执行。SandBox 可以防止恶意代码对系统的破坏，保护用户的隐私和数据安全。SandBox 的实现方式有多种，如 iframe、Web Worker、Proxy 等。
-   手写 SandBox
    -   with + New Function + Proxy
        -   使用 `with` 语句创建一个新的作用域，使用 `new Function` 创建一个动态执行的函数，使用`Proxy`对对象进行拦截，禁止访问全局变量和对象。
    ```javascript
    function SandBox(code) {
        const sandbox = {}; // 创建一个新的作用域
        const fn = new Function("shadow", `with(shadow) { ${code} }`); // 创建一个动态执行的函数
        const proxy = new Proxy(sandbox, { // 对对象进行代理
            //  拦截对象的属性访问
            has: (target, key) => {
                if(!target.hasOwnProperty(key)) {
                    throw new Error(`"${key}" is not defined`); // 禁止访问全局变量
                }
                return true;
            },
        });
        fn(proxy); // 执行函数
        return proxy; // 返回代理对象
    }
    ```
    -   iframe
        -   使用 `iframe` 创建一个新的执行环境，将代码注入到 `iframe` 中执行，使用 `postMessage` 和 `onmessage` 进行通信。
    ```javascript
    class SandBox {
        constructor() {
            this.iframe = document.createElement("iframe"); // 创建一个新的 iframe
            this.iframe.style.display = "none"; // 隐藏 iframe
            document.body.appendChild(this.iframe); // 将 iframe 添加到 DOM 中
            this.window = this.iframe.contentWindow; // 获取 iframe 的 window 对象
        }
        execute(code) {
            return new Promise((resolve, reject) => {
                this.window.postMessage(code, "*"); // 向 iframe 发送消息
                this.window.addEventListener("message", (e) => {
                    if (e.origin !== window.location.origin) return; // 验证消息来源
                    resolve(e.data); // 返回执行结果
                });
            });
        }
    }
    ```

#### Babel

    Babel 是一个 JavaScript 编译器，用于将 ES6+ 转换为 ES5。Babel 的核心概念是转换器，支持多种转换插件和预设。Babel 的使用方法是安装 Babel CLI 和 Babel 核心库，使用 `babel` 命令进行转换。
-   Babel 的流程
    
    1. 解析: 将源代码解析为抽象语法树 (AST)，使用 `babylon`。
    2. 转换: 使用转换插件对 AST 进行转换，使用 `@babel/traverse`。
    3. 生成: 将转换后的 AST 生成代码，使用 `@babel/generator`。
-   Babel 在vite中的配置与使用
    -   Vite 内置了 Babel 的支持，可以通过 `vite.config.js` 中的 `babel` 选项进行配置。
    -   Vite 使用 `@vitejs/plugin-legacy` 插件来支持旧版浏览器。在`plugin`配置项中添加`PluginLegacy`插件，同时进行相应的配置。常见配置项如下:
        -   `targets`: 指定支持的浏览器版本。
        -   `additionalLegacyPolyfills`: 指定需要添加的额外的 polyfill。
        -   `polyfills`: 指定需要添加的 polyfill。
   
### 简单的手写

-   Js 基础

    -   手写 instanceof

        ```javascript
        function myInstanceof(x, y) {
            const y_pro = y.prototype;
            let x_pro = x.__proto__;

            // 递归查找x的原型链
            while (x_pro) {
                if (x === y) return true;
                x_pro = x.__proto__;
            }

            return false;
        }
        ```

    -   手写 new

        ```javascript
        function myNew(x, ...args) {
            // 错误处理
            if (typeof x !== "function") {
                console.log("error");
                return;
            }

            // 创建一个新对象
            let obj = {};
            obj.__proto__ = x.prototype;
            // 执行构造函数
            let res = x.apply(obj, args);
            // 判断返回值
            let flag = res instanceof Object;

            return flag && res !== null ? res : obj;
        }
        ```

    -   手写 Object.create

        ```javascript
        function myCreate(proto) {
            // 错误处理
            if (typeof proto !== "object") {
                console.log("error");
                return;
            }

            // 创建一个新对象
            function F() {}
            F.prototype = proto;
            return new F();
        }
        ```

    -   手写 Promise(理解)

        ```javascript
        function myPromise(fn) {
            var self = this; // 保存初始状态
            this.state = "pending"; // 初始状态
            this.value = null; // 保存resolve/reject的值
            this.resolvedCallbacks = []; // 保存then的回调
            this.rejectedCallbacks = []; // 保存catch的回调

            // resolve函数
            this.resolve = function (value) {
                // 只有在pending状态下才能改变状态
                if (self.state !== "pending") return;

                self.state = "fulfilled";
                self.value = value;

                // 保证代码的执行顺序
                queueMicrotask(() => {
                    self.resolvedCallbacks.forEach((cb) => {
                        cb(self.value);
                    });
                });
            }

            // reject函数
            this.reject = function (error) {
                // 只有在pending状态下才能改变状态
                if (self.state !== "pending") return;

                self.state = "rejected";
                self.value = error;

                queueMicrotask(() => {
                    self.rejectedCallbacks.forEach((cb) => {
                        cb(self.value);
                    });
                });
            }

            // 执行fn
            try {
                fn(this.resolve, this.reject);
            } catch (e) {
                reject(e);
            }
        }

        // then方法
        myPromise.prototype.then = function (onFulfilled, onRejected) {
            var self = this;
            onFulfilled =
                typeof onFulfilled === "function"
                    ? onFulfilled
                    : function (value) {
                          return value;
                      };
            onRejected =
                typeof onRejected === "function"
                    ? onRejected
                    : function (error) {
                          throw error;
                      };

            // then方法返回一个新的promise对象
            return new myPromise((resolve, reject) => {
                // 封装一个函数，用于处理回调函数的返回值
                function handle(callback, type) {
                    try {
                        var res = callback(self.value);
                        if (res instanceof myPromise) {
                            res.then(resolve, reject);
                        } else {
                            type === 1 ? resolve(res) : reject(res);
                        }
                    } catch (e) {
                        reject(e);
                    }
                }

                // 根据状态执行不同的回调函数
                switch (self.state) {
                    case "pending":
                        self.resolvedCallbacks.push(() =>
                            handle(onFulfilled, 1)
                        );
                        self.rejectedCallbacks.push(() =>
                            handle(onRejected, 0)
                        );
                        break;
                    case "fulfilled":
                        handle(onFulfilled, 1);
                        break;
                    case "rejected":
                        handle(onRejected, 0);
                        break;
                }
            });
        };
        ```

    -   手写 Promise.all, Promise.race

        ```javascript
        function myPromiseAll(promises) {
            return new Promise((resolve, reject) => {
                // 保存结果
                let result = Array(promises.length);
                // 计数器
                let count = 0;

                promises.forEach((promise, index) => {
                    promise.then(
                        (res) => {
                            result[index] = res;
                            count++;
                            if (count === promises.length) {
                                resolve(result);
                            }
                        },
                        (err) => {
                            reject(err);
                        }
                    );
                });
            });
        }

        function myPromiseRace(promises) {
            return new Promise((resolve, reject) => {
                promises.forEach((promise) => {
                    Promise.resolve(promise).then(resolve).catch(reject);
                });
            });
        }
        ```

    -   手写 call、apply、bind

        ```javascript
        // call
        Function.prototype.myCall = function (context, ...args) {
            context = context || window; // 处理this为null或undefined的情况
            const fn = new Symbol(); // 创建一个唯一的symbol值
            context[fn] = this; // 将函数挂载到context上
            const res = context[fn](...args); // 执行函数
            delete context[fn]; // 删除挂载的函数
            return res; // 返回结果
        };
        // apply
        Function.prototype.myApply = function (context, args = []) {
            context = context || window; // 处理this为null或undefined的情况
            const fn = Symbol(); // 创建一个唯一的symbol值
            context[fn] = this; // 将函数挂载到context上
            const res = context[fn](...args); // 执行函数
            delete context[fn]; // 删除挂载的函数
            return res; // 返回结果
        };

        // bind
        Function.prototype.myBind = function (context, ...args) {
            context = context || window; // 处理this为null或undefined的情况
            const fn = this; // 保存函数
            const bound = function (...rest) {
                // 返回一个新的函数
                // 处理new调用的情况
                return fn.apply(this instanceof bound ? this : context, [
                    ...args,
                    ...rest,
                ]);
            };
            // 继承原型链
            bound.prototype = Object.create(fn.prototype);
            return bound;
        };
        ```

    -   手写深拷贝

        ```javascript
        function deepClone(obj, hash = new WeakMap()) {
            if (obj === null) return null; // null
            if (typeof obj !== "object") return obj; // 基本数据类型

            // 处理循环引用
            if (hash.has(obj)) return hash.get(obj);
            const cloneObj = Array.isArray(obj) ? [] : {}; // 数组或对象
            hash.set(obj, cloneObj); // 缓存

            for (let key in obj) {
                if (obj.hasOwnProperty(key)) {
                    cloneObj[key] = deepClone(obj[key], hash); // 递归拷贝
                }
            }
            return cloneObj;
        }
        ```

    -   手写 AJAX 请求

        ```javascript
        function myAjax(url, method = "GET", data = null) {
            return new Promise((resolve, reject) => {
                const xhr = new XMLHttpRequest(); // 创建xhr对象
                xhr.open(method, url, true); // 初始化请求
                xhr.setRequestHeader("Content-Type", "application/json"); // 设置请求头

                xhr.onreadystatechange = function () {
                    // 监听状态变化
                    if (xhr.readyState === 4) {
                        // 请求完成
                        if (xhr.status === 200) {
                            // 请求成功
                            resolve(JSON.parse(xhr.responseText)); // 解析响应数据
                        } else {
                            reject(xhr.statusText); // 请求失败
                        }
                    }
                };

                xhr.send(data ? JSON.stringify(data) : null); // 发送请求
            });
        }
        ```

    -   函数柯里化

        ```javascript
        function curry(fn, ...args) {
            // 判断参数个数
            if (fn.length === args.length) return fn(...args); // 参数个数相等，直接执行

            return function (...rest) {
                // 返回一个新的函数
                return curry(fn, ...args, ...rest); // 递归调用
            };
        }
        ```

-   数据处理

    -   日期格式化('YYYY-MM-DD HH:mm:ss')

        ```javascript
        function formatDate(date, format) {
            const map = {
                YYYY: date.getFullYear(),
                MM: String(date.getMonth() + 1).padStart(2, "0"),
                DD: String(date.getDate()).padStart(2, "0"),
                HH: String(date.getHours()).padStart(2, "0"),
                mm: String(date.getMinutes()).padStart(2, "0"),
                ss: String(date.getSeconds()).padStart(2, "0"),
            };
            return format.replace(
                /YYYY|MM|DD|HH|mm|ss/g,
                (matched) => map[matched]
            );
        }

        // 使用
        const date = new Date("2023-10-01 12:00:00");
        const format = "YYYY-MM-DD HH:mm:ss";
        const result = formatDate(date, format);
        ```

    -   数组扁平化

        ```javascript
        function flatten(arr) {
            return arr.reduce((acc, val) => {
                return acc.concat(Array.isArray(val) ? flatten(val) : val);
            }, []);
        }
        ```

    -   url 和 object 互转

        ```javascript
        // url转object
        function urlToObject(url) {
            const paramsStr = url.split("?")[1];
            const paramsArr = paramsStr.split("&");
            let paramsObj = {};

            paramsArr.forEach((param) => {
                if (param.includes("=")) {
                    const [key, value] = param.split("=");
                    paramsObj[key] = decodeURIComponent(value);
                } else {
                    paramsObj[param] = true;
                }
            });

            return paramsObj;
        }
        ```

    -   手写 json.parse 和 json.stringify

        ```javascript
        // json.stringify
        function myStringify(obj) {
            if (obj === null) return "null"; // null
            if (typeof obj !== "object") return JSON.stringify(obj); // 基本数据类型

            const arr = Array.isArray(obj) ? [] : {}; // 数组或对象
            for (let key in obj) {
                if (obj.hasOwnProperty(key)) {
                    arr[key] = myStringify(obj[key]); // 递归拷贝
                }
            }
            return JSON.stringify(arr); // 转换为字符串
        }

        // json.parse
        function myParse(str) {
            return eval("(" + str + ")"); // 使用eval解析字符串
        }
        ```

-   设计模式

    -   单例模式

        -   常见前端场景：组件实例化; Vuex 的 store 等。

        ```javascript
        class Singleton {
            constructor() {
                if (Singleton.instance) {
                    return Singleton.instance;
                }
                Singleton.instance = this;
            }
        }
        ```

    -   适配器模式

        -   常见前端场景：统一接口；替换外部依赖；适配数据格式等。

        ```javascript
        class iPhone {
            request() {
                console.log("iPhone request");
            }
        }

        class Adapter {
            constructor(iphone) {
                this.iphone = iphone;
            }

            request() {
                console.log(
                    "Android request has been adapted to iPhone request"
                );
                this.iphone.request();
            }
        }
        ```

    -   装饰器模式

        -   前端常用场景：权限控制；日志监控；流式 API 等等。

        ```javascript
        // 装饰器模式 在函数前添加函数
        Function.prototype.before = function(beforeFn) {
            const _self = this;
            return function() {
                beforeFn.apply(this, arguments); // 执行前置函数
                return _self.apply(this, arguments); // 执行原函数
            }
        }
        ```

    -   观察者模式

        -   常见前端场景：Vue 的双向绑定; `defineProperty` 的实现; 事件监听等。

        ```javascript
        class Subject {
            constructor() {
                this.observers = [];
            }

            addObserver(observer) {
                this.observers.push(observer);
            }

            notify() {
                this.observers.forEach((observer) => observer.update());
            }
        }

        class Observer {
            constructor(name) {
                this.name = name;
            }

            update() {
                console.log(`${this.name} has been notified`);
            }
        }
        ```

    -   策略模式

        -   常见前端场景：表单验证; 购物车计算; 价格计算等。

        ```javascript
        // 策略模式 实现表单验证
        class Validator {
            constructor() {
                this.strategies = {};
            }

            addStrategy(name, fn) {
                this.strategies[name] = fn;
            }

            validate(name, value) {
                return this.strategies[name](value);
            }
        }
        ```

    -   代理模式
    
        -   常见前端场景：懒加载; 访问控制; 远程代理等。

        ```javascript
        // 代理模式 图片懒加载
        class Image {
            constructor() {
                let imgNode = document.createElement("img");
                document.body.appendChild(imgNode);

                this.imgNode = imgNode;
            }

            setSrc(src) {
                this.imgNode.src = src;
            }
        }

        class ProxyImage {
            constructor() {
                let img = new Image();
                img.onload = () => {
                    this.image.setSrc(this.src);
                };
            }

            setSrc(src) {
                this.image.setSrc(this.src);
            }
        }

        ```