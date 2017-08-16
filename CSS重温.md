# CSS重温
## css选择器
	一、css选择器
	1、元素选择器（类型选择器）：文档的元素就是最基本的选择器
		eg:html {color:black}
		   h1 {color:blue;}
		   h2 {color:silver;}
	2、选择器分组
		eg:想将多个元素显示为灰色，就可以用如下规则：
		   body,h2,p,table,th,td,pre,strong,em {color:silver;}
    3、通配符选择器
		*，该选择器可以与任何元素匹配，就像是一个通配符。
	4、类选择器
		在html中：<h1 class="important">
		          </h1>
		css: .important {color:red;}
			①并且：类选择器可以结合元素选择器来使用
				eg：p.important{color:red;} 选择器会匹配class属性中包含important的所有P元素，解释为：“其class属性值为important的所有段落”
			②多类选择器
				eg:假设class为important的所有元素都是粗体，而class为warning的所有元素为斜体。class同时包含important和warning的所有元素还有一个银色的背景，就可写作：
		    在html中：<p class="important"></p> <!--粗体-->
			      <p class="warning"></p> <!--斜体-->
			      <p class="important warning"></p> <!--粗体，斜体，银色背景。-->
		    在CSS中：.important {font-weight:bold;}
                 .warning {font-style:italic;}
		             .important.warning {background:silver;}
		    所以，通过把两个类选择器连接在一起，仅可以选择**同时包含这些类名的元素**（类名顺序不变）。
	         特殊:若 <p class="important urgent warning"></p>  <!--粗体，斜体，银色背景。-->
		
	5、ID选择器
		在html中：<p id="intro"></p>
		在CSS中： #intro{color:red;}
	     ①id选择器与类选择器的区别：
		* 与类不同，在一个HTML中，ID选择器只能使用一次，而且仅一次。（id相当于你的身份证号一样，若使用多次有违语法规范。）
		* ID选择器不能结合使用，因为ID属性不允许有以空格分割的词列表	
		* id选择器可包含更多含义。
	     *注：类选择器和ID选择器是区分大小写的。
	6、CSS属性选择器
	        ①你希望把包含标题的元素变为红色，可以写作：
				在html中：	<p title="hello">hello world</p>
							<h1 title="w3c school">w3c school</h2>
                             <h2>web前端</h2>
				在CSS中：*[title] {color:red;}  //网页中的p和h1均会变成红色
            ②还可以根据多个属性进行选择，只要将属性选择器连接在一起即可。
                eg: 在html中：<a href=" " title=" "></a>
                    在CSS中：a[href][title] {color:red;}
            ③根据具体的属性值选择
                eg: 你希望指向web服务器上某个指定文档的超链接变为红色，
                         a[href="http//www.baidu.com"] {color:red;}
                    与简单性选择器类似，可以把多个属性-值选择器连接在一起选择一个文档。
			注：属性与属性值必须完全匹配。
				eg:<p class="important warning"></p>
					p[class="important"] {color:red;}//错误。
					p[class="important warning"] {color:red;}//正确。
            ④根据部分属性值选择
				如果需要根据属性值中的词列表中某个词进行选择：
				eg:想选择class属性中包含important的元素则：
					p[class~="important"] {color:red;}
			⑤子串匹配属性选择器
				[abc^="def"] 选择abc属性值以"def"开头的所有元素
				[abc$="def"] 选择abc属性值以"def"结尾的所有元素
                [abc*="def"] 选择abc属性值中包含子串"def"的所有元素
	        ⑥总结：
		   选择器                       描述
                                           
		[attribute]		用于选取带有指定属性的元素。

		[attribute=value]	用于选取带有指定属性和值的元素。

		[attribute~=value]	用于选取属性值中包含指定词汇的元素。

 		[attribute|=value]	用于选取带有以指定值开头的属性值的元素，该值必须是整个单词。

		[attribute^=value]      匹配属性值以指定值开头的每个元素。

		[attribute$=value]	匹配属性值以指定值结尾的每个元素。

		[attribute*=value]      匹配属性值中包含指定值的每个元素。
	7、后代选择器
		如果你希望你只对h1元素中的em元素应用样式：
			h1 em {color:red;}
		有关后代选择器：两个元素的层次间隔可以是无限的：例如：入股偶写作yl em,这个语法就会选择从ul元素继承的所有em元素，而不论em的嵌套层有多深。
	8、CSS子元素选择器
		如果你不希望选择任意后代元素，希望缩小范围。例如：你只希望选择h1元素子元素的strong元素：
		       h1>strong{color:red;}
		       在html中如果：
	          <h1>This is <strong>very<strong> <strong>very<strong> improtant </h1>  //very变红色
			  <h1>This is <em>really  <strong>very<strong> </em> important </h1>     //very不变色 这里strong是em的子元素。
			  <h1>This is <em>really</em> <strong>very</strong> important </h1>      //very变红色
	9、相邻兄弟选择器：可选择紧接在另一元素后的元素，且二者有相同的父元素
	    ①例如：如果要增加紧接在h1元素后出现的段落的上边距：h1+p {margin-top:50px;}
	    ②+是相邻兄弟结合符。一个结合符只能选择两个相邻兄弟中国的第二个元素。
			eg: 在html中：
			<ul>
				<li>list item1</li>
				<li>list item2</li>
				<li>list item3</li>
	    	</ul>
				在CSS中：
				li+li {font-weight:bold;}
			只会把第二个和第三个列表项变为粗体，第一个不受影响。
	    ③结合其他选择器
			html>body table + ul {margin-top:20px;}
			这个选择器解释为：选择紧接着table元素后出现的所有兄弟ul元素，该table元素包含在一个body元素中，body元素本身是html元素的子元素。
	10、CSS伪类
		①锚伪类。连接的不同状态都可以不同的方式显示。
			a:link {...} 未访问的链接
			a:visited {...} 已访问的链接
			a:hover {...} 鼠标移动到链接上
			a:active {...} 选定的链接
		②伪类可以与CSS类配合使用
			a.red:visited{...}
			<a class="red"  href=""></a>    //如果这个被访问过，它将显示红色。
	    ③:first-child伪类：选择元素的第一个子元素。
			eg:   p:first-child {font-weight:bold;}
				  li:first-child {text-transform:uppercase;}
			将作为某元素的第一个子元素的P元素设置为粗体
			将作为某元素的第一个子元素的LI元素变为大写。
			***并不是选择P元素的第一个子元素。
			eq（1）:匹配所有<p>元素中的第一个<i>元素：
				p > i:first-child {
					font-weight:bold;
				}
		html中：<p>
					some **<i>text</i>** some <i>text</i>  
				</p>
				<p>
					some **<i>text</i>** some <i>text</i>
				</p>
			eq（2）:匹配作为第一个子元素<p>元素中的所有<i>元素
				p:first-child > i{
					color:blue
				}
		html中：<p>
					some **<i>text</i>** some **<i>text</i>**  
				</p>
				<p>
					some <i>text</i> some <i>text</i>
				</p>
		④：lang伪类
		⑤：总结
		   :active                 向被激活的元素添加样式
		   :focus                  向拥有键盘输入焦点的元素添加样式
		   :hover                  当鼠标悬浮在元素上方时，向元素添加样式
		   :link                   向未被访问的链接添加样式
		   :visited                向已被访问的链接添加样式
		   :first-child            向元素的第一个子元素添加样式

	11、CSS伪元素
	    ① :first-line 伪元素用于向文本首行设置样式。注意：first-line伪元素只能用于块级元素。
		②  :first-letter伪元素用于向文本的首字母设置特殊样式。它也只能用于块级元素。
		③可重伪元素：多个伪元素可混合使用。
				p:first-letter {      
				}
				p：first-line{
				}
	    ④   :before伪元素可以在元素内容前面插入新内容。
		⑤   :after伪元素可以在元素的内容之后插入新内容。

## CSS样式
	1.背景background
		background-color                   设置背景颜色
		background-image :url(....png)     设置背景图像 
		background-repeat                  背景图像平铺
		background-position                改变图像在背景中的位置
		background-attachment              背景关联
			background-attachment ：scroll（默认值）背景图像会随页面其余部分的滚动而滚动。
			                                fixed 当页面其余部分滚动时，背景图像不会移动。
											        inherit  从父元素继承background-attachment属性设置。
	2. CSS文本								
		①缩进文本：text-indent
		②水平对齐：text-align:left,right,center,justify(两端对齐)，inherit
		③字间隔：word-spacing:改变字（单词）之间的间隔
		④字符转换：text-tranform
						*none
						*uppercase全大写
						*lowercase全小写
						*capitalize只对每个单词首字母大写
		⑤文本装饰：text-decoration
						*none
						*underline 下划线
						*overline  上划线
						*line-through 贯穿线
						*blink 文本闪烁
		⑥处理空白符：white-space：会影响到对源文档中的空格、换行和tab字符的处理
						*normal:告诉浏览器丢掉多余的空白符。
						*pre：空白符不会被忽略
						*nowrap:防止文本换行，除非使用<br>元素
						*pre-wrap:保留空白符序列，但文本会正常的换行
						*pre-line:合并空白符序列，保留换行符
	3. CSS字体
		①字体样式：font-family
		②字体风格：font-style:
						normal文本正常显示
						italic文本斜题显示
						oblique文本倾斜显示
		③字体变形：font-variant可以设置小型大写字母。
						p{font-variant:small-caps;}
	  ④字体加粗:font-weight:100~900为字体指定了9级加粗级。400相对于normal,700相对于bold;
	4. CSS列表
		①列表类型：list-style-type:disc,circle,square,decimal(数字)，decimal-leading-zero（以0开头的数字标记）
		②列表项图像：{list-style-image:url(xxx.gif)}
		③列表标记位置：list-style-position:
							outside:(默认值)列表项目标记放置在文本以内，且环绕文本根据表及对齐
							inside：列表项目标记放置在文本以内，且环绕文本根据标记对齐。
	5. 表格
		①折叠边框：border-collapse属性设置是否将表格边框折叠为单一边框
							separate:默认值，边框会被分开
							collaps：合成单一边框，会忽略border-spacing和empty-cell属性
	6. CSS轮廓（outline）
		绘制于元素周围的一条线，位于边框边缘。
		outline:#FFFFFF dotted thick;
## CSS框模型
    1、CSS内边距padding:在边框与内容之间的空白区域。
		   ①padding属性接受长度值和百分比值，但不允许使用负值。
		   ②padding内边距的百分比数值时相对于其父元素width计算的。
	  2、css外边距合并
         css外边距合并是指，当两个垂直外边距相遇时，它们将形成一个外边距，合并后外边距的高度等于两个发生合并的外边距的高度中较大者。
