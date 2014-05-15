=============
##深入理解CSS盒模型

###一、基本概念

<figure>
	<img src="https://developer.mozilla.org/files/72/boxmodel%20(1).png">
</figure>

####盒模型

内容区（content area）：包含元素的真正内容，由width和height来控制其大小

默认情况下，`width,min-width,max-width,height,min-height,max-height`控制的均为内容的大小

内边距区域（padding area）：扩展了内容区，位于内容和边框之间，有背景，颜色或图片

padding和内容之间的空间由padding-top,padding-right,padding-bottom,padding-left控制


边框区域（border area）：由border的宽高来决定其大小，border-top, border-right, border-bottom, border-left控制每个方向上 的border的样式

外边距区域（margin area）：表示与其他元素之间的距离，其大小由margin-top,margin-right,margin-bottom,margin-left。注意，与border和padding不同的是，margin有负值，可以使得相邻的盒子出现重叠

####普通流（normal flow）

普通流是一组盒子的集合，盒子属于普通流的条件：

1.display：block,list-item,table
2.float:none
3.position:static,relative
4.要么是流的根元素（flow root）的子元素，要么是属于这个普通流的盒子的子元素