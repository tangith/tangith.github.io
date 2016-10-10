---
layout: post
title: learn jquery
description: "About jquery."
tags: [jQuery]
image:
  background: triangular.png
---



{% highlight yaml %}
image:
  background: filename.png
{% endhighlight %}

## jQuery笔记 ##

### 选择器 ###


----------


*标签选择器，id选择器，类选择器，群组选择器，后代选择器，通配符选择器，后代选择器，子选择器，next选择器，nextAll选择器，属性选择器*

- JavaScript操作CSS的语法为`document.getElementById("box").style.fontSize = "14px";`需要注意的是`style`属性只能获取行内的CSS样式，对于另外两种形式内联`<style>`和链接`link`方式则无法获取到，如果想获取到`style`属性获取不到的CSS属性，可以使用`window`对象下提供的`getComputedStyle()`方法。
- jQuery操作CSS的语法为`$(#box).css('color','red');`


`.box.pox{color: red;}   //双class选择器，IE6出现异常`


<br>


	$(".one .intro.demo").css('background','red');    //获取class为one的元素下的class为intro和demo的元素
	
	$("#box p,ul li *").css('color','red');    //获取id为box的元素下的p元素和ul下的li下的所有元素
	
	$("div.box");   //获取class为box的div元素
	
	$("p#box div.side");   //获取id为box的p元素下的class为side的div元素
	
	$(".box.pox");  //获取class为box和pox的元素

**将jQuery对象转换成原生的DOM对象：`$("#box").get(0)`或者`$("#box")[0]`**

**群组选择器：**`$("span,#pox,.box")`选择span元素和id为pox的元素以及class为box的元素

**后代选择器：**`$("ul li a")`

*jQuery为后代选择器提供了一个`find()`方法：`$("#box").find('p');`*

**通配符选择器：**`$("*")`选择所有元素标签的DOM对象

**子选择器：**`$("#box>p");  //获取id为box的子元素p`

*jQuery为子元素选择器提供了一个children()方法*

**next选择器：**`$("#box+p");  //获取id为box的下一个同级的兄弟元素p`

*jQuery为子next选择器提供了一个next()方法*

**nextAll选择器：**`$("#box~p");  //获取id为box的后面所有的同级的兄弟元素p`

*jQuery为子next选择器提供了一个nextAll()方法*

此外，jQuery还提供了更加丰富的方法来选择元素：

	prev()选择同级上一个元素
	prevAll()选择同级所有上面的的元素
	prevUntil()选择同级上非指定元素
	nextUntil()选择同级下非指定元素
	siblings()选择所有同级元素
	
*理论上讲，jQuery提供的方法`find()`,`next()`,`nextAll()`和`children()`运行速度要快于使用高级选择器*

### 过滤选择器 ###

**过滤选择器主要通过特定的过滤规则来筛选出所需的DOM元素，和CSS中伪类的语法类似：使用冒号(:)开头**

	$("li:first");  //选择文档中第一个li元素，需要注意的是，它返回单个元素。如果文档中多个ul下的多个li元素，依然只返回第一个li元素
	$("li:last");  //返回文档中最后一个li元素，依然只返回单个元素
	$("li:not(.rex)");  //返回class不是red的li元素集合
	$("li:even");  //返回索引（0开始）是偶数的li元素集合
	$("li:odd");  //返回索引（0开始）是基数的li元素集合
	$("li:eq(2)");  //返回索引（0开始）等于index的元素，返回单个元素
	$("li:gt(2)");  //返回索引（0开始）大于index的元素集合
	$("li:lt(2)");  //返回索引（0开始）小于index的元素集合
	
	$(":header");  //返回标题元素集合，h1~h6
	$(":animated");  //返回正在执行动画的元素
	
	$(":focus");  //返回当前被焦点的元素
	//需要注意的是，:focus过滤器必须是网页初始状态的已经被激活焦点的元素才能实现元素获取，不是鼠标点击或者Tab键盘敲击激活的

jQuery为常用的过滤器提供了专用的方法，以达到提高性能和效率的作用：

	$("li").eq(2);
	$("li").first();
	$("li").last();
	$("li").not(".red");

**内容过滤器**

	$(":contains('123')");  //返回含有“123”文本的元素
	$(":empty");  //返回不包含子元素或空文本的元素
	$("ul:has(.red)");  //返回子元素含有class为red的元素，注意返回的是ul元素
	$(":patent");  //返回含有子元素或文本的元素，即非空元素

jQuery提供了一个has()方法来提供:has过滤器的性能：

	$("ul").has(".red").css("background","red");  //选择子元素含有class为red的元素

*jQuery提供了一个名称和:parent相似的方法，但这个方法并不是选取含有子元素或文本的元素，而是获取当前元素的父元素，返回的是元素集合*

	$("li").parent();  //选择当前元素的父元素
	$("li").parents();  //选择当前元素的父元素以及祖先元素
	$("li").parentUntil("div");  //选择当前元素遇到div父元素停止

**可见性过滤器**

	$(":hidden");  //选取所有不可见的元素
	$("visible");  //选取所有可见的元素
	

**子元素过滤器**

*和`:first`不同的是，`：first-child`选择的是每一个父元素的第一个元素，返回一个元素集合*

	$("li:first-child");  //获取每一个父元素的第一个子元素
	$("li:last-child");  //获取每一个父元素的最后一个子元素
	$("li:only-child");  //获取父元素只有一个li元素的li元素
	$("li:nth-child(odd/even/eq(index))");

**其他方法**

	is();
	hasClass();
	slice();
	end();
	filter();
	contents();

### 基础DOM和CSS操作 ###

----------

**设置元素及内容**

	html();  //设置和获取元素中的html内容，类似于innerHTML
	text();  //设置和获取元素的文本内容，会自动转移html标签
	val();  //设置和获取表单中的文本内容

使用`val()`设置默认选中的表单：

	$('input').val(["check1","check2","redio1"]);  //value值是这些的将被选定

**设置元素属性**

	attr(key);  //获取某个元素key属性的属性值
	attr(key,value);  //设置某个元素key属性的属性值
	removeAttr();  //删除指定的属性

**元素样式操作**

	css(name);  //获取某个元素行内的css样式
	css([name,name2,name3]);  //获取某个元素行内多个css样式

	css(name,value); //设置某个元素行内的css样式
	css(name1:value1,name2:value2);  //设置某个元素行内多个css样式
	addClass(class);  //给某个元素添加一个css类
	removeClass(class);  //删除某个元素的一个css类
	addClass(class1 class2 class3);  //给元素添加多个css类
	removeClass(class1 class2 class3);  //删除某个元素的多个css类
	toggleClass(class);  //来回切换默认样式和指定样式
	toggleClass(class1 class2 class3);
	toggleClass(class,switch);  //来回切换样式的时候设置切换频率
	toggleClass(function(){});  //通过匿名函数设置切换的规则
	toggleClass(function(){}，switch);  //在匿名函数设置时也可以设置频率

`css([name1,name2,name3])`获取到的是一个对象数组，如何解析:

	var box = $('div').css(['color','height','width']);
	for(var i in box){				//使用传统方式的for in 逐个遍历
		alert(i+':'+box[i]);
	}
	
	$.each(box,function(attr,value){		//使用jQuery提供的$.each()方法轻松遍历对象数组
		alert(attr+':'+box[i]);
	})

**CSS方法**

	width();  //获取和设置某个元素的长度，设置的时候可以直接传数值，默认加px
	width(function(index,width){});  //通过匿名函数设置某个元素的长度
	height();  //获取和设置某个元素的长度
	height(function(index,width){});
	
	innerWidth();  //获取元素宽度，包含内边距padding
	innerHeight(); //获取元素高度，包含内边距padding
	outerWidth();  //获取元素宽度，包含边框border和内边距padding
	outerHeight();  //获取元素高度，包含边框border和内边距padding
	outerWidth(true);  //同上且包含外边距
	outerHeight(true);  //同上且包含外边距
	
	offset();  //获取某个元素相对于视口的偏移位置，返回一个对象
	//使用left和top属性
	position();  //获取某个元素相对于父元素的偏移位置
	scrollTop();  //获取和设置垂直滚动条的值
	scrollLeft();  //获取和设置水平滚动条的值

### DOM节点操作 ###

---

**创建节点**

	var box = $('<div id="box">节点</div>');  //创建一个节点
	$('body').append(box);  //将节点插入到<body>元素内部

**插入节点**

	append(content);  //向指定元素内部后面插入节点content
	append(function(index,html){});  //使用匿名函数向指定元素内部后面插入节点
	appendTo(content);  //将指定元素移入到指定元素content内部后面
	prepend(content);  //向指定元素content内部的前面插入节点
	prepend(function(){index,html});  //使用匿名函数向指定元素内部的前面插入节点
	prependTo(content);  //将指定元素移入到指定元素content内部里面
	
	after(content);  //向指定元素的外部后面插入节点content
	after(function(index,html){});  //使用匿名函数向指定元素的外部后面插入节点
	before(content);  //向指定元素的外部前面插入节点content
	before(function(index,html){});  //使用匿名函数向指定元素的外部前面插入节点
	insertAfter(content);  //将指定节点移到指定元素content外部的后面
	insertBefore(content);  //将指定节点移到指定元素content外部的前面
	
	wrapp(html);  //向指定元素包裹一层html代码
	wrap(element);  //向指定元素包裹一层DOM对象节点
	unwrap();  //移除一层指定元素包裹的内容
	wrapAll();  //用html将所有元素包裹在一起
	wrapInner(html);  //向指定元素的子内容包裹一层html
	wrapInner(element);  //向指定元素的子内容包裹一层DOM对象节点
	
	clone();  //复制一个节点
	clone(true);  //参数加上true表示把这个元素附带的事件处理行为也复制出来
	remove();  //删除节点
	detach();  //保留事件的删除节点
	empty();  //清空节点
	$('div')replaceWith($('span'));   //将dic替换成span
	$('span').replaceAll($('div'));   //效果同上

*节点被替换后，所包含的事件行为就全部消失了*

### 表单选择器 ###

---

**常规选择器**

	$('input[type=password]');
	$(':input');
	$(':text');
	//password,redio,checkbox,submit,reset,image,button,file,hidden
	//表单过滤器
	$(':enable');  //选取所有可用元素
	$(':disable');  //选取所有不可用元素
	$(':checked');  //选取所有被选中的元素，单选和复选字段
	$(':select');  //选取所有被选中的元素，下拉列表

### 基础事件 ###

---

常用的事件有click,dblclick,mousedown,mouseup,mousemove,mouseover,mouseout,change,select,submit,keydown,keypress,keyup,blur,focus,load,resize,scroll,error....

jQuery使用`.bind()`方法来为元素绑定这些事件。语法：`bind(type,[data],fn)`,`type`表示一个或多个类型的事件名字符串；`[data]`是可选的，作为`event.data`属性值传递一个额外的数据，这个数据是一个字符串、一个数字、一个数组或者一个对象；`fn`表示绑定到指定元素的处理函数。


**绑定事件**


	//使用点击事件
	$('input').bind('click',function(){  //点击按钮后执行匿名函数
		alert('点击');
	});
	
	//普通处理函数
	$('input').bind('click',fn);  //执行普通函数式无须圆括号
	function fn(){
		alert('点击');
	}
	
	//可以同时绑定多个事件
	$('inout').bind('mouseout mouseover',function(){  //移入和移除分别执行一次
		$('div').html(function(index,value){
			return value+'1';  //value表示div里面原有的内容
		})
	})
	
	//通过对象键值对绑定多个参数
	$('input').bind({			//传递一个对象
		'mouseout':function(){		//事件名的引号可以省略
			alert('移除');
		},
		'mouseover':function(){
			alert('移入');
		}
	})；
	
	//使用unbind删除绑定的事件
	$('input').unbind();		//删除所有当前元素的事件
	
	//使用unbind参数删除指定类型事件
	$('input').unbind('click');		//删除当前元素的click事件
	
	//使用unbind参数删除指定处理函数的事件
	function fn1(){
		alert('点击1');
	}
	function fn2(){
		alert('点击2');
	}
	$('input').bind('click',fn1);
	$('input').bind('click',fn2);
	$('input').unbind('click',fn1);		//只删除fn1处理函数的事件

**简写事件**

	//方法名				触发条件				描述
	click(fn)			  鼠标					单击
	dblclick(fn)		  鼠标					双击
	mousedown(fn)		  鼠标
	mouseup(fn)			  鼠标
	mouseover(fn)		  鼠标
	mouseout(fn)		  鼠标
	mousemove(fn)
	mouseenter(fn)								鼠标穿过
	mouseleave(fn)								鼠标穿出
	keydown(fn)			  键盘					键盘按下
	keyup(fn)
	keypress(fn)
	unload(fn)			  文档					当卸载本页面时绑定一个要执行的函数
	resize(fn)			  文档					文档大小改变
	scroll(fn)			  文档					滚动条拖动
	focus(fn)			  表单					焦点激活
	blur(fn)			  表单					焦点丢失
	focusin(fn)			  表单					焦点激活
	focusout(fn)		  表单					焦点丢失
	select(fn)			  表单					文本选定
	change(fn)			  表单					表单的值改变
	submit(fn)

*`.mouseenter()`和`.mouseleave()`这组穿过子元素不会触发，而`.mouseover()`和`.mouseont()`则会触发*

*`.focus()`和`.blur()`分别表示光标激活和丢失，事件触发时机是当前元素。而`.focusin()`和`.focusout()`也表示光标激活和丢失，但事件触发时机可以子元素*

**复合事件**

	ready(fn)		//当DOM加载完毕触发事件
	hover([fn1,]fn2)		//可以传入多个方法，结合的是.mouseenter()和.mouseleave()

### 事件对象 ###

---

事件对象就是event对象，通过处理函数默认传递接受。之前处理函数的e就是event事件对象，event对象有很多可用的属性和方法。

	$('input').bind('click',function(e){		//接受事件对象参数
		alert(e);
	});

event对象的属性：

	type					获取这个事件的事件类型，例如：click
	target					获取绑定事件的DOM元素
	date					获取事件调用时的额外数据
	relatedTarget			获取移入移出目标点离开或进入的那个DOM元素
	currentTarget			获取冒泡前触发的DOM元素，等同于this
	pageX/pageY				获取相对于页面远点的水平/垂直坐标
	screenX/screenY			获取显示器屏幕位置的水平/垂直坐标（非jQuery封装）
	clientX/clientY			获取相对于页面视口的水平/垂直坐标（非jQuery封装）
	result					获取上一个相同事件的返回值
	timeStamp				获取事件触发的事件戳
	which					获取鼠标的左中右键（1,2,3），或获取键盘按键
	altKey/shiftKey/ctrlKey/metaKey		获取是否按有alt、shift、ctrl（这三个非jQuery封装）或meta键（IE原生meta键，jQuery做了封装）

*`event.target`得到的是触发元素的DOM，`event.currentTarget`得到的是监听元素的DOM，而`this`也是得到监听元素的DOM*

**冒泡和默认行为**

如果在页面中重叠了多个元素，并且重叠的这些元素都绑定了同一个元素，那么就会出现冒泡问题。从小范围到大范围，一层一层往上。

jQuery提供了一个事件对象方法：`event.stopPropagation()`,这个方法设置到需要触发的事件上时，所有上层的冒泡行为都将被取消。

	$('input')click(function(e){
		alert('按钮被触发了');
		e.stopPropagation();	//取消了所有上层的冒泡行为
	})

网页中的元素，在操作的时候会有自己的默认行为。使用`event.preventDefault();`来取消默认行为。

	//禁止提交表单
	$('form').submit(function(e){
		e.preventDefault();
	});
	//禁止a链接跳转
	$('a').click(function(e){
		e.preventDefault();
	});
	
	$('a').click(function(e){		//取消多个默认时事件可以直接返回一个false
		return false;
	});

取消和默认行为的一下方法：

	preventDefault()			取消某个元素的默认行为
	isDefaultPrevented()		判断是否调用了preventDefault()方法
	stopPropagation()			取消事件冒泡
	isPropagationStopped()		判断时候调用了stopPropagation()方法
	stopImmediatePropagation()	取消事件冒泡，并取消改事件的后续事件处理函数
	isImmediatePropagationStopped()		判断是否调用了stopImmediatePropagation()方法

### 高级事件 ###

---

**模拟操作**

	$('input').click(function(){
		alert('点击');
	});
	$('input').trigger('click');		//模拟用户点击行为
	
	//可以合并两个方法
	$('input').click(function(){
		alert('点击');
	}).trigger('click');

`.trigger()`方法提供了简写方案，只要想让某个事件执行模拟用户行为，直接再调用一个空的同名事件即可。

	$('input').click(function(){
		alert('模拟点击');
	})click();

*这种方法还可以用在其他常用的事件中*

jQuery还提供了另外一个模拟用户行为的方法：`.triggerHandle()`

两者之间的差异：

- `.triggerHandler()`方法并不会触发事件的默认行为，而`.trigger()`会。
- `.triggerHandler()`方法只会影响第一个匹配到的元素，而`.trigger()`会影响所有。
- `.triggerHandler()`方法会返回当前事件执行的返回值，如果没有返回值，则返回`undefined`；而`.trigger()`则返回当前包含事件触发元素的jQuery对象（方便链式连缀调用）。
- `.trigger()`在创建事件的时候，会冒泡。但这种冒泡是自定义事件才能体现出来，是jQuery扩展与DOM的机制，并非DOM特性。而`.triggerHandler()`不会冒泡。

**命名空间**

有时，我们想对事件进行移除。但对于同名元素绑定的事件移除往往比较麻烦，这个时候，可以使用事件的命名空间解决。

	$('input').bind('click.abc',functiion(){
		alert('abc');
	});
	$('input').bind('click.xyz',functiion(){
		alert('xyz');
	});
	$('input').unbind('click.abc');			//移除click事件中命名空间为abc的

**事件委托**

在DOM中很多元素绑定相同事件时，和在DOM中尚不存在即将生成的元素绑定事件时，推荐使用事件委托的绑定方式，否则推荐使用`.bind()`的普通绑定。

**on、off和one**

普通绑定`bind`，普通解绑`unbind`;

事件委托`live`，`delegate`

解除委托`die`，`undelegate`

其中，`live`和`die`已经废除了。

jQuery1.7以后推出了`.on()`和`.off()`方法彻底摒弃了以前绑定事件和解绑的方法。

	$('.button').on('click',function(){
		alert('替代.bind()');
	});

不管是`.bind()`还是`.on()`，绑定事件后都不是自动移除事件的，需要通过`.unbind()`和`.off()`来手工移除。jQuery提供了`.one()`方法，绑定元素执行完毕后自动移除事件。

### 动画效果 ###

---

**显示、隐藏**

jQuery中显示方法为`.show()`,隐藏方法为`.hide()`,在没有参数的时候只是硬性的显示和隐藏内容。

	$('#box').on('click',function(){
		$(this).show();					//显示，可以传递一个参数，以毫秒来控制速度
	});

除了使用毫秒来控制速度，jQuery还提供了三种预设速度参数字符串：`slow`、`normal`、`fast`，分别对应600毫秒、400毫秒和200毫秒。如果参数传递错误，会采用默认值为400毫秒。

	//列队动画，使用函数名调用自身
	$('.show').click(function(){
		$('div').first().show('fast',function showSpan(){
			$(this).next().show('fast'.showSpan);
		});
	});
	
	//列队动画，使用arguments.callee匿名函数自调用
	$('.hide').click(function(){
		$('div').last().hide('fast',function(){
			$(this).prev().hide('fast',arguments.callee);
		});
	});

我在使用`.show()`和`.hide()`的时候，如果需要一个按钮切换操作，需要进行一些条件判断。而jQuery提供了我们一个类似功能的独立方法：`.toggle()`。

	$('a').on('click',function(e){
		e.preventDefault();				//阻止a链接的默认事件
		$('#box').toggle('slow');
	});

**滑动、卷动**

jQuery提供了一组改变元素高度的方法：`.slideUp()`、`.slideDown()`、`slideToggle()`。和显示、隐藏一样具有相同的参数。

**淡入、淡出**

jQuery提供了一组专门用于透明度变化的方法：`.fadeIn()`、`.fadeOut()`分别表示淡入、淡出。当然还有一个自动切换的方法：`.fadeToggle()`。和显示、隐藏具有相同的参数。

上面三个透明度都是在0到100之间变化的。如果想设置指定值可以使用`.fadeTo()`

	$('#box').click(function(){
		$('#pox').fadeTo('slow',0.33);
	});


**自定义动画**

jQuery使用`.animate()`方法来创建自定义动画。

	$('#box').click(function(){
		$(this).animate({
			'width':'300px',
			'height':'200px',
			'fontSize':'50px'
		});
	});

必传的参数只有一个，就是一个键值对CSS变化样式的对象。还有两个可选参数分别为速度和回调函数。

	$('#box').click(function(){
		$(this).animate({
			'widht':'300px',
			'height':'200px'
		},3000,function(){
			alert('动画执行完了');
		});
	});

`.animate()`还有一个参数，easing运动方式，自带的参数有两个：`swing`(缓动)、`linear`(匀速)、默认为`swing`。

如果想实现运动状态的位移动画，就必须使用自定义动画，并且结合CSS的绝对定位功能。

	$('#box').click(function(){
		$(this).animate({
			'top':'300px',				//必须先设置CSS绝对定位
			'left':'200px'
		});
	});

自定义动画中，每次开始运动都必须是初始位置或者初始状态。如果我们想通过当前位置或者状态这再进行动画，jQuery提供了自定义动画的累加、累减功能。

	$('#box').click(function(){
		$(this).animate({
			'left':'+=100px'
		});
	});

自定义实现队列动画的方式有两种：1.在回调函数中再执行一个动画；2.通过连缀或顺序来实现队列动画。

	//通过依次顺序实现队列动画
	$('.animate').click(function(){					//如果不是同一个元素，就会实现同步动画
		$('#box').animate({'left':'100px'});
		$('#box').animate({'top':'100px'});
		$('#box').animate({'width':'100px'});
	});
	
	//通过连缀实现队列动画
	$('#box').click(function(){
		$(this).animate({
			'left':'100px'
		}).animate({
			'top':'100px'
		}).animate({
			'width':'300px'
		});
	});
	
	//通过回调函数实现队列动画
	$('#box').click(function(){
		$('.one').animate({
			'left':'100px'
		},function(){
			$('.one').animate({
				'top':'100px'
			},function(){
				$('.one').animate({
					'width':'300px'
				});
			});
		});
	});

**队列动画方法**

之前我们已经可以实现队列动画了，如果是同一个元素，可以一次顺序或连缀调用。如果是不同元素，可以使用回调函数。但有时队列动画太多了，回调函数的可读性大大降低。为此，jQuery提供了一组专门用于队列动画的方法。

	//连缀无法实现按顺序队列
	$('#box').slideUp('slow').slideDown('slow').css('background','orange');

如果是动画方法，连缀可以实现依次队列，但是`.css()`不是动画方法，会在一开始传入队列。那么，可以采用动画方法的回调函数来解决。

	//使用回调函数，强行将.css()方法排队到.slideDown()之后
	$('#box').slideUp('slow').slideDown('slow',function(){
		$(this).css('background','orange');
	});

但如果这样的话，当队列动画繁多的时候，可读性不但下降，而原本的动画方法不够清晰。所以，jQuery提供了一个类似回调函数的方法：`.queue()`。

	//使用.queue()方法模拟动画方法跟随动画方法之后
	$('#box').slideUp('slow').slideDown('slow').queue(function(){
		$(this).css('background','orange');
	});

jQuery的`.queue()`的回调函数可以传递一个参数，这个参数是next函数，在结尾处调用这个`next()`方法即可再连缀执行队列动画。

	//使用next参数来实现继续调用队列动画
	$('#box').slideUp('slow').slideDown('slow').queue(function(next){
		$(this).css('background','orange');
		next();
	}).hide('slow');

由于next函数时jQuery 1.4版本之后才出现的，在这之前使用的是`.dequeue()`方法。意思是执行下一个元素队列中的函数。

	//使用.dequeue()方法执行下一个函数动画
	$('#box').slideUp('slow').slideDown('slow').queue(function(){
		$(this).css('background','orange');
		$(this).dequeue();
	}).hide('slow');

如果采用顺序调用，那么使用队列动画方法，就非常清晰了，每一段代表一个队列，而回调函数的嵌套就会杂乱无章。

	//使用顺序调用的队列，逐个执行，非常清晰
	$('#box').slideUp('slow');
	$('#box').slideDown('slow');
	$('#box').queue(function(){
		$(this).css('background','orange');
		$(this).dequeue();
	});
	$('#box').hide('slow');

jQuery还提供了一个清理队列的功能方法：`.clearQueue()`。把它放入一个队列的回调函数或`.queue()`方法里，就可以把剩下未执行的队列给移除。

	//清理动画
	$('#box').slideDown('slow',function(){$(this).clearQueue()});

**动画相关方法**

jQuery提供了一个停止正在运行中的动画的方法：`.stop()`。它有两个可选参数：`.stop(cleatQueue,gotoEnd)`;`cleatQueue`传递一个布尔值，代表是否清空未执行完的动画队列，`gotoEnd`代表是否直接将正在执行的动画跳转到末状态。

	//强行停止运行中的动画
	$('.stop').click(function(){
		$('#box').stop();
	});

有时在执行动画或者队列的时候，需要在运动之前延迟执行，jQuery为此提供了`.delay()`方法.这个方法可以在动画之前设置延迟，也可以在队列动画中间加上。

	$('#box').click(function(){
		$(this).delay(1000).hide();		//延迟1s执行
	});

在选择器的章节中，有一个过滤器`:animated`，这个过滤器可以判断出当前运动的动画是哪个元素。

	//递归执行自我，无限循环播放
	$('#box').slideToggle('slow',function(){
		$(this).sideToggle('slow',arguments.callee);
	});

	//停止正在运动的动画，并且设置红色背景
	$('.button').click(function(){
		$('div:animaged').stop().css('background','red');
	});

**动画全局属性**

jQuery提供了两种全局设置的属性，分别为：`$.fx.interval`，设置每秒运行的帧数；`$.fx.off`，关闭页面上所有的动画。

`$.fx.intercal`属性可以调整动画每秒的运行帧数，默认为13毫秒。数字越小越流畅，但可能影响浏览性能。

`$.fx.off`属性可以关闭所有动画效果，在非常低端的浏览器，动画可能会出现各种异常问题导致错误。而jQuery设置这个属性，就是用于关闭动画效果的。

	$.fx.off=true;

### Ajax ###

---

异步JavaScript和XML，可以无刷新状态更新页面，并且实现异步提交。

优点：

- 不需要插件支持
- 用户体验极佳
- 提升Web程序的性能
- 减轻服务器和带宽的负担

不足：

- 不同版本的浏览器对XMLHttpRequest对象支持度不足
- 前进、后退的功能被破坏
- 搜索引擎的支持度不够
- 开发调试工具缺乏

jQuery对Ajax做了大量封装。对于封装的方式，jQuery采用三层封装：最底层的封装方法为：`$.ajax()`，而通过这层封装了第二层有三种方法：`.load()`、`$.get()`和`$.post()`,最高层的是`$.setScript()`和`$.getJSON()`方法。

	//使用Ajax异步载入一段HTML内容
	
	//HTML
	<input type="button" value="载入" >
	<div id="box"></div>
	
	//jQuery
	$('input').click(function(){
		$('#box').load('test.html');	//test.html在同目录
	});

	//如果要对载入的HTML进行筛选，可以在url参数后面跟着一个选择器。如：$('#box').load('test.html .a');
	
	//test.html
	<span class="a">aJax</span>
	<span class="b">html</span>

如果是服务器文件，比如php。一般不仅需要载入数据，还需要向服务器提交数据，那么我们就可以使用第二份可选参数data。想服务器提交数据有两种方式：`get`和`post`。

	//不传递data，则默认get方式
	$('input').click(function(){
		$('#box').load('test.php?url=thisang');
	});

	//get方式接收的php
	<?php
		if($_GET['url']=='thisang'){		//post方式接收为$_post
			echo'thisang';
		}else{
			echo'未知的';
		}
	？>

	//传递data，则为post方式
	$('input').click(function(){
		$('#box').load('test.php',{
			url:'thisang'
		})
	});

post提交不能使用问号传参；post提交可以使用字符串形式的键值对传参，自动转化为http消息实体传参；post提交可以使用对象键值对。

在Ajax数据载入完毕之后，就能执行回调函数callback，也就是第三个参数。回调函数也可以传递三个可选参数：`responseText`(请求返回)、`textStatus`（请求状态）、`XMLHttpRequest`（XMLHttpRequest对象）。

	$('input').click(function(){
		$('#box').load('test.php',{
			url:'thisang'
		},function(response,status,xhr){
			alert('返回的值为：'+response+'，状态为：'+status+',状态是：'+xhr.statusText);
		});
	});

注意：`status`得到的值，如果成功返回数据则为：`success`，否则为：`error`。XMLHttpRequest对象属于JavaScript范畴，可以调用如下一些属性：

	responseText			作为相应主体被返回的文本
	responseXML				如果相应主体内容类型是"text/xml"或者"application/xml"，则返回包含相应数据的XML DOM文档
	status					相应的HTTP状态
	statusText				HTTP状态的说明

如果成功的返回数据，那么xhr对象的`statusText`属性则返回‘OK’字符串。除了‘OK’的状态字符串，`statusText`属性还提供了一系列其他的值：

	//HTTP状态码			状态字符串				说明
	200					OK						服务器成功反悔了页面
	400					Bad Request				语法错误导致服务器不识别
	401					Unauthorized			请求需要用户认证
	404					Not found				指定的URL在服务器上找不到
	500					Internal Server Error	服务器遇到意外错误，无法完成请求
	503					ServiceUnavailable		由于服务器过载或维护导致无法完成请求

**$.get()和$.post()**

`.load()`方法是局部方法，因此它需要一个包含元素的jQuery对象作为前缀。而`$.get()`和`$.post()`是全局方法，无须指定某个元素。对于用途而言，`.load()`适合做静态文件的异步获取，而对于需要传递参数到服务器页面的，`$.get()`和`$.post()`更加适合。

`$.post()`和`$.get()`的区别：

- GET请求是通过URL提交的，而POST请求则是HTTP消息实现提交的；
- GET提交有大小限制（2KB），而POST方式不受限制；
- GET方式会被缓存下来，可能有安全性问题，而POST没有这个问题；
- GET方式通过$_GET[]获取，POST通过$_POST[]获取；

**$.getScript()和$.getJSON()**

jQuery提供了一组用于特定异步加载的方法：`$.getScript()`，用于加载特定的JS文件；`$.getJSON()`，用于专门加载JSON文件。

	//点击按钮再加载JS文件
	$('input').click(function(){
		$.getScript('test.js');
	});

**$.ajax()**

`$.ajax()`是所有ajax方法中最底层的方法，所有其他方法都是基于`$.ajax()`方法的封装。这个方法之后一个参数，传递一个各个功能键值对的对象。

	$('input').click(function(){
		$.ajax({
			type:'POST',
			url:'test.php',
			data:{
				url:'thisang'
				},
			success:function(response,status,xhr){
				$('#box').html(response);
			}
		});
	});

**表单序列化**

传统的表单操作是通过submit提交将数据传输到服务器端。如果使用Ajax异步处理的话，我们需要将每一个表单元素逐个获取才能提交，这样工作效率大大降低。

	//常规形式的表单提交
	$('form input[type=button]').click(function(){
		$.ajax({
			type:'POST',
			url:'test.php',
			data:{
				user:$('form input[name=user]').val(),
				email:$('form input[name=email]').val()
			},
			success:function(response,status,xhr){
				alert(reponse);
			}
		});
	});

使用表单序列化方法`serialize()`，会智能的获取指定表单内的所有元素。这样，在面对大量表单元素的时候，会把表单内容序列化为字符串，然后再使用Ajax请求。

	$使用.serialize()序列化表单内容
	$('form input[type=button]').click(function(){
		$.ajax({
			type:'POST',
			url:'test.php',
			data:$('form').serialize(),
			success:function(response,status,xhr){
				alert(response);
			}
		});
	});

`.serialize()`方法不但可以序列化表单元素，还可以直接获取单选框、复选框和下拉列表等内容。

	//使用序列化得到选中的元素内容
	$(':radio').click(function(){
			$('#box').html(decodeURIComponent($(this).serialize()));
		});

除了`.serialize()`方法，还有一个可以返回JSON数据的方法：`.serializeArray()`。这个方法直接把数据整合成键值对的JSON对象。

	$('radio').click(function(){
		console.log($(this).serializeArray());
		var json=$(this).serializeArray();
		$('#box').html(json[0].value);
	});

有时候，我们可能会在同一个程序中多洗调用`$.ajax()`方法。而他们很多参数都相同，这个时候我们可以使用jQuery提供的`$.ajaxSetup()`请求默认值来初始化参数。

	$('form input[type=button]').click(function(){
		$.ajaxSetup({
			type:'POST',
			url：'test.php',
			data:$('form').serialize()
		});
		$.ajax({
			success:function(resposse,status,xhr){
				alert(response);
			}
		});
	});

在使用data属性传递的时候，如果是以对象形式传递键值对，可以使用`$.param()`方法将对象转换为字符串键值对格式。

	var obj={a:1,b:2,c:3};
	var form=$.param(obj);
	alert(form);

### Ajax进阶 ###

---

**加载请求**

jQuery提供了两个全局事件：`.ajaxStart()`和`.ajaxStop()`。这两个全局事件，只要用户触发了Ajax，请求开始时（未完成其他请求）激活`.ajaxStart()`，请求结束时（所有请求都结束了）激活`.ajaxStop()`。

	//请求加载提示的显示和隐藏
	$('.loading').ajaxStart(function(){
		$(this).show();
	}).ajaxStop(function(){
		$(this).hide();
	});

以上代码在jQuery1.8及以后的版本不再有效，需要使用jquer-migrate想下兼容才行。新版本中，必须绑定在`document`元素上。

	$(document).ajaxStart(function(){
		$('.loading').show();
	}).ajaxStop(function(){
		$('.loading').hide();
	});

	//如果请求时间太长，可以设置超时
	$.ajax({
		timeout:500
	});

	//如果某个ajax不想触发全局函数，可以设置取消
	$.ajax({
		global:false
	});

**错误处理**

Ajax异步提交时，不可能所有情况都是成功完成的，也有因为代码异步提交错误、网络错误导致提交失败的。这时，我们应该把错误报告出来，提醒用户重新提交或者提示开发者进行修补。

在之前高层封装中是没有回调错误处理的，比如`$.get()`、`$.post()`和`.load()`。所以，早期的方法是通过全局`.ajaxError()`事件方法来返回错误信息。而在jQuery1.5之后，可以通过连缀处理局部`.error()`方法即可。而对于`$.ajax()`方法，不但可以用这两种方法，还有自己的属性方法`error:function(){}`。

	//$.ajax()使用属性提示错误
	$.ajax({
		type:'POST',
		url:'test.php',
		data:$('form').serialize(),
		success:function(response,status,xhr){
			$('#box').html(response);
		},
		error:function(xhr,errorText,errorStatus){
			alert(xhr,status+':'+xhr.starusText);
		}
	});

	//$.post()使用连缀.error()方法提示错误，连缀方法将被.fail()取代
	$.post('test.php').error(function(xhr,status,info){
		alert(xhr.status+':'+xhr,statusText);
		alert(status+':'+info);
	});

	//$.post()使用全局函数.ajaxError()事件提示错误
	$(document).ajaxError(function(event,xhr,setting,infoError){
		alert(xhr,status+':'+xhr.statusText);
		alert(setting+':'+info);
	});

**请求全局事件**

jQuery对于Ajax操作提供了很多全局事件方法，`.ajaxStart()`、`.ajaxStop()`、`.ajaxError()`等事件方法。它们都属于请求时触发的全局事件，除了这些，还有一些其他全局事件。

`.ajaxSuccess`对应一个局部方法:`.success()`,请求成功完成时执行。

`.ajaxComplete()`对应一个局部方法:`.complete()`,请求完成后注册一个回调函数。

`.ajaxSend()`，没有对应的局部方法，只有属性`beforeSend`,请求发送之前要绑定的函数。

	//$.post()使用局部方法.success()
	$.post('test.php',$('form').serialize(),function(response,status,xhr){
		$('#box').html(response);
	}).success(function(response,status,xhr){
		alert(response);
	});

	//$.post()使用全局事件方法.ajaxSuccess()
	$(document).ajaxSuccess(function(event,xhr,setting){
		alert(xhr.responseText);
	});

全局事件方法是所有Ajax请求都会触发到，并且只能绑定在`document`上。而局部方法，则是针对某个Ajax。

对于一些全局事件方法的参数，大部分为对象，而这些对象有哪些属性或方法能调用，可以通过遍历方法得到。

	//遍历setting对象的属性
	$(document).ajaxSuccess(function(event,xhr,setting){
		for(var i in setting){
			alert(i);
		}
	});

	//$.post()请求完成的局部方法.complete()
	$.post('test.php',$('form').serialize(),function(response,status,xhr){
		alert('成功');
	}).complete(function(xhr,status){
		alert('完成');
	});

	//$.post()请求完成的全局方法.ajaxComplete()
	$(document).ajaxComplete(function(event,xhr,setting){
		alert('完成');
	});

	//$.post()请求发送之前的全局方法.ajaxSend()
	$(document).ajaxSend(function(event,xhr,setting){
		alert('发送请求之前');
	});

	//$.ajax()方法，可以直接通过属性设置即可
	$.ajax({
		type:'POST',
		url:'test.php',
		data:$('form').serialize(),
		success:function(response,status,xhr){
			$('#box').html(response);
		},
		complete:function(xhr,status){
			alert('完成'+'-'+xhr,responseText+'-'+status);
		},
		beforeSend:function(xhr,setting){
			alert('请求之前'+'-'+xhr.readyState+'-'+setting.url);
		}
	});

在jQuery1.5版本以后，使用`.success()`、`.error()`和`.complete()`连缀的方法，可以用`.done()`、`.fail()`和`.always()`取代。

**JSON和JSONP**

在同一个域下，`$.ajax()`方法只要设置`dataType`属性即可加载JSON文件。

	//$.ajax()加载JSON文件
	$.ajax({
		type:'POST',
		url:'test.json',
		dataType:'json',
		sunccess:function(response,status,xhr){
			alert(response[0].url);
		}
	});

如果想跨域操作文件的话，我们就必须使用JSONP。JSONP（JSON with Padding）是一个非官方的协议，它允许在服务器端集成Script tags返回至客户端，通过JavaScript callback的形式实现跨域访问（这仅仅是JSONP简单的实现形式）。

	//跨域的PHP文件
	<?php
		$arr=array('a'=>1,'b'>=2,'c'>=3,'d>=4','e'>=5);
		$result=json_encode($arr);
		$callback=$_GET['callback'];
		echo $callback."($result)";
	?>

	//$.getJSON()方法跨域获取JSON
	$getJSON('http://www.li.cc/test.php?callback=?',function(response){
		console.log(response);
	});

	//$.ajax()方法跨域获取JSON
	$.ajax({
		url:'http://www.li.cc/test.php?callback=?',
		dataType:'jsonp',
		success:function(response,status,xhr){
			console.log(response);
			alert(response.a);
		}
	});

**jsXHR对象**

在之前，我们使用了局部方法：`.success()`、`.complete()`和`.error()`。这三个局部方法并不是`XMLHttpRequest`对象调用的，而是`$.ajax()`之类的全局方法返回的对象调用的。这个对象就是`jqXHR`对象，它是原生对象XHR的一个超集。

`jqXHR`对象就是`$.ajax()`返回的对象。

如果使用`jqXHR`对象的话，建议使用`.done()`、`.alway()`和`.fail()`代替`.success()`、`.conplete()`和`.error()`。因为在未来的版本中，很可能这三种方法会被废弃取消。

	//成功后回调函数
	jqXHR.done(function(response){
		$('#box').html(response);
	});

使用`jqXHR`的连缀方式比`$.ajax()`的属性方式有三大好处：

1.  可以连缀操作，可读性大大提高；
2.  可以多次执行同一个回调函数；
3.  为多个操作指定回调函数；

`jqXHR.done().done();`	//同时执行多个成功后的函数

	//多个操作指定回调函数
	var jqXHR=$ajax('test,php');
	var jqXHR2=$ajax('test2.php')

	$.when(jqXHR,jqXHR2).done(function(r1,r2){
		alert(r1[0]);
		alert(r2[0]);
	});

### 工具函数 ###

---

工具函数是指直接依附于jQuery对象，针对jQuery对象本身定义的方法，即全局性的函数。它的作用主要是提供比如字符串、数组、对象等操作方面的遍历。

**字符串操作**

在jQuery中，字符串的工具函数只有一个，就是去除字符串左右空格的工具函数：`$.trim()`。

	var str = '    ang    ';
	$.trim(str);

**数组和对象操作**

jQuery为处理数组和对象提供了一些工具函数，这些函数可以遍历的给数组或对象进行遍历、筛选、搜索等操作。

	//$.each()遍历数组
	var arr=['张三','李四'，'王五','马六'];
	$.each(arr,function(index,value){function(){
		$('#box').html($('#box').html()+index+'.'+value+'<br />');
	}});

	//$.each()遍历对象
	$.each($.ajax(),function(name,fn){
		$('#box'),html($('#box'),html()+index+'.'+value+'<br />');
	});

注意：`$.each()`中`index`表示数组元素的编号，默认从0开始。

	//$.gerp()数组筛选
	var arr = [5,2,3,6,9,45,22,8];
	var arrGrap = $.grep(arr,function(element,index){
		return element < 6 && index < 5;
	});

注意：`$.grep()`方法的`index`是从0开始计算的。

	//$.map()修改数据
	var arr = [5,2,3,9,11,25,35,4,3];
	var arrMap = $.map(arr,function(element,index){
		if(element < 6 && index < 5){
			return element + 1;
		}
	});

	//$.inArray()的下标从0开始计算
	var arr = [5,2,3,4,11,54,89,1,23];
	var arrInArray = $.inArray(1,arr);
	alert(arrInArray);

注意：`$,inArray()`的下标是从0开始的。

	//$.unique()删除重复的DOM元素
	<div></div>
	<div></div>
	<div class="box"></div>
	<div class="box"></div>
	<div class="box"></div>
	<div></div>

	var divs = $('div').get();
	divs = divs.concat($('.box').get());
	alert($(divs).size());
	$.unique(divs);
	alert($(divs).size());

`.toArray`合并多个DOM元素组成数组

	$('li').toArray();

**测试操作**

在jQuery中，数据有着各种类型和状态。有时，我们希望能通过判断数据的类型和状态做相应的操作。jQuery提供了五组测试用的工具函数。

	$.isArray(obj)			//判断是否为数组对象，是返回ture
	$.isFunction(obj)		//判断是否为函数，是返回ture
	$.isEmptyObject(obj)	//判断是否为空对象，是返回true
	$.isPlainObject(obj)	//判断是否为纯粹对象，是返回true
	$.contains(obj)			//判断DOM节点是否含有另一个DOM对象，是返回true
	$.type(data)			//判断数据类型
	$.isNumeric(data)		//判断数据是否为数值
	$.isWindow(data)		//判断数据是否为window对象

如果使用`new Object('name');`传递参数后，返回类型已不是`Object`，而是字符串，所以就不是纯粹的原始对象了。

	//判断第一个DOM节点是否包含有第二个DOM节点,需要使用原生JavaScript DOM，而非jQuery对象
	alert($.contains($('#box').get(0),$('#pox'),get(0)));

**URL操作**

URL地址操作只有一个方法：`$.param()`,将对象的键值对转化为URL键值对字符串形式。

	//$.param()将对象键值对转换为URL字符串键值对
	var obj={
		name:'ang',
		age:'20'
	};
	alert($.param(obj));	//name=ang&age=20

**浏览器检测**

早期的jQuery提供了`$.bowser`工具对象，而现在已经废弃了这个工具对象，如果还想使用这个对象来获取浏览器版本型号的信息，可以使用兼容插件。

`$.bowser`对象属性:

	webkit			//判断webkit浏览器，是返回true
	mozilla			//判断mozilla浏览器，是返回true
	safari			//判断Safari浏览器
	opera			//判断opera浏览器
	msie			//判断IE浏览器
	version			//获取浏览器版本号

`$.support`对象部分属性:

	Ajax			//如果浏览器支持ajax操作，则返回true
	opacity			//如果浏览器能适当解释透明度样式属性，则返回true，目前在IE中返回false，因为他用alpha滤镜代替
	...

**其他操作**

jQuery提供了一个预备绑定函数上下文的工具函数：`$.proxy()`。这个方法，可以解决诸如外部事件触发调用对象方法时`this`的指向问题。

	//$.proxy()调整this指向
	var obj={
		name:'ang',
		test:function(){
			alert(this.name);
		}
	};

	$('#box').click(obj.test);					//指向this为#box元素
	$('#box').click($.proxy(obj,'test'));		//指向的this为方法属于对象box

### 知问前端 ###

---

设置网页的`favicon.icon`:

	<link rel="short icon" type="image/x-icon" href="img/favicon.ico" />

**jQuery UI dialog**

开启多个dialog

	$('#reg').dialog();
	$('#login').dialog();

修改dialog样式中header的背景图

	.ui-widget-header{
		background:url(../img/ui_header_bg,png);
	}

`dialog()`方法的属性:

	title			对话框的标题
	buttons			以键值对的方式，给dialog添加按钮。
	position		这只对话框的位置。默认为center。其他设置值为：left top、top right、bottom left、right bottom、top、bottom、left、right、center。
	width			
	height
	minWidth
	minHeight
	maxWidth
	maxHeight
	show			默认为false，淡入效果
	hide			默认为false，淡出

以下是`show`和`hide`的可选特效：

	blind			对话框从顶部显示或者消失
	bounce			对话框断断续续的显示或者消失，垂直运动
	clip			对话框从中心垂直的显示或者消失
	slide			对话框从左边显示或者消失
	drop			对话框从左边显示或者消失，有透明度变化
	fold			对话框从左上角显示或者消失
	heighlight		对话框消失或者消失，伴随着透明度和背景色的变化
	puff			对话框从中心开始缩放，显示时收缩，消失时生长
	scale			对话框从中心开始缩放，显示时生长，消失时收缩
	pulsate			对话框以闪烁的形式显示或者消失

`dialog`行为选项

	autoOpen		默认为true，调用dialog()方法就会打开对话框。false对话框不可见，可以通过dialog('open')才能可见
	draggable		默认为true，可以拖动对话框
	resizable		默认为ture，可以调成对话框大小
	modal			默认为false，对话框外可以操作，ture对话框会遮罩一层灰纱，无法操作
	closeText		设置关闭按钮的title文字

`dialog()`方法的事件

	focus			当对话框被激活时（首次显示以及每次在上面点击）会调用focus方法，有两个参数(event,ui)。此事件中ui参数为空
	create
	open
	boforeClose
	close
	drag
	dragStart
	dragStop
	resize
	resizeStart
	resizeStop

以下是`#dialog_test`的小例子：

	$('#dialog_test').dialog({
		title:'注册',
		button:{
			'按钮1':function(){
				alert('你点击了');
			},
			'按钮2':function(){
				console.log('你点击了');
			}
		},
		position:'center',
		show:'puff',
		hide:'slip',
		autoOpen:false,
		closeText:'关闭',
		beforeClose:function(e,ui){
			alert('将要关闭');	
		}
	});

	$('#btn').click(function(){
		$('dialog_test').dialog('open');
	});

`dialog('action',param)`方法

	dialog('open')			打开对话框
	dialog('close')			关闭对话框
	dialog('destroy')		删除对话框，直接阻断了dialog
	dialog('isOpen')		判断对话框是否打开状态
	dialog('widget')		获取对话框的jQuery对象
	dialog('option',param)	获取options属性的值
	dialog('options',param,value)		设置options属性的
	dialog('moveToTop')		将指定对话框置前

`dialog`中使用`on()`

	dialogfocus			得到焦点时触发
	dialogopen			显示时触发
	dialogbeforeclose	将要关闭时触发
	dialogdrag			每一次移动时触发
	dialogdragstart		开始移动时触发
	dialogdragstop		移动结束后触发
	dialogresize		每一次调整大小时触发
	dialogresizestart	开始调整大小时触发
	dialogresizestop	结束调整时触发

	$('#reg').on('dialogclose',function(){
		alert('关闭');
	});

**jQuery UI button**

使用button按钮UI的时候，不一定必须是`input`按钮形式，普通的文本也可以设置成`button`按钮。

	$('#btn').button();

修改`button`样式：

	//修改默认样式
	.ui-state-default, .ui-widget-content .ui-state-default, .ui-widget-header .ui-state-default {
		background:url(../img/ui_header_bg.png);
	}
	//修改active样式
	.ui-state-active, .ui-widget-content .ui-state-active, .ui-widget-header .ui-state-active {
		background:url(../img/ui_white.png);
	}

`button`按钮选项：

	label		对应按钮上的文字，如果没有，HTML内容将被作为按钮的文字
	icons		对应按钮上的图标，按钮前面 primary 和后面 secondary 都可以放置一个图标，通过对象键值对的方式完成
	text		布尔值。false不会显示文字，但是必须指定一个图标

	$('#search_button').button({
		disable:false,
		icons:{
			primary:'ui-icon-search'
		},
		label:'查找',
		text:false
	});

注意，对于`button`的事件方法，只有`create`，当创建`button`的时候调用。

`button('action',param)`方法能设置和获取按钮。`antion`表示指定操作的方式。

	button('disable')			禁用按钮
	button('enable')			启用按钮
	button('destroy')			删除按钮，直接阻断了button
	button('refresh')			更新按钮布局
	button('widget')			获取button的jQuery对象
	button('option',param)		获取options属性的值
	button('options',param,value)		设置options属性的值

`button`按钮不但可以设置普通的按钮，还能设置单选框、复选框。

	//HTML
	<input type="radio" name="sex" value="male" id="male">
		<label for="male">男</label>
	</input>
	<input type="radio" name="sex" value="female" id="female">
		<label for="female">女</label>
	</input>

	//jQuery单选框
	$('input[type=radio]').button();

	//在单选按钮外面包一层div.out
	$('.out').buttonset();			//单选按钮会挨在一起

复选框和单选框类似。

**jQuery UI tooltip**

工具提示`tooltip`是一个非常使用的UI。它彻底扩展了HTML中的`title`属性，让提示更加丰富，更加可控制，全面提升了用户体验。

调用`tooltip()`方法，首先需要针对元素设置相应的title属性。

	<span id="tool" title="提示">tooltip</span>
	$('#tool').tooltip();

`tooltip()`方法的外观选项：

	disabled		默认为false，true将禁止显示工具提示
	content			设置title内容
	items			设置选择器以限定范围
	tooltipClass	引入class形式的CSS样式

	$('#tool').tooltip({
		disable:false,
		content:'改变文字',
		items:'input',
		tooltipClass:'reg_tooltip'
	});

`tooltip`页面位置选项

	position		使用对象的键值对赋值，有两个属性：my和at表示坐标。my是以目标点左下角为基准，at以my为基准

	$('#tool').tooltip({
		position:{
			my:'left center',
			at:'right+5 center'
		}
	});

`tooltip`视觉选项

	show		布尔值/字符串 显示对话框时，默认采用淡入效果
	hide		布尔值/字符串 关闭对话框时，默认采用淡出效果

`show`和`hide`的可选特效和`dialog`的可选参数相同。

`tooltip`行为选项：

	track		布尔值，默认为false，true能跟随数遍移动

`tooltip()`方法的事件：

	create		当工具被创建时会调用create方法
	open
	close

`tooltip('action',param)`方法：

	tooltip('open')			打开工具提示
	tooltip('close')		关闭工具提示
	tooltip('disable')		禁用
	tooltip('enable')		启用
	tooltip('destroy')		删除
	tooltip('widget')		获取工具提示的jQuery对象
	tooltip('option',param)	获取options属性的值
	tooltip('option',param,value)	设置options属性的值

`tooltip()`中使用`on()`

	tooltipopen			显示时触发
	tooltipclose		关闭时触发

	$('#tool').on('tooltipopen',function(){
		alert('打开时触发');
	});

**jQuery UI autocomplete**

自动补全是一个可以减少用户输入完整信息的UI工具。一般在邮箱、搜索关键字等，然后提取出相应完成字段字符串公用户选择。

调用：

	$('#email').autocomplete({
		...
	});

外观选项：

	disable			默认false，true时将禁止自动补全
	source			指定数据源，可以是本地的，也可以是远程的
	minLength		默认为1，触发补全列表最少输入的字符串
	autoFocus		默认false，true时第一个项目会被自动选定
	delay			默认300，设置延迟显示

	$('#email').autocomplete({
		source:['aaa@hihi.com','bbb@sasa.com','ccc@yuyu.com'],
		disable:false,
		minLength:2,
		delay:50,
		autoFocus:true
	});

页面位置选项

	position		同tooltip

	$('#email').autocomplete({
		position:{
			my:'left center',
			at:'right center'
		}
	});

`autocomplete()`方法事件

	create
	open
	close
	focus
	select
	change
	seatch			当自动补全搜索完成后，会调用search方法
	response		当自动补全搜索完成后，在菜单显示之前，会调用response方法

	autocomplete('close')
	autocomplete('diaable')
	autocomplete('enable')
	autocomplete('destroy')
	autocomplete('widget')			获取自动补全的jQuery对象
	autocomplete('search',value)	在数据源获取匹配的字符串
	autocomplete('option',param)
	autocomplete('option',param,value)

`autoconplete`中使用`on()`

	autocomoleteopen
	autocomoleteclose
	autocomoletesearch			查找时触发
	autocomoletefocus
	autocomoleteselect
	autocomoletechange
	autocomoleteresponse		搜索完毕后，显示之前

**jQuery UI datepicker**

**调用`datepicker()`方法**

	$('#date').datepicker();		//#date是一个input输入框

`input`输入框属性`readonly="readonly"`设置只能读，不能输入。

**修改`datepicker()`样式**

	//修改当天日期的样式
	.ui-datepicker-today .ui-state-highlight{
		border:1px solid #eee;
		color:#f60;
	}

	//修改选定日期的样式
	.ui-datepicker-current-day .ui-state-active{
		border:1px solid #eee;
		color:#06f;
	}

**`datepicker()`方法的属性**

	//太长了，不想写了，查资料吧
	
	//设置为中文
	$('#date').datepicker({
		dateFormat : 'yy-mm-dd',
		dayNames : ['星期日','星期一','星期二','星期三','星期四','星期五','星期六'],
		dayNamesShort : ['星期日','星期一','星期二','星期三','星期四','星期五','星期六'],
		dayNamesMin : ['日','一','二','三','四','五','六'],
		monthNames : ['一月','二月','三月','四月','五月','六月','七月','八月','九月','十月','十一月','十二月'],
		monthNamesShort : ['一','二','三','四','五','六','七','八','九','十','十一','十二'],
		altField : '#abc',
		altFormat : 'yy-mm-dd',
		appendText : '(yy-mm-dd)',
		firstDay : 1,
		showWeek : true,
		weekHeader : '周',
		});

	yaerRange		设置下拉菜单年份的区间

jQuery UI只允许使用选项中定义的事件，目前还不可以使用`.on()`方法来管理。

**验证插件---`validate.js`**

	//第一步：引入validate.js
	<script type="text/javascript" src="js/jQuery.validate.js"></script>

	//第二步：在JS文件中执行
	$('#reg').validate();		//#reg是一个form表单

`validate.js`的默认验证规则有两种形式：1.控件属性方式；2.JS键值对传参方式（推荐）。

	required:true			必须输入字段
	email:true				必须输入正确格式的电子邮件
	url:true				必须输入正确格式的网址
	date:true				必须输入正确格式的日期（IE6验证出错）
	dateISO:true			必须输入正确格式的日期（ISO）（只验证格式，不验证有效）
	number:true				必须输入合法的数字（负数，小数）
	digits:true				必须输入整数
	creditcard:true			必须输入合法的信用卡账号
	equalTo:"#pass_again"	输入值必须和#pass_again相同，可以用来验证重新输入密码
	minlength:5				输入长度最小是5
	maxlength：5				输入长度最多是5
	rangelength:[5,10]		输入值必须介于5和10之间
	range:[5,10]			输入值必须介于5和10之间
	min:5					输入值不能小于5
	max:10					输入值不能大于10
	remote:"check.php"		使用ajax方法调用check.php验证输入值

	//使用JS对象键值对传参方式设置
	$('#reg').validate({
		rules:{
			user:{
				required:true,
				minlength:2,
			},
			url:{
				url:true,
			},
			notpass:{
				equalTo:'#pass',
			}
		},
		message:{
			user:{
				required:'账号不得为空',
				minlength:'账号不得小于2位',
			},
		}
	});

`validate()`的方法和选项

除了默认的验证规则外，validate.js还提供了大量的其他属性和方法供开发者使用。比如，调试属性，错误提示位置一系列比较有用的选项。

	//jQuery.format格式化错误提示
	$('#reg').validate({
		messages:{
			user:{
				required:'账号不得为空',
				minlength:jQuery.format('账号不得小于{0}位'),
				rangelength:jQuery.fotmat('账号限制在{0}-{1}位'),
			}
		}
	});

	//开启调试模式禁止提交
	$('#reg').validate({
		debug:true,
	});

	//设置调试模式为默认，可以禁止多个表单提交
	$.validator.setDefaults({
		debug:true,
	});

	//使用其他方式代替默认提交
	submitHandler:function(){
			//可以执行ajax提交，并且无须debug:true阻止提交了
	},

	//忽略某个字段验证
	ignore:'#pass',

	//将群组的错误指定存放位置
	errorPlacement:function(error,element){
		error.appendTo('.myerror');
	},

	//设置错误提示的class名
	errorClass:'error_list',

	//设置错误提示的标签
	errorElement:'p',

	//设置成功后加载的class
	success:'success',
	
	//使用方法加载class并添加文本
	success:function(label){
		label.addClass('success').text('ok');
	},

使用`remote:url`，可以对表单进行ajax验证，默认会提交当前验证的值到远程地址。如果需要提交其他的值，可以使用`data`选项。

**Ajax表单插件---`form.js`**

form.js插件有两个核心方法：`ajaxForm()`和`ajaxSubmit()`，它们集合了从控制表单元素到决定如何管理提交进行的功能。

	//ajaxForm提交方式
	$('#reg').ajaxForm(function(){
		alert('提交成功');
	});

使用`ajaxForm()`方法，会直接实现ajax提交。自动阻止了默认行为，而它提交的默认页面是`form`控件的`action`属性的值。提交的方式是`method`属性的值。

	//ajaxSubmit()提交方式
	$('#reg').submit(function(){
		$(this).ajaxSubmit(function(){
			alert('提交成功');
		});
		return false;
	});

`ajaxForm()`方法是针对form直接提交的，所以组织了默认行为。而`ajaxSubmit()`方法，由于是针对`submit()`方法的，所以需要手动阻止默认行为。

option参数是一个以键值对传递的对象，可以通过这个对象，设置各种Ajax提交的功能。

	$('#reg').submit(function(){
		$(this).ajaxSubmit({
			url:'test.php',				//设置提交的url，可以覆盖action属性
			target:'#box',				//服务器返回的内容存放在#box里
			type:'POST',				//GET，POST
			dataType:null,				//xml,json,script,默认为null
			clearForm:ture,				//成功提交后，清空表单
			resetForm:true,				//成功提交后，重置表单
			data:{						//增加额外的数据提交
				aaa:'bbb',
				ccc:'ddd',
			},
			beforeSubmit:function(formData,jqForm,options){
										//formData是传递表单元素
										//jqForm是form的jQuery对象
										//options是目前options设置的属性
			},
			success:function(){
				
			},
			error:function(event,errorText,errorType){

			}
		});
		return false;					//手动阻止默认行为
	});

form.js除了提供两个核心方法之外，还提供了一些常用的工具方法。这些方法主要是在提交前后对数据或表单进行处理的。

	//表单序列化
	$('#reg').formSerialize();

	//序列化某一个字段
	$('#reg #user').fieldSerialize();

	//得到某个字段的value值
	$('#reg #user').fieldValue();

	//重置表单
	$('#reg').resetForm();

	//清空某个字段
	$('#reg #user').clearFields();

**cookie插件---`cookie.js`**

引入cookie.js文件。

	//生成一个cookie
	$.cookie('user','ang');

	//设置cookie参数
	$.cookie('user','ang',{
		expire:7,					//过期时间，7天后
		path：'/',					//设置路径，上一层
		domain:'www.thisang.com',	//设置域名
		secure:true,				//默认为false，需要使用安全协议https
	});

	//关闭编码/解码，默认为false
	$.cookie.raw=true;

	//读取cookie数据
	alert($.cookie('user'));

	//读取所有cookie数据
	alert($.cookie());

读取所有的cookie是以对象键值对存放的，所以，也可以$.cookie().user获取。

	//删除cookie
	$.reomoveCookie('user');

	//删除指定路径cookie
	$.removeCookie('user',{
		path:'/',
	});

如何实现注册后直接登录：

首先设置“注册”和“登录”的位置分别有着“用户”和“退出”两个模块，只是默认为隐藏。注册成功后生成一个cookie，如果有cookie存在的时候，显示“用户”和“退出”。如果没有cookie存在的时候，显示“注册”和“登录”。当点击“退出”的时候，删除cookie信息，回到未登录状态。

登录表单处放一个7天内自动登录，当成功登录后新建一个cookie，7天有效期。

**选项卡 tabs UI**

使用tabs需要按照指定的规范：

	//HTML部分
	<div id="tabs">
		<ul>
			<li><a href="#tabs1">tab1</a></li>
			<li><a href="#tabs2">tab2</a></li>
			<li><a href="#tabs3">tab3</a></li>
		</ul>
		<div id="tabs1">tab1-content</div>
		<div id="tabs2">tab2-content</div>
		<div id="tabs3">tab3-content</div>
	</div>

	//jQuery部分
	$('#tabs').tabs();

修改样式

	//去掉外边框
	#tabs{
		border:none;
	}
	//内容区域修饰
	#tabs1,#tabs2,#tabs3{
		height:100px;
		padding:10px;
		border:1px solid #aaa;
		border-top:none;
		position:relative;
		top:-2px;
	}

`tabs()`方法的属性：

	collapsible			默认为false，ture时允许现象卡折叠对应的内容
	disable				使用数组来指定禁用哪个选项卡的索引
	event				默认click，设置触发tab的事件类型
	active				默认为0，设置默认显示哪个tab
	heightStyle			默认为content，即根据内容伸展高度。auto则是根据最高的那个为基准，fill则是填充一定的可用高度
	show				默认false，淡入
	hide				默认false，淡出

show和hide的其他参数参考dialog

`tabs()`方法的事件

	create				当创建一个选项卡时激活此事件
	active				当切换一个选项卡时，启动此事件
	beforeActive		当切换一个选项卡之前，启动此事件
	load				当ajax加载一个文档后激活此事件
	beforeLoad			当ajax加载一个文档前激活此事件

使用ajax调用html

	//HTML部分
	<ul>
		<li><a href="tabs1.html">tab1</a></li>
		<li><a href="tabs2.html">tab2</a></li>
		<li><a href="tabs3.html">tab3</a></li>
	</ul>

而tabs1.html,tabs2.html,tabs3.html只要书写即可，无须包含<div>

CSS需要做一定的修改，只要将之前的ID换成如下：

	##ui-tabs-1, #ui-tabs-2, #ui-tabs-3 {}

ajax加载前触发

	$('#tabs').tabs({
		beforeLoad:function(event,ui){
			ui.ajaxSetting.url='tabs2.html';
			ui.jqXHR.success(function(responseText){
				alert(responseText);
			});
		}
	});

`tabs('action',param)`方法

	tabs('disable')			禁用选项卡
	tabs('enable')			启用选项卡
	tabs('load')			通过ajax获取选项卡的内容
	tabs('widget')			获取选项卡的jQuery对象
	tabs('destroy')			删除选项卡，直接阻断了tabs
	tabs('refresh')			更新选项卡
	tabs('option',param)	获取options属性值
	tabs('option',param,value)		设置options属性的值

	//重载指定选项卡内容
	$('#button').click(function(){
		$('#tabs').tabs('load',0);
	});

tabs中使用`on()`

	tabsload			ajax加载后触发
	tabsbeforeload		ajax加载前触发
	tabsactivate		选项卡切换时触发
	tabsbeforeactivate	选项卡切换前触发

**折叠菜单 accordion UI**

	//HTML 部分
	<div id="accordion">
		<h1>菜单1</h1>
		<div>内容1</div>
		<h1>菜单2</h1>
		<div>内容2</div>
		<h1>菜单3</h1>
		<div>内容3</div>
	</div>

	//jQuery部分
	$('#accordion').accordion();

方法属性

	collapsible
	disable
	event
	active
	heightStyle
	header				默认为h1，设置折叠菜单的标题标签，HTML部分也要改
	icons				设置想要的图标

	$('#accordion').accordion({
		icons:{
			"header":"ui-icons-plus",
			"activeHeader":"ui-icon-minus",
		}
	});

`accordion()`方法事件

	create
	active
	beforeActive

	accordion('disable')
	accordion('enable')
	accordion('widget')
	accordion('destroy')
	accordion('refresh')
	accordion('option',param)
	accordion('option',param,value)

accordion中使用`on()`

	accordionactive			折叠菜单切换时触发
	accordionbeforeactive	折叠菜单切换前触发