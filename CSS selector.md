==========

##CSS选择器的使用方法，场景及浏览器兼容性

1、元素选择器（类型选择器）

最基本的选择器，HTML元素就是选择器

`a {text-decoration:none;}`

`p {color:gray;}`

选择器分组

选择器放在规则左边，用逗号分隔，后面写样式

`body, h2, p, table, th, td, pre, strong, em {color:gray;}`

2、类选择器

类名前加点号（.）

`.active {color:red;}`

类选择器结合元素选择器，比如只希望包含active的class的p元素上显示红色文本

`p.active {color:red;}`

就算其他标签比如h1中也添加class=active，也不会变成红色文本

多类选择器：HTML中，class可以包含很多词列表，词之间用空格分隔

`<p class="important warning">`

	.important {font-weight:bold;}
	.warning {font-style:italic;}
	.important.warning {background:silver;}

然而上面的`.important.warning {background:silver;}`只能选择同时包含这两个类名的元素

兼容性：IE7之前，IE无法正确处理多类选择器

3、ID选择器

ID名前加#号，只能在HTML文档中使用一次，没有ID词列表，即ID选择器不能结合使用

注意：ID选择器区分大小写

4、属性选择器

E[attr]:选择具有attr属性的元素E 

`a[href]{color:red;}`

也可对多个属性进行选择

`a[href][title] {color:red;}`

这么做可以凸显某些样式

E[attr=val]:选择具有attr=val的元素E

`input[type=password] {border:1px solid #aaa;}`

E[attr|=val]:选择具有属性attr，且属性值为val或以val开始的元素E

`*[lang|="en"] {color: red;}`

则会选中

	<p lang="en">Hello!</p>
	<p lang="en-us">Greetings!</p>
	<p lang="en-au">G'day!</p>

而不会选中

	<p lang="cy-en">Jrooana!</p>

E[attr~=val]:选择具有属性attr，且值为完整的单词val的元素E，也即对属性值中词列表中的某个词进行选择

比如要选择class属性中包含important的元素

`p[class~="important"] {color: red;}`

E[attr^=val]：选择具有属性attr且属性值以val开头的元素E：

`a[title=^"abc"]`定位title为abc-开头的所有a

E[attr$=val]：与E[attr^=val]正好相反，选择具有属性attr且属性值以val结尾的元素E：

`a[title=$"abc"]`定位title为abc结尾的所有a

E[attr*=val]：与E[attr~=val]相似，但更进一步，选择具有属性attr且属性值任意位置包含val的元素E，val可以是一个完整的单词，也可以是一个单词中的一部分：

`a[title*="image"]`定位title中包含image子串的元素a

总的来说，属性选择器可以省去再编写class的麻烦

5、关系选择器

后代选择器

E F：选择元素E后代中的所有元素F

`h1 em {color:red;}`

子元素选择器

E > F：选择元素E的直接子元素中的所有元素F，忽略任何的进一步嵌套（与后代选择器的区别，后代选择器不会忽略进一步嵌套）

`ul > li {list-style:none;}`如果li中有进一步嵌套，则不受影响

相邻兄弟选择器：

E + F：选择与元素E有相同父元素且在紧接E的元素F

如增加紧接h1后的p的上边距，二者具有相同的父元素

`h1 + p {margin-top:50px;}`

注意：一个结合符+只能选择两个相邻兄弟中的第二个元素

`li + li {font-weight:bold;}`

	<ul>
	    <li>List item 1</li>
	    <li>List item 2</li>
	    <li>List item 3</li>
		<li>List item 4</li>
	 </ul>

只能使列表中的第二，三，四个列表项变为粗体

一般兄弟选择器

E ~ F：选择与元素E有相同父元素，且位于E之后的所有元素F

`h1 ~ p {color:#f00;}` 选择具有相同父元素的，h1标签之后的所有p标签

6.伪类

选择器与伪类中间以：隔开

`：focus`向拥有键盘输入焦点的元素添加样式

锚伪类：

	a:link {color: #FF0000}		/* 未访问的链接 */
	a:visited {color: #00FF00}	/* 已访问的链接 */
	a:hover {color: #FF00FF}	/* 鼠标移动到链接上 */
	a:active {color: #0000FF}	/* 选定的链接 */

遵循“LOVE HATE”原则

first-child伪类：选择元素的第一个子元素。必须声明DTD，才能在IE中生效

lang伪类：为不同的语言定义特殊的规则

E F:nth-child(n):选择元素E的第n个子元素F

E F:nth-last-child(n)：选择元素E的倒数第n个子元素的元素F

E:nth-of-type(n)：选择元素E的第n个指定类型子元素

E:nth-lash-of-type(n)：选择元素E的倒数第n个指定类型子元素



7、伪元素

用于向某些选择器设置特殊效果，选择器与伪元素中间以：隔开

first-line伪元素：用于向文本的首行设置特殊样式。只能用于块级元素

first-letter伪元素：用于向文本的首字母设置特殊样式。只能用于块级元素

after伪元素可以在元素的内容之后插入新内容

	h1:after
	  {
	  	content:url(logo.gif);
	  }

before伪元素可以在元素的内容前面插入新内容

	h1:before
	  {
	  	content:url(logo.gif);
	  }

