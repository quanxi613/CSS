=============
##深入理解CSS盒模型

###一、基本概念

<figure>
	<img src="https://developer.mozilla.org/files/72/boxmodel%20(1).png">
</figure>

大框代表一个元素生成的矩形区域(box)，每个box都包括一个content（元素内容，比如文本，图片等），环绕四周的padding（元素内边距，填充），border（元素边框）和margin（元素的外边框）。

####盒模型

内容区（content area）：包含元素的真正内容，尺寸由元素渲染后的内容的width和height决定

内边距区域（padding area）：扩展了内容区，位于内容和边框之间，有背景，颜色或图片

padding和内容之间的空间由padding-top,padding-right,padding-bottom,padding-left控制

边框区域（border area）：由border的宽高来决定其大小，border-top, border-right, border-bottom, border-left控制每个方向上 的border的样式

外边距区域（margin area）：表示与其他元素之间的距离，其大小由margin-top,margin-right,margin-bottom,margin-left。注意，与border和padding不同的是，margin有负值，而且margin在某些情况下可以使得相邻的盒子出现重叠现象（collapsing margins）

###几个常见的名词解释

####格式化上下文（formatting context）

指的是初始化元素定义的环境

两个要点：元素定义的环境；初始化

* 元素定义的环境

包含两种：

1. 块格式化上下文（block formatting context，即BFC）
2. 行内格式化上下文（inline formatting context）

格式化的含义：表示在这种环境下元素该如何布局

####普通流（normal flow）

相对于浮动和绝对定位的一个概念，浮动和绝对定位都脱离了普通流

普通流包括块框（block boxes）的块格式化（block formatting），行内框（inline boxes）的行内格式化（inline formatting）。

普通流中的box都属于一个格式化上下文中，这个上下文可能是块的，也可能是行内的，但不可能同时是行内又是块的

####块格式化上下文（BFC）

哪些元素会创建BFC？注意是创建，而不是元素本身是BFC

* 浮动元素
* 绝对定位元素
* 行内块元素，即display：inline-block
* 单元格，即table-cell
* 表格标题元素，即table-caption
* overflow不是visible的元素

BFC可以想象为一个大盒子，有很多元素装在里面，这个大盒子把这些元素与外面的元素隔开

BFC中的元素盒会垂直排列，起点是一个包含块的顶部。在BFC中相邻的块级元素的垂直外边距会发生折叠

BFC与普通盒的区别：

* 包含浮动元素
* 阻止外边距折叠
* 防止元素被浮动元素覆盖

具体的BFC另会写文章解释