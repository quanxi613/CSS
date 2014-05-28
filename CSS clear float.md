==========

##清除浮动

目前清除浮动的主流方案是

	.clearfix:after{
	    content:"."; 
	    display:block; 
	    height:0; 
	    visibility:hidden; 
	    clear:both;
	}
	.clearfix{
		*zoom:1;
	}

解释：

对父容器添加clearfix后，由于使用伪元素after，向父容器中追加了一个不可见的块元素，又有clear：both，表示追加的这个块元素的左侧和右侧均不允许出现浮动元素，也即这个块元素会按照左右均不浮动来定位自己，会定位到浮动元素的下一行，当父容器发现有一个非浮动普通流的子元素，便会将其包围，如此便解决了浮动元素造成的父元素高度塌陷问题

设置display：block是因为display默认值为inline，不能使用clear的特性，设置height：0将追加的块元素的高度设为0，并设置visibility隐藏，是创建一个隐形的内容为空的块元素

*zoom：1是兼容IE6/7