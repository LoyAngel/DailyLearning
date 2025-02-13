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

### HTML `<head>`

`<head>` 元素包含了所有的头部标签元素。  
`<title>` 元素描述了文档的标题，包括浏览器工具栏、收藏夹默认和搜索引擎结果页上的标题。  
`<base>` 元素为页面上的所有链接规定默认地址或默认目标，即定义所有标签默认的 target 属性。  
`<link>` 元素定义文档与外部资源的关系, 比如引入 css 表等。  
`<meta>` 元素提供有关页面的元信息，比如针对搜索引擎和更新频度的描述。  
`<style>` 元素定义文档的样式信息, 可以直接引入 css 文件。  
`<script>` 元素用于定义客户端脚本, 可以直接引入 js 文件。

### HTML 表单和输入

表单和输入一般用于收集。  
action:规定当提交表单时向何处发送表单数据。当有 submit 按钮时，点击按钮会向 form 的 action 属性指定的地址发送表单数据。  
method: 规定用于发送表单数据的 HTTP 方法。常见的有 get 和 post。  
`<input>`: 用于表单输入。常见 type 有:text(文本域), password(密码域), radio(单选框), checkbox(复选框), submit(提交按钮), button(按钮), file(文件域)  
HTML5 新元素:  
`<datalist>`: 规定输入域的选项列表。  
`<keygen>`: 规定用于表单的密钥对生成器字段。  
`<output>`: 规定不同类型的输出，比如脚本的输出。

### XHTML

XHTML 是更严格更纯净的 HTML 版本。其中的规则有:

-   开头必须是 `<!DOCTYPE html>`，声明文档类型
-   元素必须被正确地嵌套，必须始终关闭，区分大小写，必须有个根元素
-   属性必须小写，值必须用引号包围，属性值必须被赋值

### HTML5 SVG 和 HTML Canvas

SVG 指可伸缩矢量图形 (Scalable Vector Graphics)。  
HTML SVG 用来定义用于网络的基于矢量的图形。  
xmlns: 定义命名空间。命名空间，是一个用来区分不同 XML 元素的独特标识符，一般默认为 "http://www.w3.org/2000/svg"。  
Canvas 是一个矩形区域，您可以控制其每一像素。Canvas 拥有多种绘制路径、矩形、圆、字符以及添加图像的方法。  
HTML Canvas 是使用 JavaScript 在 HTML 页面上绘图的一种方法。  
在 HTML 中，SVG 和 Canvas 都是用来绘图的，它们区别在于:SGG 不依赖分辨率，支持事件处理，适合大型渲染区域的应用，复杂度高会影响性能，不适合游戏;Canvas 依赖分辨率，不支持事件处理，文本能力渲染弱，能够以.png 或.jpg 格式保存图像，适合游戏密集型应用。

### HTML5 应用缓存

HTML5 引入了应用程序缓存，这意味着 web 应用可进行缓存，并可在没有因特网连接时进行访问。  
缓存开启:在文档的 `<html>` 标签中包含 manifest 属性，指向一个 manifest 文件。

#### Manifest 文件:

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

id 选择器:`#id`，用于指定一个唯一的 HTML 元素。  
class 选择器:`.class`，用于指定一组 HTML 元素。其中，"."前面可以加上标签名，表示该标签下的 class。  
嵌套选择器:`p {}`，表示选择 p 标签下的元素; `.myclass p {}`，表示选择 class 为 myclass 的元素下的 p 标签; `p.myclass {}`，表示选择 class 为 myclass 的 p 标签。  
后代选择器:`div p {}`，表示选择 div 标签下的所有 p 标签。  
群组选择器:`h1, h2, h3 {}`，表示选择 h1、h2、h3 标签。  
子元素选择器:`div>p {}`，表示选择 div 下的直接子元素 p。  
相邻兄弟选择器:`div+p {}`，表示选择 div 后面的第一个 p 元素。  
后续兄弟选择器:`div~p {}`，表示选择 div 后面的所有 p 元素。  
属性和值选择器:`[attribute(=value)]`，表示选择具有指定属性值的元素。分隔符~=、\*=(包含指定值)、|=(值为指定值或一个单词内以指定值开头)、^=(值以指定值开头)、$=(值以指定值结尾)。

### CSS 创建

外部样式表:`<link rel="stylesheet" type="text/css" href="mystyle.css">`，在外部文件中定义样式。样式表应该以.css 扩展名保存。  
内部样式表:`<style>`，在`<head>`中定义样式。  
内联样式:`<p style="color: red;">`，在 HTML 元素中使用样式。  
优先权:内联样式 > 内部样式 > 外部样式 > 浏览器默认样式，并且是继承关系。

### CSS 计量单位

常见的计量单位有:  
绝对单位  
px: 像素，绝对单位，不可伸缩。  
pt: 物理长度单位，1pt=1/72in。  
相对单位
rpx: 相对单位，相对于屏幕宽度的 1/750。
em: 相对单位，相对于所在容器的 font-size 大小。  
rem: 相对单位，相对于 html 的 font-size 大小。  
%: 百分比，相对于父元素的大小。  
vw/vh: 视窗宽度/视窗高度，相对于 viewpoint 的大小。  
ch: 字符宽度，相对于 0 的宽度。

有时会用到 calc()函数，用于动态计算长度值。如:`width: calc(100% - 100px);`。

### CSS 伪类和伪元素

伪类指的是添加到选择器的关键词，指定元素的特殊状态。  
伪元素指的是添加到选择器的关键词，指定元素的特殊部分。  
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

### 布局讲解

#### display

-   display 属性用于定义元素的显示方式。
-   inline: 行内元素，不换行，不可以设置宽高。
-   block: 块级元素，换行，可以设置宽高。
-   inline-block: 行内块级元素，不换行，可以设置宽高。
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
-   grid-gap: 设置网格容器的行列间距。
-   grid-auto-flow: 设置网格容器的子元素如何排列。row(默认值，按行排列)、column(按列排列)、row dense(按行排列，紧凑排列)、column dense(按列排列，紧凑排列)。

-   grid-template-areas: 设置网格容器的区域。用''和空格分隔区域，用'.'表示空白区域。
-   grid-area: 设置网格子元素的区域, 起到了标签的作用。

#### position

position 属性用于定义元素的定位方式。

-   static: 默认值，元素按照文档流进行排列，不会被绝对定位或浮动元素覆盖。元素会忽略 top、right、bottom、left 等定位属性。
-   relative: 相对定位，元素相对于自身原来的位置进行定位。当元素设置了 top、right、bottom、left 属性时，元素会相对于原来的位置进行偏移。
-   fixed: 固定定位，元素相对于浏览器窗口进行定位，即使页面滚动，元素也不会移动。
-   absolute: 绝对定位，元素相对于最近的已定位(position 不为 static)祖先元素进行定位。如果没有已定位的祖先元素，则相对于最初的包含块进行定位。
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

overflow: hidden常见处理三种情况:
-   清除浮动: 一般而言，父级元素不设置高度时，高度由随内容增加自适应高度。当父级元素内部的子元素全部都设置浮动float之后，子元素会脱离标准流，不占位，父级元素检测不到子元素的高度，造成父级元素塌陷。此时可以通过设置overflow: hidden来清除浮动，使父级元素检测到子元素的高度。
-   遮罩：给一个元素中设置overflow:hidden，那么该元素的内容若超出了给定的宽度和高度属性，那么超出的部分将会被隐藏，不占位。
-   解决外边距折叠：当两个相邻的块级元素的外边距相遇时，外边距会合并为一个外边距，取两者中的最大值。此时可以通过设置overflow: hidden来清除外边距折叠。


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

##### BFC

BFC(Block Formatting Context) 块级格式化上下文，是一个独立的渲染区域，只有 Block-level Box 参与，它规定了内部的 Block-level Box 如何布局。

-   BFC 的触发的简单条件：
    -   overflow: hidden
    -   display: inline-block
    -   position: absolute
    -   position: fixed
    -   display: table-cell
    -   display: flex
-   BFC 规则
    -   BFC 就是一个块级元素，块级元素会在垂直方向一个接一个的排列
    -   BFC 就是页面中的一个隔离的独立容器，容器里的标签不会影响到外部标签
    -   垂直方向的距离由 margin 决定， 属于同一个 BFC 的两个相邻的标签外边距会发生重叠
    -   计算 BFC 的高度时，浮动元素也参与计算
-  BFC 的应用
    -   使用Float脱离文档流，高度塌陷
    -   Margin边距重叠
    -   两栏布局

## JavaScript 基础

JavaScript 可以由 src="\*.js"进行引用。
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

字面量: 一般固定的值，有数字(Number)、字符串(String)、布尔(Boolean)、数组(Array)、对象(Object)、null、undefined。
变量: 用于存储数据值。一般用 var、let、const 进行声明。请注意变量声明，未声明使用会导致变量自动作为 window 的属性。非严格模式下，因为变量提升，变量可以在声明之前使用，但是不推荐，会导致代码难以理解。
注释: 单行注释`//`，多行注释`/* */`。

#### JS 字符串

在 JS 中，字符串是一串字符，可以用单引号、双引号、反引号进行定义。
字符串长度用.length 获取。
字符串可以是对象，可以用`new String()`创建，此时该对象可以调用字符串方法。

#### JS 运算符

特殊比较运算符: `==`和`===`，前者会进行类型转换，后者不会。(注意，NaN 不等于自身, +0 不等于-0, 两者用`===`会出错，可以用`Object.is()`进行比较)
逻辑运算符: `&&`、`||`、`!`。
扩展运算符: `...`，用于函数参数、数组、对象等, 用于对数组进行解构。
其他运算符: `in`——比较特殊，右边必须是对象（因此不能判断数组存在），判断对象是否具有指定的属性；`&`交叉可以作为交叉类型，比如`PageParams & {subType?: string}`可以表示在 PageParams 的基础上增加 subType 属性；`|`可以作为联合类型，比如`string | number`表示可以是字符串或者数字。
空值运算符：`??=`, `??`, `?.`——见 ES6 特性

#### JS 循环

类似 C，有 for、while、do-while、for-of 等循环, 写法也类似。
注意: js 中 for-in 用来遍历对象的属性，不适用于数组，数组使用 for-of 遍历。(for-in 在数组里遍历表示遍历下标)

#### JS 类型

6 种基本数据类型: string, number, boolean, null, undefined, symbol(ES6)。
3 种对象类型: Object, Date, Array。
2 种不包含任何值的类型: null, undefined。(NaN, Infinity 是 Number 类型)
typeof 可以判断基本数据类型，但无法区分 Object 和 Array 类型，

一般运用 Constructor 或者 instanceof 进行判断, 即`variable.constructor == Array`, `variable instanceof Array`。
任意转字符串: `String()`, `toString()`, `+""`, `${}`。
任意转数字: `Number()`, `parseInt()`, `parseFloat()`, `+`(置于字符串前)。(无法转换则返回 NaN)。
json 转换: `JSON.stringify()`、`JSON.parse()`。

String 常用属性或方法:

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

Array 常用属性和方法:

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

若拷贝数组 arr,浅拷贝:

-   `arr.slice()`: 返回一个新数组，包含从开始到结束的元素。
-   `arr.concat()`: 返回一个新数组，包含原数组的值。
-   `[...arr]`: 返回一个新数组，包含原数组的值。
-   `Array.from(arr)`: 返回一个新数组，包含原数组的值。
    深拷贝:
-   `JSON.parse(JSON.stringify(arr))`: 返回一个新数组，包含原数组的值。

#### JS 正则(RegExp)

JS 中正则表达式由 /pattern/modifiers(可选) 组成。  
正则一般在 search()、replace()、match()、test()、exec()等方法中使用。
常见的 modifiers(修饰符)有: i(执行对大小写不敏感的匹配)、g(执行全局匹配)、m(执行多行匹配)。

### JS 对象

JS 中对象的定义:

```JavaScript
var person = {
    firstName: "John",
    lastName: "Doe",
    age: 50,
    eyeColor: "blue"
};
```

对象属性可以用`.`或`[]`进行访问。  
对象方法的定义:

```JavaScript
var person = {
    fullName: function() {
        return this.firstName + " " + this.lastName;
    }
};
```

对象获得属性的方法: `Object.keys()`、`Object.values()`、`Object.entries()`。
基本类型转对象: `new Object()`

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

闭包是指有权访问另一个函数作用域中变量的函数。
闭包样例:

```JavaScript
// 闭包实现记忆计数器
var add = (function() {
    var counter = 0;
    return function() {
        return counter += 1;
    }
})();
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

回调函数: 将函数作为参数传入另一个函数中，等待调用。
异步 AJAX: 通过 XMLHttpRequest 对象进行异步请求。
Promise: 用于异步编程，可以链式调用。

#### Promise

Promise 的构造:

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

Promise 会返回一个 Promise 对象，可用以下几个方法进行处理:
`then()`: 用于指定 resolve 和 reject 的回调函数。
`catch()`: 用于指定 reject 的回调函数。
`finally()`: 用于指定不管 Promise 对象最后状态如何都会执行的操作。

#### 异步函数

async 函数: 用于定义异步函数，返回一个 Promise 对象。
await 关键字: 用于等待 Promise 对象的返回结果。
async 可以对 Promise 进行简化，使代码更加清晰，例子如下:

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
事件循环涉及三个存储区:

-   函数调用栈: 存储函数调用。
-   宏任务队列: 存储宏任务，如 setTimeout、setInterval、setImmediate、I/O、UI rendering。
-   微任务队列: 存储微任务，如 Promise、process.nextTick、MutationObserver。
    压栈顺序按照上述存储区依次执行，并且为先进后出，所以会先执行微任务队列中的任务，再执行宏任务队列中的任务。

### JS 类

类的构造函数: `constructor`，用于初始化类的实例。
类可以匿名创建。

#### 类继承

类: JS 的类其实是语法糖，本质上还是函数。但类不会提升。
类继承: 使用`extends`关键字。子类构造函数中用`super()`可以调用父类的构造函数。
原型链: JS 在函数创建时，会生成 prototype 属性，该属性指向一个对象，称为原型对象。原型对象中有一个 constructor 属性，指向构造函数。通过构造函数创建的对象，有一个**proto**属性，指向构造函数的原型对象。因此在访问对象时，查找的先后顺序是:对象本身->原型对象->原型对象的原型对象->...->Object.prototype，如此形成的链式结构称为原型链。
getter 和 setter: 用于获取和设置对象的属性。
静态方法: 使用`static`关键字，又称为类方法。

### JS HTML DOM

DOM: Document Object Model，文档对象模型，是 HTML 和 XML 的应用程序接口。
DOM 是文档的逻辑结构，可以通过 JS 进行访问和修改。

#### DOM 查找

`document.getElementById(id)`: 通过 id 获取元素。
`document.getElementsByTagName(tag)`: 通过标签名获取元素。
`document.getElementsByClassName(class)`: 通过类名获取元素。
`document.querySelector(selector)`: 通过选择器获取元素。

#### DOM 修改

`element.innerHTML`: 获取或设置元素的内容。
`element.attribute`: 获取或设置元素的属性。

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
-   省略: 当只有一个参数时，可以省略括号; 当只有一个表达式时，可以省略大括号和 return。
-   示例: `let fun = (a, b) => a + b`;

```JavaScript
// 普通函数
var x = function(x, y) {
    return x * y;
}
// 箭头函数
var x = (x, y) => x * y;
```

#### 模板字符串

-   模板字符串: 用于创建多行字符串，可以嵌入变量。
-   模板字符串使用反引号`进行定义，变量使用'${}'进行替换，同时还支持多行文本。

```JavaScript
let name = "John";
let age = 30;
let text = `My name is ${name}, I am ${age} years old.`;
```

## TypeScript 基础

-   TypeScript 是 JavaScript 的超集，可以编译为纯 JavaScript。
-   TypeScript 支持类型注解、接口、类、模块等。

以下重点叙述 TypeScript 区别于 JavaScript 的部分。

### TypeScript 变量声明

-   TypeScript 支持变量声明时指定类型，如`let name: string = "John";`。
-   联合类型: 变量可以有多种类型，如`let name: string | number = "John";`。
-   类型断言: 用于告诉编译器变量的类型，有两种形式，`<type>value`和`value as type`。
-   非空断言: 用于告诉编译器变量不为空，如`let stu{ name!: string; } = {}; console.log(stu!.name);`。
-   类型推断: TypeScript 可以根据变量的值推断变量的类型, 如果未申明类型，则默认类型为 any。

### TypeScript 函数

-   TypeScript 可以指定返回值类型，如`function fun(): number {return 1;}`。
-   TypeScript 可以指定参数类型，如`function fun(name: string): void {console.log(name);}`; 可以指定可选参数，如`function fun(name?: string): void {console.log(name);}`；可以指定默认参数，如`function fun(name: string = "John"): void {console.log(name);}`；可以指定剩余参数，如`function fun(...name: string[]): void {console.log(name);}`。
-   TypeScript 支持函数重载，即可以定义多个同名函数，但参数类型或个数不同。

### TypeScript 元组和数组

元组和数组区别:

-   元组: 元组中的元素类型不必相同。
-   数组: 数组中的元素类型必须相同。
-   元组和数组的定义: 元组使用`[type1, type2, ...]`，数组使用`type[]`。

### TypeScript 接口 和 类型

-   接口: 用于定义对象的类型，可以包含属性、方法、索引签名等。
-   接口定义: 使用`interface`关键字，如`interface Person {name: string; age: number;}`。
-   接口可以设置数组的索引值和元素类型，如`interface StringArray { [index: number]: string; }`。
-   接口也支持继承，并且支持多继承，如`interface Person extends Name, Age {}`。

-   类型：用于定义类型别名，可以包含基本类型、联合类型、元组、对象等。
-   类型定义: 使用`type`关键字，如`type Name = string;`。
-   类型别名可以定义联合类型，如`type Name = string | null;`。
-   类型别名可以定义元组，如`type Name = [string, number];`。

-   类型和接口的区别:
    -   实现继承方面有区别:

```TypeScript
// type 继承 type
type Person {
    name: string
}

type Student = Person & { stuId: number }

// type 继承 interface
interface Person {
    name: string
}

type Student = Person & { stuId: number }
```

    - type能做到：声明基本类型、联合类型、元组等类型
    - interface能做到：声明合并(type会报重复定义的错误)

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
-   泛型函数: 使用泛型来创建一个可以支持多种类型的函数，如`function identity<T>(arg: T): T {return arg;}`。
-   泛型约束: 用于限制泛型类型。

```TypeScript
// 泛型约束
interface Lengthwise {
    length: number;
}
function loggingIdentity<T extends Lengthwise>(arg: T): T {
    console.log(arg.length);
    return arg;
}
// 正确使用
loggingIdentity("Hello");
// 错误使用, 因为数字没有length属性
loggingIdentity(3);
```

```TypeScript
// 样例讲解
// 定义一个接口，包含length属性
interface ApiResponseData<T> {
  code: number
  data: T
  message: string
}
// 下面这个接口继承了上面的接口，并指定了data的类型为string
type LoginResponseData = ApiResponseData<{
  token: string
}>
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
