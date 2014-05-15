=============

##Collapsing margins

某些相邻的margins会合并为一个单个的margin，这被称之为折叠（collapse）


官方介绍：两个或多个毗邻（父子元素或兄弟元素）的普通流中的块元素在垂直方向上的margin会发生折叠。这种方式产生的外边距称为外边距叠加（Collapsing margins）

需要强调的几点：

1.两个或多个

数量必须大于一个，叠加是元素间的相互行为

2.毗邻的含义

如果某些margins没有被非空内容，padding，border areas或空白分隔彼此，那么我们说这些margins是相邻的，同时这些margin都处于普通流（非浮动元素，非定位元素）中 

注意一点，在没有被分隔开的情况下，一个元素(非浮动元素等)的 margin-top 会和它普通流中的第一个子元素的 margin-top 相邻； 只有在一个元素的 height 是 “auto” 的情况下，它的 margin-bottom 才会和它普通流中的最后一个子元素(非浮动元素等)的 margin-bottom 相邻。

3.垂直方向

只有垂直方向的margin才会叠加，水平方向的margin不会发生叠加


####发生margin叠加

两种情况下发生：1.父子元素  2.兄弟元素
举个栗子

	<div style="border:1px solid red; width:100px;">
	    <div style="margin:50px 0; background-color:green; height:50px; width:50px;">
		    <div style="margin:20px 0;">
		        <div style="margin:100px 0;">green</div>
		    </div>
	    </div>
	</div>

效果图

<figure>
	<img src="http://d.pcs.baidu.com/thumbnail/2277bd38e48b38fe3896ca25884a11c9?fid=1409859911-250528-545897435163712&time=1400036400&rt=pr&sign=FDTAER-DCb740ccc5511e5e8fedcff06b081203-HZUALkl3n9TwmEAytmstHWKxoZE%3D&expires=8h&prisign=RK9dhfZlTqV5TuwkO5ihMQzlM241kT2YfffnCZFTaEMATYGtWbeBgRXLxDSXMBba1Ms9seOiqT9/QffwI8K2Baw0mmLABRQNl51b/oS8+InqoadADmwcyvUvQUkAvl8j879BObtgHePZ09BZiFo3CF7dwGcK/xIzj9971pKao/QALkDxW+JJC9zJS3FHk0o7K3AvxUdo+G6eyRN1SNLGNa0D1UAV5NRAenChpEOFUtk=&chkv=0&chkbd=0&r=826842028&size=c850_u580&quality=100">
</figure>

对上述栗子的解释：

为了描述方便，从外到内对div编号：div1，div2，div3，div4.由于

一些rules：

* 只有块级的盒子的margin才会有重叠的可能
* 浮动的盒子的margin不会与其他任何margin产生重叠
* overflow不是visible的盒子与自己子元素的margin不会重叠
* 绝对定位的盒子不会与其他元素的margin产生重叠
* inline-block的盒子不会与其他盒子产生margin重叠
* 根元素的margin不会重叠
* 如果一个盒子已经出现重叠现象，这时对重叠的margin的某个方向（top,right,left）加间隔（clearance），那么相应方向的margin将不再和其父元素的bottom,left,right margin重叠
* 如果margin P与margin Q重叠，margin Q与margin R重叠，那么P,Q,R互相重叠，重叠是会传递的



