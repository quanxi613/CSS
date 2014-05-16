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

* 元素定义的环境，包含两种：



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

CSS3中对块格式化上下文做了改动，将BFC叫做flow root

触发方式也修改的更为准确：

`The value of 'position' is neither "static" nor "relative"`

即position为fixed的时候也会创建flow root

具体的BFC另会写文章解释

####行内格式化上下文（inline formatting context）

#####行框（line boxes）

在行内格式化上下文中，boxes水平排列，起点是包含块（containing box）的顶部。

水平方向上，margin，border和padding在boxes直接仍然存在

垂直方向上，有很多种对齐方式，顶部对齐，底部对齐，根据其中的文字的基线对齐

包含这些boxes的长方形区域会形成一行，称为行框

栗子

	<p style="background-color:silver; font-size:30px;">TEXT1<span style="border:3px solid blue;">text in span</span>great1<em style="border:3px solid red;">thx a lot</em>bee<strong style="border:3px solid green;">give me 5!</strong>Aloha!</p>

例子中没有换行符和空格，形成了7个行内框，见下图

<figure>
	<img src="http://www.w3help.org/zh-cn/kb/010/010/line_box.png">
</figure>

行框的宽度由其包含块和其中的浮动元素决定

#####行框的范围

通常情况下，行框的左边紧靠其包含块的左边，右边紧靠其包含块的右边，注意，浮动元素可能会位于包含块边缘和行框边缘之间

在相同的行内格式化上下文中的行框通常有相同的宽度，即包含块的宽度，但若有浮动元素，可能会造成可用宽度变短

栗子

	<p style="background-color:silver; width:500px; overflow:hidden; ">
	    <span style="border:1px solid blue; font-size:50px; float:left;">FLOAT</span>
	    <em style="border:1px solid yellow; font-size:30px;">great1</em>
	    <span style="border:1px solid yellow;">good</span>
	</p>

效果图

<figure>
	<img src="http://www.w3help.org/zh-cn/kb/010/010/scope_line_box.png">
</figure>

注意到红线的line box由于浮动元素的存在，宽度不再是包含块的宽度500px了

#####分割的行内框

若一个行框内的多个行内框在水平方向上无法放下，则这些行内框会被分配到多个垂直堆叠的行框中。

比如一个段落p，就是行框在垂直方向上的堆叠

若一个行内框超出包含它的行框的宽度，这个行内框会被分割为几个框，并分别分布到几个行框中。

但若一个行框无法被分割，比如行内框只包含单个字符，或语言特殊的断字规则不允许在行内框里换行，或者行内框受到带有 "nowrap" 或 "pre" 值的 'white-space' 特性的影响，那么此时行内框会溢出行框

被分割的行内框在所有分割处，其margin，padding，border没有视觉效果

行内框还可能由于双向文本处理（bidirectional text processing）而在同一个行框内被分割为好几个框

例子

	<p style="background-color:silver; width:100px; ">
	    <span style="border:1px solid blue; font-size:50px;">text in span</span>
	    <em style="border:1px solid yellow; font-size:30px; vertical-align:top;">great1</em>
	</p>

示意图

<figure>
	<img src="http://www.w3help.org/zh-cn/kb/010/010/inline_box_break.png">
</figure>

第一个span元素的行内框被分割为了3段

#####行内框的对齐

1.垂直方向的对齐

行框的高度总是足够容纳所包含的所有框。不过，它可能高于它包含的最高的框（例如，框对齐会引起基线对齐）。 当一个框 B 的高度小于包含它的行框的高度时，B 在行框中垂直方向上的对齐决定于 'vertical-align'2 特性。 'vertical-align'2 默认值为基线( 'baseline' )对齐。

	<p style="background-color:silver; width:500px; ">
	    <span style="border:1px solid blue; font-size:50px;">text in span</span>
	    <em style="border:1px solid yellow; font-size:30px; vertical-align:top;">great1</em>
	</p>

<figure>
	<img src="http://www.w3help.org/zh-cn/kb/010/010/line_box_align.png">
</figure>

2.水平方向的对齐

当一行中行内框宽度的总和小于包含它们的行框的宽，它们在水平方向上的对齐，取决于 'text-align' 特性。 如果其值是 'justify'，用户端也可以拉伸行内框(除了 'inline-table' 和 'inline-block' 框)中的空间和文字 。

	<p style="background-color:silver; width:500px;overflow:hidden; text-align:center;">
	    <span style="border:1px solid blue; font-size:50px; float:left;">FLOAT</span>
	    <em style="border:1px solid yellow; font-size:30px;">great1</em>
	    <span style="border:1px solid yellow;">good</span>
	</p>

<figure>
	<img src="http://www.w3help.org/zh-cn/kb/010/010/inline_box_horizontal_align.png">
</figure>

由于行内存在浮动元素，导致行框变短，且行内框在对齐的时候是根据行框的宽度进行对齐